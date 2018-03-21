---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Email delivery service server-side configuration: CentOS, Plesk, and Postfix

Follow these steps to configure your server to use {{site.data.keyword.SendGrid}}, the {{site.data.keyword.cloud}} email delivery service as a smart host. The example below was performed with a standard {{site.data.keyword.cloud}} OS Reload of CentOS 6.5 with Plesk 12 and Postfix.

## Configuration

1.  Locate your Postfix configuration file. It is often located here: /etc/postfix/main.cf.
2.  Open main.cf file with a text editor and add the following to the configuration.

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  Save and close the /etc/postfix/main.cf file.
4.  Restart Postfix using this command:

  `/etc/init.d/postfix restart`

## Troubleshooting

1.  If you get a "no mechanism available" error, verify that you have all of the neccesary libraries for authentication/encryption. You can install these libraries using the following commands:

  For Debian/Ubuntu:  `apt-get install libsasl2-modules`

  For Redhat/CentOS: `yum install cyrus-sasl-plain`

  After you install these libraries, issue the same restart command:

    /etc/init.d/postfix restart

2.  If port 587 does not work, use port 2525 in the Postfix configuration. You might also need to open the configuration file /etc/postfix/main.cf  and uncomment the following line:

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
