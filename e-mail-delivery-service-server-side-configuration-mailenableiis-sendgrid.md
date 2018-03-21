---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Email delivery service server-side configuration: MailEnable/IIS and SendGrid

Complete the following steps to configure your server to use {{site.data.keyword.cloud}} email delivery service as a smart host. The examples below are for standard Windows 2008 or 2012 server with MailEnable or IIS configured as your SMTP service.

## IIS Configuration

1.  Open IIS Manager in Windows.
2.  Click on your site. The main configuration options page is displayed to the right.
3.  Double-click the **SMTP E-mail** icon.
4.  In the email address field, type the email address that will be the sender.
5.  Click **Deliver e-mail to SMTP server radio**.
6.  In the **SMTP Server** field, type: smtp.sendgrid.net.
7.  In the **Port** field type: 587
8.  Under **Authentication Settings**, choose **Specify Credentials** and click **Set**.
9.  Add your {{site.data.keyword.SendGrid}} username and password and click **Save**.

## MailEnable

1.  Open the MailEnableAdmin application.
2.  Expand the **Servers** tab in the left hand navigation pane.
3.  Click localhost > System > Right click on SMTP.
4.  In the **SMTP Properties** box, click **Smart Host**.
5.  Enable the box next to **Smart Host Enabled**.
6.  Under **IP/Domain**, type: smtp.sendgrid.net. 
7.  In the **Port** field type: 587
8.  Check the box that says "The remote server requires authentication".
9.  Enter your {{site.data.keyword.SendGrid}} username and password and click **Apply**.
10.  Go to **Windows Services** and restart MailEnable.
