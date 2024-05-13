---

copyright:
  years: 2014, 2024
lastupdated: "2024-05-13"

keywords: email delivery faq

subcollection: email-delivery

---

{{site.data.keyword.attribute-definition-list}}

# FAQs
{: #email-delivery-faq}
{: faq}

## Can I use outbound email on port 25?
{: #can-i-use-port25}
{: faq}

As of 28 October 2015, {{site.data.keyword.cloud}} no longer allows outbound connections through TCP port 25 (SMTP) on new accounts.

## Why is the standard email port 25 blocked?
{: #why-is-port25-blocked}
{: faq}

By default, the standard SMTP TCP port 25 is blocked due to the large amount of abuse that is targeted at this port. {{site.data.keyword.cloud}} offers a trusted third-party email relay service from {{site.data.keyword.SendGrid}} if you need to send outbound email from their domains or applications.

## What options do I have if I want to send email from my server or application?
{: #what-options-send-email}
{: faq}

If you need send email from your servers, you need to use a smart host outside of {{site.data.keyword.cloud}}. A smart host is a host that relays SMTP traffic from an SMTP server, mail client, or any other service or programming language capable of handling SMTP. Servers typically send this type of traffic by using the mail submission TCP ports 465 or 587. You can communicate with 465, 587, or any custom port other than TCP port 25. If you want to use your own email server on a custom port, use the documentation specific to your email service to configure a custom email port.

## Why are my emails flagged as spam?
{: #why-emails-flagged-as-spam}
{: faq}

Your emails can be flagged as spam if you don't use authentication with RDNS, DMARC, BIMI, SPF, or DKIM. If your emails don't comply with internet privacy laws, then they might be blocked or flagged as spam. The following are some common privacy laws.

- Controlling the Assault of Non-Solicited Pornography and Marketing (CAN-SPAM)
- Canada Anti-Spam Law (CASL)
- General Data Protection Regulation (GDPR)
- California Consumer Protection Act (CCPA)

## Why are my emails not being delivered?
{: #why-email-not-being-delivered}

- Your email size might be higher than threshold restrictions. Failure notices often give more details about size restrictions.
- The recipient server might block your emails because of compliance and regulation reasons. For more information, see [Why are my emails flagged as spam?](#why-emails-flagged-as-spam).

## Why do emails take a long time to deliver?
{: #why-emails-taking-long-deliver}

Internet traffic congestion and SMTP server configuration issues can cause delivery delays. For more information, see [SendGrid - Troubleshooting Delays and Latency](https://docs.sendgrid.com/ui/account-and-settings/troubleshooting-delays-and-latency){: external} or check with your email vendor.

## Why do recipients not see emails in the inbox, but I see that they show as delivered?
{: #why-recipients-not-see-email-but-shows-delivered}

The recipient might have filters set up that move emails into folders other than the inbox. For more information, see [SendGrid - Troubleshooting Email Messages Marked "Delivered", But Not Appearing in Inbox](https://support.sendgrid.com/hc/en-us/articles/4408443310619-Troubleshooting-Email-Messages-Marked-Delivered-But-Not-Appearing-in-Inbox){: external}.

## Does {{site.data.keyword.cloud}} offer a smart host service?
{: #offer-smart-host-service}
{: faq}

{{site.data.keyword.cloud}} now offers an email delivery service that is powered by {{site.data.keyword.SendGrid}} that allows clients to use a smart host to relay your outbound mail services. This service has many other functions such as generating metrics, tracking email lists, tracking email activity, assisting with newsletters, and authenticating.

## Why do I need to warm up an IP address?
{: #why-warm-up-IP-address}
{: faq}

Warming up an IP address gradually increases the volume of email that is sent from a dedicated IP address that follows a predetermined schedule. The gradual increase helps establish a good reputation with ISPs as a legitimate email sender.

## How do I warm up a new IP address?
{: #how-warm-up-ip-address}
{: faq}

The proper volume and frequency of your email program depends on your total email volume. But, you need to send enough email at a volume that ISPs can properly determine your reputation. See the following suggestions to help build your reputation.

- Start by sending a welcome message to your hyper-engaged recipients. Then, send the message to your recently engaged recipients.
- If you don't have engagement data, keep in mind that your recent signups are most active right after they sign up to your email list.

For more information, see [SendGrid’s Email Guide for IP Warm Up](https://sendgrid.com/en-us/resource/email-guide-ip-warm-up).

## How do I get a dedicated IP address?
{: #how-get-dedicated-ip-address}
{: faq}

If you want a dedicated IP address, send a request to `ibm_partner@twilio.com`. Make sure that you include the account contact information and your SendGrid account email address.

## Is SendGrid the only choice for email delivery with {{site.data.keyword.cloud}}?
{: #is-sendgrid-only-choice-email-delivery}
{: faq}

No. But, you need to use SendGrid through {{site.data.keyword.cloud}} to have your email service appear on the same {{site.data.keyword.cloud}} invoice.

If you want to use a third-party email delivery product, you need to use a smart host that is outside of {{site.data.keyword.cloud}}. A smart host relays SMTP traffic from an SMTP server, email client, or any other service or programming language that can handle SMTP.

## How do I use my own email server?
{: #how-use-own-email-server}
{: faq}

Contact [support](/docs/get-support?topic=get-support-using-avatar#getting-support) to request an exemption to open port 25 so you can host your own email server.

## How do I get help from SendGrid?
{: #how-get-help-sendgrid}
{: faq}

Log in to your [SendGrid account](https://support.sendgrid.com/hc/en-us) and submit a support request.

## Where can I find the Terms of Service for SendGrid and Twilio?
{: #where-sendgrid-tos}
{: faq}

For the Terms of Service for SendGrid and Twilio, see [Twilio Terms of Service](https://www.twilio.com/legal/tos).

## Where can I find more information about SendGrid?
{: #where-more-information-sendgrid}
{: faq}

For more information about SendGrid, see the following links.

- [SendGrid documentation](https://docs.sendgrid.com/)
- [SendGrid Email API documentation](https://www.twilio.com/sendgrid/email-api)
- [SendGrid for developers](https://docs.sendgrid.com/for-developers)
