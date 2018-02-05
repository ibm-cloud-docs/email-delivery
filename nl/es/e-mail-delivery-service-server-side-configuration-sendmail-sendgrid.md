---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuración de lado del servidor del servicio de entrega de correo electrónico: Sendmail y SendGrid

## Visión general

Utilice este procedimiento para configurar su servidor para utilizar el servicio de entrega de correo electrónico de {{site.data.keyword.cloud}} con Sendmail. El siguiente ejemplo se ha realizado en una instalación nativa de Centos 6.5 y Ubuntu 14.

## Preconfiguración

Deberá instalar los paquetes siguientes para que Sendmail utilice correctamente {{site.data.keyword.SendGrid}} como si fuera un smarthost.

### RHEL/Centos
Para RHEL/Centos, ejecute este mandato:
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
Para Ubuntu/Debian, ejecute este mandato:
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Configuración

1. Añada su nombre de usuario y su contraseña de {{site.data.keyword.SendGrid}} al archivo /etc/mail/access:
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. Ejecute el siguiente mandato para generar la correlación de base de datos /etc/mail/access.db:
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. Edite el archivo /etc/mail/sendmail.mc para utilizar {{site.data.keyword.SendGrid}} como nuestro propio smarthost. 

### Configure sendmail.mc en RHEL/Centos
1. Busque y abra el archivo sendmail.mc.
2. Comente la siguiente línea:
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. También el archivo sendmail.mc y añada nuevas líneas con el código siguiente: `define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Configure sendmail.mc en Ubuntu/Debian
1. Busque y abra el archivo sendmail.mc.
2. Al final del archivo ponga el código siguiente sobre la línea que dice 'MAILER_DEFINITIONS' `define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Vuelva a generar sendmail.cf
El archivo sendmail.mc es una recopilación de macros que pueden ampliarse en el archivo de configuración real (y más complejo) sendmail.cf. Para que los cambios sean accesibles para sendmail, vuelva a generar sendmail.cf con el mandato m4:
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Reinicie Sendmail
Reinicie Sendmail con el mandato siguiente:
`service sendmail restart`

## Realice una prueba con el programa de utilidad de correo de la línea de mandatos
Realice una prueba para ver los cambios con el siguiente mandato:
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
