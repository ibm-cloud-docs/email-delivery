---

copyright:
  years: 2014, 2024
lastupdated: "2024-07-15"

keywords: Email delivery server configuration, IIS MailEnable, SendGrid

subcollection: email-delivery

---

{{site.data.keyword.attribute-definition-list}}

# Configuring server-side email delivery service for IIS MailEnable and SendGrid
{: #Email-delivery-server-configuration-IISMailEnable-SendGrid}

Complete the following steps to configure your server to use {{site.data.keyword.cloud}} email delivery service as a Smart Host. These examples are for standard Windows 2008 or 2012 server with MailEnable or IIS configured as your SMTP service.

## Configuring IIS
{: #configure-iis}

1. Open IIS Manager in Windows.
1. Click your site.
1. Double-click the **SMTP email** icon.
1. In the email address field, enter the email address of the sender.
1. Click **Deliver email to SMTP server radio**.
1. In the **SMTP server** field, enter `smtp.sendgrid.net`.
1. In the **Port** field, enter `587`.
1. Under **Authentication settings**, choose **Specify credentials** and click **Set**.
1. Add your {{site.data.keyword.SendGrid}} username and password. Click **Save**.

## Enabling a smart host
{: #enable-smart-host}

1. Open the MailEnableAdmin application.
1. Expand the **Servers** tab in the navigation pane.
1. Click **localhost > System**, then right-click **SMTP**.
1. In the **SMTP properties** box, click **Smart host**.
1. Enable the box next to **Smart host enabled**.
1. Under **IP/Domain**, enter `smtp.sendgrid.net`.
1. In the **Port** field, enter `587`.
1. Check the box that says "The remote server requires authentication".
1. Enter your {{site.data.keyword.SendGrid}} username and password. Click **Apply**.
1. Go to **Windows services** and restart MailEnable.
