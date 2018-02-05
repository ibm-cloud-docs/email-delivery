---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Abgehende E-Mail an Port 25

## Übersicht

Ab 28. Oktober 2015 lässt {{site.data.keyword.BluSoftlayer_notm}} für neue Konten keine abgehenden Verbindungen über TCP-Port 25 (SMTP) mehr zu.

## Warum wird ein Standard-E-Mail-Port blockiert?

Standardmäßig wird der TCP-Standardport 25 für SMTP aufgrund des hohen Aufkommens böswilliger Zugriffe an diesem Port blockiert. {{site.data.keyword.BluSoftlayer_notm}} bietet einen auf [SendGrid] basierenden E-Mail-Weiterleitungsservice eines vertrauenswürdigen Drittanbieters an, falls Sie abgehende E-Mails von den entsprechenden Domänen oder Anwendungen senden möchten.  

## Welche Optionen stehen zur Verfügung, wenn ich E-Mails von meinem Server oder meiner Anwendung senden möchte?

Wenn Sie E-Mails von Ihren Servern senden möchten, müssen Sie einen Smart Host außerhalb von {{site.data.keyword.BluSoftlayer_notm}} verwenden. Bei einem Smart Host handelt es sich um einen Host, der SMTP-Datenverkehr von einem SMTP-Server, einem E-Mail-Client oder einem anderen Service bzw. einer anderen Programmiersprache, der bzw. die SMTP verarbeiten kann, weiterleitet. Server senden solchen Datenverkehr normalerweise über die für die E-Mail-Übermittlung konfigurierten TCP-Ports 465 bzw. 587. Sie können diese Ports oder einen beliebigen anderen benutzerdefinierten Port - mit Ausnahme von TCP-Port 25 - für die Kommunikation verwenden. Wenn Sie einen eigenen E-Mail-Server an einem benutzerdefinierten Port verwenden möchten, lesen Sie die Informationen zur Konfiguration eines benutzerdefinierten E-Mail-Ports in der Dokumentation Ihres E-Mail-Service.

## Bietet SoftLayer einen Smart-Host-Service?

{{site.data.keyword.BluSoftlayer_notm}} bietet nun einen auf SendGrid basierenden E-Mail-Zustellungsservice, der es Clients ermöglicht, einen Smart Host für die Weiterleitung der abgehenden E-Mail-Services zu nutzen. Dieser Service umfasst eine Reihe weiterer Funktionen, z. B. das Generieren von Metriken, das Verfolgen von E-Mail-Listen, die Überwachung von E-Mail-Aktivitäten, Unterstützung für Newsletters und Authentifizierung.
