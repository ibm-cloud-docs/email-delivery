---

copyright:
  years: 2014, 2025
lastupdated: "2025-10-06"

keywords: getting started email delivery

subcollection: email-delivery

---

{{site.data.keyword.attribute-definition-list}}

# Getting started
{: #getting-started-email-delivery}

Use this information to configure your server to use {{site.data.keyword.cloud}} email service.
{: shortdesc}

## Preparing for email delivery
{: #preparing-for-email-delivery}

1. Confirm that you can send emails from the device before you add or update smart host settings. Fix any existing problems in the send and receive process before you proceed.
1. Follow these steps to access the Exim Configuration Editor:

   * Access WHM with your credentials.
   * Go to **Service Configuration > Exim Configuration Editor**.
   * Click **Advanced Editor** to open the editor.

### Notes
{: #email-delivery-preparing-notes}

* Specific instructions about using the Advanced Editor are on the **Exim configuration editor** screen.
* This procedure can cause Exim to fail.
* The **Exim Configuration Editor** screen displays the contents of the file _exim.conf_. You can edit _exim.conf_ by using the Exim Configuration Manager.

## Authenticating with SendGrid credentials
{: #authenticating-with-sendgrid-credentials}

Locate the **Begin Authenticators** section and enter the following commands in the corresponding text box that is labeled **Section: AUTH**

   `sendgrid_login:`

   `driver = plaintext`

   `public_name = LOGIN`

   `client_send = : username@example.com :`

   `YourSendgridPassword`

## Configuring routers
{: #configuring-email-routers}

Add the following commands to **Routers Configuration** in the section that is labeled **Section: PREROUTERS:**

   `send_via_sendgrid:`

   `driver = manualroute`

   `domains = ! +local_domains`

   `transport = sendgrid_smtp`

   `route_list = "* smtp.sendgrid.net::587 byname"`

   `host_find_failed = defer`

   `no_more`

## Configuring transports
{: #configuring-email-transports}

1. Add the following commands to **Transports Configuration** in the section that is labeled **Section: TRANSPORTSTART**

   `sendgrid_smtp:`

   `driver = smtp`

   `hosts = smtp.sendgrid.net`

   `hosts_require_auth = smtp.sendgrid.net`

   `hosts_require_tls = smtp.sendgrid.net`

1. Click the **Save** at the end of the page.

To receive `root/nobody/cpanel` mail that is forwarded to an external address, the hostname of the cPanel servers needs to be in the `/etc/localdomains` file.
{: note}

## Next steps
{: #email-configuration-next-steps}

The system runs a series of checks against the updated configuration file and restarts Exim. If you are logged in to any WebMail pages, log out, and log back in after the restart is complete. Send a test email to make sure that the proper credits are used.
