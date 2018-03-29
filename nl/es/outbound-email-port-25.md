---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Correo electrónico saliente en puerto 25

Desde el 28 de octubre de 2015, {{site.data.keyword.BluSoftlayer_notm}} ya no permite conexiones salientes a través del puerto TCP 25 (SMTP) en cuentas nuevas.

## ¿Por qué está bloqueado un puerto de correo electrónico estándar?

De forma predeterminada, el puerto estándar SMTP TCP 25 está bloqueado a causa de una gran cantidad de abuso que se destina a este puerto. {{site.data.keyword.BluSoftlayer_notm}} ofrece un servicio de retransmisión de correo electrónico de tercero de confianza desde SendGrid si necesita enviar correo electrónico saliente desde sus dominios o aplicaciones.  

## ¿Qué opciones tengo si quiero enviar correo electrónico desde mi servidor o aplicación?

Si necesita enviar correo electrónico desde sus servidores, necesita utilizar un smarthost externo a {{site.data.keyword.BluSoftlayer_notm}}. Un smarthost es un host que retransmite tráfico de SMTP de un servidor SMTP, cliente de correo electrónico o cualquier otro servicio o lenguaje de programación capaz de gestionar SMTP. Los servidores envían típicamente este tipo de tráfico mediante el envío de correo de puertos TCP 465 o 587.  Puede comunicarse con dichos puertos o cualquier puerto personalizado distinto al puerto TCP 25. Si quiere utilizar su propio servidor de correo electrónico en un puerto personalizado, utilice la documentación específica de su servicio de correo electrónico para configurar un puerto de correo electrónico personalizado.

## ¿IBM Cloud ofrece un servicio de smarthost?

{{site.data.keyword.BluSoftlayer_notm}} ofrece ahora un servicio de entrega de correo electrónico basado en SendGrid que permite a los clientes utilizar un smarthost para retransmitir sus servicios de correo saliente. Este servicio tiene muchas otras funciones tales como generar métricas, realizar el seguimiento de listas de correo electrónico, realizar el seguimiento de la actividad de correo electrónico, ayudar con los boletines y autenticar.
