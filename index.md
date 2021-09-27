---

copyright:
  years: 2014, 2021
lastupdated: "2020-05-15"

keywords: getting started email delivery

subcollection: email-delivery

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:note: .note}
{:table: .aria-labeledby="caption"}

# Getting started tutorial
{: #getting-started-email-delivery}

Use this information to configure your server to use {{site.data.keyword.cloud}} email service.

## Preparation

1.  Confirm that you can send emails from the device before you add or update smart host settings. Fix any existing problems in the send and receive process before you proceed.
2. Follow these steps to access the Exim Configuration Editor:
   * Access WHM with your unique credentials.
   * Navigate to **Service Configuration > Exim Configuration Editor**.
   * Click **Advanced Editor** to open the editor.

### Notes
- Specific instructions for using the Advanced Editor are on the **Exim Configuration Editor** screen.
- This procedure can cause Exim to fail.
- The **Exim Configuration Editor** screen displays the contents of the file _exim.conf_. You can edit _exim.conf_ by using the Exim Configuration Manager.

## Authenticate by using SendGrid Credentials

Locate the **Begin Authenticators** section and enter the following commands in the corresponding text box labeled **Section: AUTH**

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :`

`YourSendgridPassword`

## Configure the Routers

Add the following commands to **Routers Configuration** in the section labeled **Section: PREROUTERS:**
`send_via_sendgrid:`

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## Configure the Transports

Add the following commands to **Transports Configuration** in the section labeled **Section: TRANSPORTSTART**

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

Click the **Save** at the end of the page.

To receive root/nobody/cpanel mail forwarded to external address, the hostname of the cPanel servers needs to be in /etc/localdomains file.
{: note}

## Next Steps

The system runs a series of checks against the updated configuration file and restarts Exim. If you are logged in to any WebMail pages, log out and log back in after the restart is complete. Send a test email to ensure that the proper credits are used.
