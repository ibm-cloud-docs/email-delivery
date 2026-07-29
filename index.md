---

copyright:
  years: 2014, 2026
lastupdated: "2026-07-29"

keywords: getting started email delivery

subcollection: email-delivery

---

{{site.data.keyword.attribute-definition-list}}

# Getting started
{: #getting-started-email-delivery}

Use the following information to configure your server to use SendGrid, an {{site.data.keyword.cloud}} email delivery service.
{: shortdesc}

## Email delivery options
{: #how-to-choose}

You have two options when you need to send outbound transactional email.

* IBM Cloud Email Delivery for Classic - creates a connection to a SendGrid account.
* IBM Cloud Event Notifications - an IBM Cloud service that is hosted, operated, and supported by IBM.

Both options offer similar transactional email capabilities such as 1-to-1 or 1-to-many sending and API and SMTP interfaces.

Email Delivery for Classic is best if you have the following needs.

* Marketing campaigns and transactional email from a single platform
* Marketing features such as contact management, campaign creation, segmentation, or marketing analytic
* Specialized functions like inbound email parsing

Event Notifications is best if you have the following needs:

* A fully managed service that is integrated with IBM Cloud billing, IAM, and IBM Cloud support.
* A focus on transactional emails, such as password resets, two-factor authentication messages, receipts, and policy notices that are sent from your own application.
* Send emails that are based on events and notices from your IBM Cloud platform or from other IBM-managed services such as cloud logs and monitoring.
* To securely connect to the email service by using virtual private endpoints.
* A single multi-channel integration that extends beyond email to SMS, push notifications, webhooks, and other event-driven notification channels.

For current IBM Cloud customers, [IBM Cloud Event Notifications email](https://cloud.ibm.com/docs/event-notifications?topic=event-notifications-en-destinations-email) is the preferred choice for transactional enterprise needs.
{: tip}

## Preparing for email delivery
{: #preparing-for-email-delivery}

1. Confirm that you can send emails from the device before you add or update smart host settings. Fix any existing problems in the send and receive process before you proceed.
1. Follow these steps to access the Exim configuration editor:

   * Access WHM with your credentials.
   * Go to **Service configuration > Exim configuration editor**.
   * Click **Advanced editor** to open the editor.

### Notes
{: #email-delivery-preparing-notes}

* Specific instructions about using the advanced editor are on the **Exim configuration editor** screen.
* This procedure can cause Exim to fail.
* The **Exim configuration editor** screen displays the contents of the file `exim.conf`. You can edit `exim.conf` by using the Exim Configuration Manager.

## Authenticating with SendGrid credentials
{: #authenticating-with-sendgrid-credentials}

Locate the **Begin authenticators** section and enter the following commands in the corresponding text box that is labeled **Section: AUTH**

   `sendgrid_login:`

   `driver = plaintext`

   `public_name = LOGIN`

   `client_send = : username@example.com :`

   `YourSendgridPassword`

## Configuring routers
{: #configuring-email-routers}

Add the following commands to **Routers configuration** in the section that is labeled **Section: PREROUTERS:**

   `send_via_sendgrid:`

   `driver = manualroute`

   `domains = ! +local_domains`

   `transport = sendgrid_smtp`

   `route_list = "* smtp.sendgrid.net::587 byname"`

   `host_find_failed = defer`

   `no_more`

## Configuring transports
{: #configuring-email-transports}

1. Add the following commands to **Transports configuration** in the section that is labeled **Section: TRANSPORTSTART**

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
