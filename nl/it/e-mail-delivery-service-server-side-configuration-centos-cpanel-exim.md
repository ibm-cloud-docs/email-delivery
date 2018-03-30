---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurazione del tuo server in modo che utilizzi il servizio di recapito email di IBM Cloud: CentOS, cPanel e Exim

Utilizza queste informazioni per configurare il tuo server per utilizzare il servizio email {{site.data.keyword.cloud}}. 

## Preparazione

1.  Conferma di poter inviare le email dal dispositivo prima di aggiungere o aggiornare le impostazioni smart host. Correggi tutti i problemi esistenti nel processo di invio/ricezione prima di procedere.
2. Attieniti a questa procedura per accedere a Exim Configuration Editor:
  * Accedi a WHM utilizzando le tue credenziali univoche.
  * Passa a **Service Configuration > Exim Configuration Editor**.
  * Fai clic su **Advanced Editor** per aprire l'editor.
  
**Note:**
- Le istruzioni specifiche per l'utilizzo di Advanced Editor si trovano nella schermata **Exim Configuration Editor**.
- Questa procedura può causare un errore con Exim.
- La schermata **Exim Configuration Editor** visualizza i contenuti del file _exim.conf_. Puoi modificare _exim.conf_ utilizzando Exim Configuration Manager.

## Autenticati utilizzando le credenziali SendGrid

Individua la sezione **Begin Authenticators** e immetti i seguenti comandi nella casella di testo corrispondente etichettata **Section: AUTH**

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## Configura i router

Aggiungi i seguenti comandi a **Routers Configuration** nella sezione etichettata **Section: PREROUTERS:**
`send_via_sendgrid:`

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## Configura i trasporti

Aggiungi i seguenti comandi a **Transports Configuration** nella sezione etichettata **Section: TRANSPORTSTART**

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

Fai clic su **Save** alla fine della pagina.

<em>**Nota:** per poter ricevere email root/nobody/cpanel inoltrate da un indirizzo esterno, il nome host dei server cPanel deve essere nel file /etc/localdomains.</em>

## Passi successivi

Il sistema esegue una serie di controlli nel file di configurazione aggiornato e riavvia Exim. Se hai eseguito l'accesso a una qualsiasi pagina WebMail, disconnettiti e riaccedi dopo il completamente del riavvio. Invia un'email di verifica per assicurarti che vengano utilizzati i crediti corretti dalla schermata [E-mail Delivery Service ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/services/emaildelivery){: new_window} in [{{site.data.keyword.slportal_full}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){: new_window}.
