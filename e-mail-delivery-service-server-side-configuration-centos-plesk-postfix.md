---

copyright:
  years: 2014, 2024
lastupdated: "2024-07-15"

keywords: email delivery server configuration, centos, plesk, postfix

subcollection: email-delivery

---

{{site.data.keyword.attribute-definition-list}}

# Configuring server-side email delivery service for CentOS, Plesk, and Postfix
{: #email-delivery-server-config}

Use the following steps to configure your server to use {{site.data.keyword.SendGrid}}, the {{site.data.keyword.cloud}} email delivery service as a smart host.

The following example is a standard {{site.data.keyword.cloud}} OS Reload of CentOS 6.5 with Plesk 12 and Postfix.
}{: note}

## Configuration
{: #email-delivery-config}

1. Locate your Postfix configuration file. A common location is `/etc/postfix/main.cf`.
1. Open the main.cf file with a text editor and add the following to the configuration.

   `smtp_sasl_auth_enable = yes`

   `smtp_sasl_password_maps = static:_Your {{site.data.keyword.SendGrid}} Username_:_Your {{site.data.keyword.SendGrid}} Password_`

   `smtp_sasl_security_options = noanonymous`

   `smtp_tls_security_level = encrypt`

   `header_size_limit = 4096000`

   `relayhost = [smtp.sendgrid.net]:587`

1. Save and close the /etc/postfix/main.cf file.
1. Restart Postfix by using this command:

   `/etc/init.d/postfix restart`

## Troubleshooting
{: #email-delivery-troubleshoot}

1. If you get the "no mechanism available" error, verify that you have all of the necessary libraries for authentication or encryption. You can install these libraries by using the following commands:

   For Debian and Ubuntu, use this command:  `apt-get install libsasl2-modules`

   For Red Hat and CentOS, use this command: `yum install cyrus-sasl-plain`

   After you install these libraries, use the same restart command:

    `/etc/init.d/postfix restart`

1. If port 587 does not work, use port 2525 in the Postfix configuration. You might also need to open the configuration file `/etc/postfix/main.cf` and uncomment the following line:

   `#tlsmgr unix - - n 1000? 1 tlsmgr`
