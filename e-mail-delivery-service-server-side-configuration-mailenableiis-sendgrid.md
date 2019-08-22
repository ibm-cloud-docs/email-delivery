---

copyright:
  years: 2014, 2019
lastupdated: "2019-08-21"

keywords: Email delivery server configuration, IIS MailEnable, SendGrid

subcollection: email-delivery

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuring server-side email delivery service for IIS MailEnable and SendGrid
{: #Email-delivery-server-configuration-IISMailEnable-SendGrid}

Complete the following steps to configure your server to use {{site.data.keyword.cloud}} email delivery service as a smart host. These examples are for standard Windows 2008 or 2012 server with MailEnable or IIS configured as your SMTP service.

## IIS Configuration

1.  Open IIS Manager in Windows.
2.  Click your site. The main configuration options page is displayed to the right.
3.  Double-click **SMTP Email**.
4.  In the email address field, enter the email address of the sender.
5.  Click **Deliver email to SMTP server radio**.
6.  In the **SMTP Server** field, enter `smtp.sendgrid.net`.
7.  In the **Port** field enter `587`.
8.  Under **Authentication Settings**, select **Specify Credentials** and click **Set**.
9.  Add your {{site.data.keyword.SendGrid}} user name and password and click **Save**.

## MailEnable

1.  Open the MailEnableAdmin application.
2.  Expand the **Servers** tab in the left navigation pane.
3.  Click **localhost > System**, then right-click **SMTP**.
4.  In the **SMTP Properties** box, click **Smart Host**.
5.  Enable the box next to **Smart Host Enabled**.
6.  Under **IP/Domain**, enter `smtp.sendgrid.net`.
7.  In the **Port** field enter `587`.
8.  Check the box that says "The remote server requires authentication".
9.  Enter your {{site.data.keyword.SendGrid}} user name and password and click **Apply**.
10.  Go to **Windows Services** and restart MailEnable.
