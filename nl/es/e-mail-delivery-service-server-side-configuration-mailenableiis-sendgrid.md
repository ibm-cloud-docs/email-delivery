---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuración de lado del servidor del servicio de entrega de correo electrónico: MailEnable/IIS y SendGrid

Complete los pasos siguientes para configurar su servidor para utilizar el servicio de entrega de correo electrónico de {{site.data.keyword.cloud}} como si fuera un smarthost. Los siguientes ejemplos son para servidores estándar de Windows 2008 o 2012 con MailEnable o IIS configurados como su servicio SMTP.

## Configuración de IIS

1.  Abra Gestor IIS en Windows.
2.  Pulse su sitio. En la parte derecha aparecerá la página de las opciones principales de configuración.
3.  Efectúe una doble pulsación en el icono de **correo electrónico** SMTP.
4.  En el campo de la dirección de correo electrónico, escriba la dirección de correo electrónico que será el remitente.
5.  Pulse el botón de selección **Entregar correo electrónico a servidor SMTP**.
6.  En el campo **Servidor SMTP**, escriba: smtp.sendgrid.net.
7.  En el campo **Puerto** escriba: 587
8.  En la **Configuración de autenticación** seleccione **Especificar credenciales** y pulse **Establecer**.
9.  Añada su nombre de usuario y su contraseña de {{site.data.keyword.SendGrid}} y pulse **Guardar**.

## MailEnable

1.  Abra la aplicación MailEnableAdmin.
2.  Expanda el separador **Servidores** en el panel de navegación de la izquierda.
3.  Pulse localhost > Sistema > Pulse con el botón derecho en SMTP.
4.  En el recuadro **Propiedades de SMTP** pulse en **Smarthost**.
5.  Active el recuadro al lado de **Smarthost activado**.
6.  En **IP/dominio**, escriba: smtp.sendgrid.net. 
7.  En el campo **Puerto** escriba: 587
8.  Marque el recuadro "El servidor remoto requiere autenticación".
9.  Escriba su nombre de usuario y su contraseña de {{site.data.keyword.SendGrid}} y pulse **Aplicar**.
10.  Vaya a **Servicios de Windows** y reinicie MailEnable.
