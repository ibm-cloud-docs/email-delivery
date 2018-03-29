---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuración de su servidor para utilizar el servicio de entrega de correo electrónico de IBM Cloud: CentOS, cPanel y Exim

Utilice esta información para configurar su servidor para utilizar el servicio de correo electrónico de {{site.data.keyword.cloud}}. 

## Preparación

1.  Confirme que puede enviar correo electrónico desde el dispositivo antes de añadir o actualizar la configuración de smarthost. Arregle los problemas existentes en el proceso de enviar/recibir antes de proceder.
2. Siga estos pasos para acceder al editor de configuración de Exim:
  * Acceda a WHM con sus credenciales exclusivas.
  * Vaya a **Configuración de servicio > Editor de configuración de Exim**.
  * Pulse en **Editor avanzado** para abrir el editor.
  
**Notas:**
- Las instrucciones específicas para utilizar el Editor avanzado se encuentran en la pantalla **Editor de configuración de Exim**.
- Este procedimiento puede producir un error en Exim.
- La pantalla **Editor de configuración de Exim** muestra los contenidos del archivo _exim.conf_. Puede editar _exim.conf_con el Gestor de configuración de Exim.

## Autenticar con credenciales de SendGrid

Busque la sección **Iniciar autenticadores** y especifique los mandatos siguientes en el recuadro de texto correspondiente etiquetado **Sección: AUTH**

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## Configurar los direccionadores

Añada los mandatos siguientes a **Configuración de direccionadores** en la sección etiquetada **Sección: PREROUTERS:**
`send_via_sendgrid:`

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## Configurar los transportes

Añada los mandatos siguientes a **Configuración de transportes** en la sección etiquetada **Sección: TRANSPORTSTART**

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

Pulse **Guardar** en la parte inferior de la página.

<em>**Nota:** Para recibir correo root/nobody/cpanel reenviado a una dirección externa el nombre de host de los servidores cPanel debe estar en el archivo /etc/localdomains.</em>

## Pasos siguientes

El sistema ejecuta una serie de comprobaciones en el archivo de configuración actualizado y reinicia Exim. Si ha iniciado sesión en cualquier página de WebMail, cierre la sesión y vuelva a iniciarla una vez finalizado el reinicio. Envíe un correo electrónico de prueba para asegurarse de que se utilizan los créditos correctos desde la pantalla de [E-mail Delivery Service ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/services/emaildelivery){: new_window} en [{{site.data.keyword.slportal_full}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window}.
