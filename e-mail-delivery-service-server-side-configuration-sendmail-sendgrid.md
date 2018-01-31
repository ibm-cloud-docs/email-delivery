---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Email delivery service server-side configuration: Sendmail and SendGrid

## Overview

Use this procedure to configure your server to use the {{site.data.keyword.cloud}} email delivery service 
with Sendmail. The example below was performed on a bare metal install of Centos 6.5 and Ubuntu 14.

## Pre-Configuration

You will need to install the following packages for Sendmail to properly use {{site.data.keyword.SendGrid}} as a smart host.

### RHEL/Centos
For RHEL/Centos, run this command:
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
For Ubuntu/Debian, run this command:
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Configuration

1. Add your {{site.data.keyword.SendGrid}} username and password to the file /etc/mail/access:
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. Run the following command to generate the /etc/mail/access.db database map:
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. Edit the /etc/mail/sendmail.mc file to use {{site.data.keyword.SendGrid}} as our smart host.

### Configure sendmail.mc in RHEL/Centos
1. Locate and open the sendmail.mc file.
2. Comment out the following line: 
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. Also to the sendmail.mc file, and add new lines with the following code:
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Configure sendmail.mc in Ubuntu/Debian
1. Locate and open the in the sendmail.mc file.
2. At the bottom of the file place the following code above the line that reads 'MAILER_DEFINITIONS'
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Re-generate sendmail.cf
The sendmail.mc file is a collection of macros that can be expanded into the real (and more complex) sendmail.cf config file. To make your changes accessible to sendmail, re-generate sendmail.cf using the m4 command:
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Restart the Sendmail
Restart Sendmail using the following command:
`service sendmail restart`

## Test using the command line mail utility
Test the changes using the following command:
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
