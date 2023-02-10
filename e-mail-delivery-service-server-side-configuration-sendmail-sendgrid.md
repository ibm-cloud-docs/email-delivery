---

copyright:
  years: 2014, 2023
lastupdated: "2023-02-09"

keywords: Email delivery server configuration, Sendmail, SendGrid

subcollection: email-delivery

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Configuring server-side email delivery service for Sendmail and SendGrid
{: #Email-delivery-server-configuration-Sendmail-SendGrid}

Complete the following steps to configure your server to use the {{site.data.keyword.cloud}} email delivery service with Sendmail. This example is a bare metal installation of CentOS 6.5 and Ubuntu 14.

## Pre-configuration
{: #sendmail-preconfiguration}

You need to install the following packages for Sendmail to properly use {{site.data.keyword.SendGrid}} as a smart host.

### RHEL and CentOS
{: #rhel-centos-sendmail-preconfig}

For RHEL and CentOS, run the following command:

   `yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu and Debian
{: #ubuntu-debian-sendmail-preconfig}

For Ubuntu and Debian, run the following command:

   `apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Configuring SendGrid
{: #configure-email-delivery-sendgrid}

1. Add your {{site.data.keyword.SendGrid}} username and password to the file /etc/mail/access:
   `AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. Run the following command to generate the /etc/mail/access.db database map:
   `makemap hash /etc/mail/access.db < /etc/mail/access`
3. Edit the /etc/mail/sendmail.mc file to use {{site.data.keyword.SendGrid}} as our smart host.

### Configuring sendmail.mc in RHEL and CentOS
{: #configure-sendmail-rhel-centos}

1. Locate and open the _sendmail.mc_ file.
2. Comment out the following line:
   `dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. Add new lines with the following code:
   `define('SMART_HOST', 'smtp.sendgrid.net')dnl`
   `FEATURE('access_db')dnl`
   `define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
   `define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Configuring sendmail.mc in Ubuntu and Debian
{: #configure-sendmailmc-ubuntu-debian}

1. Locate and open the sendmail.mc file.
2. At the end of the file, insert the following code before the line that reads 'MAILER_DEFINITIONS'
   `define('SMART_HOST', 'smtp.sendgrid.net')dnl`
   `FEATURE('access_db')dnl`
   `define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
   `define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Regenerate sendmail.cf
{: #regenerate-sendmailcf}

The sendmail.mc file is a collection of macros that expand into the real (and more complex) sendmail.cf config file. To make your changes accessible to Sendmail, regenerate sendmail.cf by using the m4 command:
   `m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Restart Sendmail
{: #restart-sendmail}

Restart Sendmail by using the following command:
   `service sendmail restart`

## Test changes by using the command line mail utility
{: #test-changes-with-cl-mail-utility}

Test the changes by using the following command:
   `echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
