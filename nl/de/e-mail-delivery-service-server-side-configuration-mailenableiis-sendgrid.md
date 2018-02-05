---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Serverseitige Konfiguration für den E-Mail-Zustellungsservice: MailEnable/IIS und SendGrid

## Übersicht

Verwenden Sie diese Prozedur, um Ihren Server für die Verwendung des {{site.data.keyword.cloud}}-E-Mail-Zustellungsservice als Smart Host zu konfigurieren. Die nachfolgend beschriebenen Beispiele beziehen sich auf Windows 2008- oder Windows 2012-Standardserver, wobei MailEnable oder IIS als SMTP-Service konfiguriert ist.

## IIS-Konfiguration

1.  Öffnen Sie IIS Manager in Windows.
2.  Klicken Sie auf Ihre Site. Die Hauptseite mit den Konfigurationsoptionen wird auf der rechten Seite angezeigt.
3.  Klicken Sie doppelt auf das Symbol für SMTP-E-Mail.
4.  Geben Sie im E-Mail-Adressfeld die E-Mail-Adresse für den Absender ein.
5.  Klicken Sie auf das Optionsfeld für das Senden der E-Mail an den SMTP-Server.
6.  Geben Sie im SMTP-Serverfeld den Wert 'smtp.sendgrid.net' ein.
7.  Geben Sie im Feld für den Port den Wert 587 ein.
8.  Wählen Sie unter den Authentifizierungseinstellungen 'Berechtigungsnachweise angeben' aus und klicken Sie auf 'Festlegen'.
9.  Fügen Sie Ihren {{site.data.keyword.SendGrid}}-Benutzernamen und das Kennwort hinzu und klicken Sie auf 'Speichern'.

## MailEnable

1.  Öffnen Sie die MailEnableAdmin-Anwendung.
2.  Erweitern Sie die Registerkarte mit den Servern im Navigationsbereich auf der linken Seite.
3.  Klicken Sie auf 'localhost > System >' und klicken Sie mit der rechten Maustaste auf SMTP.
4.  Klicken Sie im Feld mit den SMTP-Eigenschaften auf die Registerkarte 'Smart Host'.
5.  Aktivieren Sie das Feld neben 'Smart Host aktiviert'.
6.  Geben Sie unter 'IP/Domäne' den Wert 'smtp.sendgrid.net' ein. 
7.  Geben Sie im Feld für den Port 587 ein.
8.  Wählen Sie das Feld 'Authentifizierung für den fernen Server erforderlich' aus.
9.  Geben Sie Ihren {{site.data.keyword.SendGrid}}-Benutzernamen und das Kennwort ein und klicken Sie auf 'Anwenden'.
10.  Rufen Sie die Windows-Dienste auf und starten Sie MailEnable erneut.
