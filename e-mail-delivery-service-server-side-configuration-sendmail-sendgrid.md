---

copyright:
  years: 2014, 2019
lastupdated: "2018-03-21"

keywords: Email delivery server configuration, Sendmail, SendGrid

subcollection: email-delivery

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Email delivery service server-side configuration for Sendmail and SendGrid
{: #Email-delivery-server-configuration-Sendmail-SendGrid}

Complete the following steps to configure your server to use the {{site.data.keyword.cloud}} email delivery service with Sendmail. This example is a bare metal installation of CentOS 6.5 and Ubuntu 14.

## Pre-Configuration

You need to install the following packages for Sendmail to properly use {{site.data.keyword.SendGrid}} as a smart host.

### RHEL and CentOS
For RHEL/CentOS, run this command:
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu and Debian
For Ubuntu and Debian, run this command:
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Configuration

1. Add your {{site.data.keyword.SendGrid}} user name and password to the file /etc/mail/access:
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. Run the following command to generate the /etc/mail/access.db database map:
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. Edit the /etc/mail/sendmail.mc file to use {{site.data.keyword.SendGrid}} as our smart host.

### Configure sendmail.mc in RHEL and CentOS
1. Locate and open the sendmail.mc file.
2. Comment out the following line: 
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. Add new lines with the following code:
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Configure sendmail.mc in Ubuntu and Debian
1. Locate and open the sendmail.mc file.
2. At the end of the file, place the following code before the line that reads 'MAILER_DEFINITIONS'
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Regenerate sendmail.cf
The sendmail.mc file is a collection of macros that can be expanded into the real (and more complex) sendmail.cf config file. To make your changes accessible to Sendmail, regenerate sendmail.cf using the m4 command:
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Restart the Sendmail
Restart Sendmail by using the following command:
`service sendmail restart`

## Test by using the command line mail utility
Test the changes by using the following command:
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
