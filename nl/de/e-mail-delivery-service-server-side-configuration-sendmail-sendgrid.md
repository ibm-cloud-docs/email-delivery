---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Serverseitige Konfiguration für den E-Mail-Zustellungsservice: Sendmail und SendGrid

Führen Sie die folgenden Schritte aus, um Ihren Server für die Verwendung des {{site.data.keyword.cloud}}-E-Mail-Zustellungsservice
mit Sendmail zu konfigurieren. Das nachfolgend beschriebene Beispiel wurde für eine Bare-Metal-Installation von Centos 6.5 und Ubuntu 14 durchgeführt.

## Konfigurationsvorbereitung

Sie müssen die folgenden Pakete für Sendmail installieren, um {{site.data.keyword.SendGrid}} ordnungsgemäß als Smart Host verwenden zu können.

### RHEL/Centos
Führen Sie für RHEL/Centos diesen Befehl aus:
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
Führen Sie für Ubuntu/Debian diesen Befehl aus:
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Konfiguration

1. Fügen Sie Ihren {{site.data.keyword.SendGrid}}-Benutzernamen und das Kennwort zur Datei '/etc/mail/access' hinzu:
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. Führen Sie den folgenden Befehl aus, um die Datenbankzuordnung '/etc/mail/access.db' zu generieren:
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. Bearbeiten Sie die Datei '/etc/mail/sendmail.mc' so, dass {{site.data.keyword.SendGrid}} als Smart Host verwendet wird.

### sendmail.mc in RHEL/Centos konfigurieren
1. Suchen und öffnen Sie die Datei sendmail.mc.
2. Setze Sie die folgende Zeile auf Kommentar:
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. Fügen Sie neue Zeilen mit dem folgenden Code hinzu:
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### sendmail.mc in Ubuntu/Debian konfigurieren
1. Suchen und öffnen Sie die Datei sendmail.mc.
2. Fügen Sie am Dateiende den folgenden Code oberhalb der Zeile 'MAILER_DEFINITIONS' ein:
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### 'sendmail.cf' erneut generieren
Die Datei 'sendmail.mc' ist eine Gruppe von Makros, die in die eigentliche (und komplexere) Konfigurationsdatei 'sendmail.cf' erweitert werden können. Damit Sendmail auf die Änderungen zugreifen kann, generieren Sie sendmail.cf mit dem Befehl m4 erneut:
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Sendmail erneut starten
Starten Sie Sendmail mit dem folgenden Befehl erneut:
`service sendmail restart`

## Test mit dem Befehlszeilendienstprogramm 'mail' durchführen
Testen Sie die Änderungen mit dem folgenden Befehl:
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
