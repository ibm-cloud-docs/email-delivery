---

copyright:
  years: 2014, 2023
lastupdated: "2023-02-09"

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

Complete the following steps to configure your server to use {{site.data.keyword.cloud}} email delivery service as a Smart Host. These examples are for standard Windows 2008 or 2012 server with MailEnable or IIS configured as your SMTP service.

## Configuring IIS
{: #configure-iis}

1. Open IIS Manager in Windows.
2. Click your site. The main configuration options page is displayed to the right.
3. Double-click the **SMTP email** icon.
4. In the email address field, type the email address of the sender.
5. Click **Deliver email to SMTP server radio**.
6. In the **SMTP server** field, type `smtp.sendgrid.net`.
7. In the **Port** field type `587`.
8. Under **Authentication settings**, choose **Specify credentials** and click **Set**.
9. Add your {{site.data.keyword.SendGrid}} username and password and click **Save**.

## Enabling Smart Host
{: #enable-smart-host}

1. Open the MailEnableAdmin application.
2. Expand the **Servers** tab in the left navigation panel.
3. Click localhost > System, then right-click SMTP.
4. In the **SMTP properties** box, click **Smart host**.
5. Enable the box next to **Smart host enabled**.
6. Under **IP/Domain**, type `smtp.sendgrid.net`.
7. In the **Port** field type `587`.
8. Check the box that says "The remote server requires authentication".
9. Enter your {{site.data.keyword.SendGrid}} username and password and click **Apply**.
10. Go to **Windows services** and restart MailEnable.
