---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurazione lato server del servizio di recapito email: Sendmail and SendGrid

Completa la seguente procedura per configurare il tuo server per utilizzare il servizio di recapito email {{site.data.keyword.cloud}}
con Sendmail. L'esempio di seguito è stato eseguito su un'installazione bare metal di Centos 6.5 e Ubuntu 14.

## Pre-configurazione

Devi installare i seguenti pacchetti perché Sendmail utilizzi correttamente {{site.data.keyword.SendGrid}} come uno smart host.

### RHEL/Centos
Per RHEL/Centos, esegui questo comando:
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
Per Ubuntu/Debian, esegui questo comando:
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Configurazione

1. Aggiungi i tuoi nome utente e password {{site.data.keyword.SendGrid}} al file /etc/mail/access:
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. Immetti il seguente comando per generare l'associazione database /etc/mail/access.db:
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. Modifica il file /etc/mail/sendmail.mc per utilizzare {{site.data.keyword.SendGrid}} come nostro smart host.

### Configura sendmail.mc in RHEL/Centos
1. Individua e apri il file sendmail.mc.
2. Imposta come commento la seguente riga:
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. Aggiungi delle nuove righe con il seguente codice:
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Configura sendmail.mc in Ubuntu/Debian
1. Individua e apri il file sendmail.mc.
2. In fondo al file, inserisci il seguente codice al di sopra della riga 'MAILER_DEFINITIONS'
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Rigenera sendmail.cf
Il file sendmail.mc è una raccolta di macro che possono essere espanse nel file di configurazione reale (e più complesso) sendmail.cf. Per rendere le tue modifiche accessibili a Sendmail, rigenera sendmail.cf utilizzando il comando m4:
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Riavvia Sendmail
Riavvia Sendmail utilizzando il seguente comando:
`service sendmail restart`

## Esegui il test utilizzando il programma di utilità email della riga di comando
Verifica le modifiche utilizzando il seguente comando:
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
