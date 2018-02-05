---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Serverseitige Konfiguration für den E-Mail-Zustellungsservice: CentOS, Plesk und Postfix

## Übersicht

Mit den folgenden Schritten können Sie Ihren Server für die Verwendung von {{site.data.keyword.SendGrid}}, den {{site.data.keyword.cloud}}-E-Mail-Zustellungsservice, als Smart Host konfigurieren. Für das nachfolgend beschriebene Beispiel wurde ein standardmäßiges erneutes Laden des Betriebssystems von CentOS 6.5 mit Plesk 12 und Postfix in {{site.data.keyword.cloud}} verwendet.

## Konfiguration

1.  Suchen Sie die Postfix-Konfigurationsdatei. Sie befindet sich in der Regel an der folgenden Speicherposition: /etc/postfix/main.cf.
2.  Öffnen Sie 'main.cf' mit einem Texteditor und fügen Sie die folgenden Einträge zur Konfiguration hinzu.

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  Speichern und schließen Sie die Datei /etc/postfix/main.cf.
4.  Starten Sie Postfix mit diesem Befehl erneut:

  `/etc/init.d/postfix restart`

## Fehlerbehebung

1.  Wenn der Fehler "no mechanism available" ausgegeben wird, stellen Sie sicher, dass alle erforderlichen Bibliotheken für die Authentifizierung/Verschlüsselung vorhanden sind. Sie können diese Bibliothek mit den folgenden Befehlen installieren:

  Für Debian/Ubuntu: `apt-get install libsasl2-modules`

  Für Redhat/CentOS: `yum install cyrus-sasl-plain`

  Geben Sie nach der Installation dieser Bibliotheken denselben Neustartbefehl ein:

    /etc/init.d/postfix restart

2.  Wenn Port 587 nicht funktioniert, verwenden Sie Port 2525 in der Postfix-Konfiguration. Möglicherweise müssen Sie auch die Konfigurationsdatei '/etc/postfix/main.cf' öffnen und die Kommentarzeichen von der folgenden Zeile entfernen:

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
