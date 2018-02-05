---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuración de lado del servidor del servicio de entrega de correo electrónico: CentOS, Plesk y Postfix

## Visión general

Siga estos pasos para configurar su servidor para utilizar {{site.data.keyword.SendGrid}}, el servicio de entrega de correo electrónico de {{site.data.keyword.cloud}} como si fuera un smarthost. El siguiente ejemplo se ha realizado con una recarga estándar de SO {{site.data.keyword.cloud}} de CentOS 6.5 con Plesk 12 y Postfix.

## Configuración

1.  Busque su archivo de configuración Postfix. Normalmente se encuentra aquí: /etc/postfix/main.cf.
2.  Abra el archivo main.cf con un editor de texto y añada lo siguiente a la configuración.

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  Guarde y cierre el archivo /etc/postfix/main.cf.
4.  Reinicie postfix con este mandato:

  `/etc/init.d/postfix restart`

## Resolución de problemas

1.  Si obtiene un error "ningún mecanismo disponible", verifique que dispone de todas las bibliotecas necesarias para autenticación/cifrado. Puede instalar estas bibliotecas con los siguientes mandatos:

  Para Debian/Ubuntu:  `apt-get install libsasl2-modules`

  Para Redhat/CentOS: `yum install cyrus-sasl-plain`

  Una vez instaladas estas bibliotecas, emita el mismo mandato de reinicio:

    /etc/init.d/postfix restart

2.  Si el puerto 587 no funciona, utilice el puerto 2525 en la configuración de postfix. Puede que necesite también el archivo de configuración /etc/postfix/main.cf y elimine el comentario de la siguiente línea:

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
