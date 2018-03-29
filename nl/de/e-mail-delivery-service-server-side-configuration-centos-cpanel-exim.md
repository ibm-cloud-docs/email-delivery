---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Server für die Verwendung des E-Mail-Zustellungsservice von IBM Cloud konfigurieren: CentOS, cPanel und Exim

Verwenden Sie diese Informationen, um Ihren Server für die Verwendung des {{site.data.keyword.cloud}}-E-Mail-Service zu konfigurieren. 

## Vorbereitung

1.  Stellen Sie sicher, dass das Senden von E-Mails auf dem verwendeten Gerät möglich ist, bevor Sie Smart-Host-Einstellungen hinzufügen oder aktualisieren. Beheben Sie gegebenenfalls bestehende Probleme beim Sende-/Empfangsprozessm, bevor Sie fortfahren.
2. Führen Sie diese Schritte aus, um auf den Exim-Konfigurationseditor zuzugreifen:
  * Rufen Sie WHM mit Ihren eindeutigen Berechtigungsnachweisen auf.
  * Navigieren Sie zu **Servicekonfiguration > Exim-Konfigurationseditor**.
  * Klicken Sie auf **Erweiterter Editor**, um den Editor zu öffnen.
  
**Hinweise:**
- Spezifische Anweisungen zur Verwendung des erweiterten Editors befinden sich in der Anzeige **Exim-Konfigurationseditor**.
- Diese Prozedur kann dazu führen, dass Exim fehlschlägt.
- In der Anzeige **Exim-Konfigurationseditor** wird der Inhalt der Datei _exim.conf_ angezeigt. Sie können _exim.conf_ mit dem Exim-Konfigurationsmanager bearbeiten.

## Authentifizierung mit den SendGrid-Berechtigungsnachweisen

Suchen Sie den Abschnitt **Begin Authenticators** und geben Sie die folgenden Befehle im entsprechenden Textfeld mit der Bezeichnung **Section: AUTH** ein.

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## Router konfigurieren

Fügen Sie die folgenden Befehle zu **Routers Configuration** im Abschnitt mit der Bezeichnung **Section: PREROUTERS:**
`send_via_sendgrid:` hinzu.

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## Transport konfigurieren

Fügen Sie die folgenden Befehle zu **Transports Configuration** im Abschnitt mit der Bezeichnung **Section: TRANSPORTSTART** hinzu.

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

Klicken Sie auf **Speichern** im unteren Bereich der Seite.

<em>**Hinweis:** Für den Empfang von root/nobody/cpanel-Mail, die an eine externe Adresse weitergeleitet wird, muss der Hostname der cPanel-Servers in der Datei '/etc/localdomains' enthalten sein.</em>

## Weitere Schritte

Das System führt eine Reihe von Prüfungen für die aktualisierte Konfigurationsdatei durch und startet Exim erneut. Wenn Sie bei WebMail-Seiten angemeldet sind, melden Sie sich ab und nach dem Abschluss des Neustarts erneut an. Senden Sie eine Test-E-Mail, um sicherzustellen, dass die korrekten Angaben aus der Anzeige des [E-Mail-Zustellungsservice ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/services/emaildelivery){: new_window} im [{{site.data.keyword.slportal_full}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} verwendet werden.
