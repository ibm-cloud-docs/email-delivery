---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurazione lato server del servizio di recapito email: MailEnable/IIS e SendGrid

Completa la seguente procedura per configurare il tuo server per utilizzare il servizio di recapito email {{site.data.keyword.cloud}} come uno smart host. I seguenti esempi sono per il server Windows 2008 o 2012 con MailEnable o IIS configurati come tuo servizio SMTP.

## Configurazione IIS

1.  Apri il gestore IIS in Windows.
2.  Fai clic sul tuo sito. Viene visualizzata la pagina delle opzioni principali a destra.
3.  Fai doppio clic sull'icona **Posta SMTP**.
4.  Nel campo dell'indirizzo email, immetti l'indirizzo email che sarà il mittente.
5.  Fai clic sul pulsante di opzione **Recapita messaggio a server SMTP**.
6.  Nel campo **Server SMTP**, immetti: smtp.sendgrid.net.
7.  Nel campo **Port**, immetti: 587
8.  In **Impostazioni di autenticazione**, scegli **Specifica credenziali** e fai clic su **Imposta**.
9.  Aggiungi i tuoi nome utente e password {{site.data.keyword.SendGrid}} e fai clic su **Salva**.

## MailEnable

1.  Apri l'applicazione MailEnableAdmin.
2.  Espandi la scheda **Servers** nel riquadro di navigazione di sinistra.
3.  Fai clic su localhost > System > Fai clic con il pulsante destro del mouse su SMTP.
4.  Nella casella **SMTP Properties**, fai clic su **Smart Host**.
5.  Spunta la casella accanto a **Smart Host Enabled** per abilitarla.
6.  In **IP/Domain**, immetti: smtp.sendgrid.net. 
7.  Nel campo **Port**, immetti: 587
8.  Spunta la casella "The remote server requires authentication".
9.  Immetti i tuoi nome utente e password {{site.data.keyword.SendGrid}} e fai clic su **Apply**.
10.  Vai a **Windows Services** e riavvia MailEnable.
