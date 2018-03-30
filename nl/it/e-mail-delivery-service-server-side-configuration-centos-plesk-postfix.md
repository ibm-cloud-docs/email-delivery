---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurazione lato server del servizio di recapito email: CentOS, Plesk e Postfix

Attieniti alla seguente procedura per configurare il tuo server per utilizzare {{site.data.keyword.SendGrid}}, il servizio di recapito email {{site.data.keyword.cloud}} come uno smart host. Il seguente esempio è stato eseguito con un ricaricamento SO {{site.data.keyword.cloud}} standard di CentOS 6.5 con Plesk 12 e Postfix.

## Configurazione

1.  Individua il tuo file di configurazione Postfix. Spesso è posizionato qui: /etc/postfix/main.cf.
2.  Apri il file main.cf con un editor di testo e aggiungi quanto segue alla configurazione.

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  Salva e chiudi il file /etc/postfix/main.cf.
4.  Riavvia Postfix utilizzando questo comando:

  `/etc/init.d/postfix restart`

## Risoluzione dei problemi

1.  Se ricevi un errore "no mechanism available", verifica di avere tutte le librerie necessarie per l'autenticazione/codifica. Puoi installare queste librerie utilizzando i seguenti comandi:

  Per Debian/Ubuntu:  `apt-get install libsasl2-modules`

  Per Redhat/CentOS: `yum install cyrus-sasl-plain`

  Dopo aver installato queste librerie, immetti lo stesso comando di riavvio:

    /etc/init.d/postfix restart

2.  Se la porta 587 non funziona, utilizza la porta 2525 nella configurazione Postfix. Potresti anche dover aprire il file di configurazione /etc/postfix/main.cf e annullare il commento della seguente riga:

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
