---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Email in uscita sulla porta 25

A partire dal 28 ottobre 2015, {{site.data.keyword.BluSoftlayer_notm}} non consente più le connessioni in uscita tramite la porta TCP 25 (SMTP) nei nuovi account.

## Perché la porta email standard è bloccata?

Per impostazione predefinita, la porta TCP SMTP standard 25 è bloccata a causa di una grande quantità di abusi indirizzati a tale porta. {{site.data.keyword.BluSoftlayer_notm}} offre un servizio di inoltro email di terze parti attendibile da SendGrid se hai bisogno di inviare un'email in uscita dai tuoi domini o applicazioni.  

## Quali opzioni devo avere se voglio inviare l'email dal mio server o dalla mia applicazione?

Se devi inviare l'email dai tuoi server, dovrai utilizzare un smart host all'esterno di {{site.data.keyword.BluSoftlayer_notm}}. Uno smart host è un host che inoltra il traffico SMTP da un server SMTP, da un client email o da un qualsiasi altro servizio o linguaggio di programmazione in grado di gestire SMTP. I server normalmente inviano questo tipo di traffico utilizzando le porte TCP di invio email 465 o 587.  Puoi comunicare con queste porte o con qualsiasi porta personalizzata diversa dalla porta TCP 25. Se vuoi utilizzare il tuo proprio server email su una porta personalizzata, utilizza la documentazione specifica del tuo servizio email per configurare una porta email personalizzata.

## IBM Cloud offre un servizio smart host?

{{site.data.keyword.BluSoftlayer_notm}} offre ora un servizio di recapito email potenziato da SendGrid che consente ai client di utilizzare uno smart host per inoltrare i tuoi servizi email in uscita. Questo servizio dispone di molte altre funzioni come la generazione delle metriche, il tracciamento degli elenchi email, il tracciamento dell'attività email, l'assistenza con le newsletter e l'autenticazione.
