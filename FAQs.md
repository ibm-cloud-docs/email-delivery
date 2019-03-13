---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-30"

keywords: email delivery faq

subcollection: email-delivery

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# FAQs
{: #email-delivery-faw}

## Can I use outbound email on port 25?

Starting 28 October 2015, {{site.data.keyword.BluSoftlayer_notm}} no longer allows outbound connections through TCP port 25 (SMTP) on new accounts.

## Why is a standard email port blocked?

By default, the standard SMTP TCP port 25 is blocked due to the large amount of abuse that is targeted at this port. {{site.data.keyword.BluSoftlayer_notm}} offers a trusted third-party email relay service from {{site.data.keyword.SendGrid}} if you need to send outbound email from their domains or applications.  

## What options do I have if I want to send email from my server or application?

If you need send email from your servers, you need to use a smart host outside of {{site.data.keyword.BluSoftlayer_notm}}. A smart host is a host that relays SMTP traffic from an SMTP server, mail client, or any other service or programming language capable of handling SMTP. Servers typically send this type of traffic by using the mail submission TCP ports 465 or 587. You can communicate with 465, 587, or any custom port other than TCP port 25. If you want to use your own email server on a custom port, use the documentation specific to your email service to configure a custom email port.

## Does IBM Cloud offer a smart host service?

{{site.data.keyword.BluSoftlayer_notm}} now offers an email delivery service that is powered by {{site.data.keyword.SendGrid}} that allows clients to use a smart host to relay your outbound mail services. This service has many other functions such as generating metrics, tracking email lists, tracking email activity, assisting with newsletters, and authenticating.


1. Log in to **WHM**.
2. Click **Service Manager**.
3. Set the port after **Run another copy of Exim on port**.
4. Click **Save**.

## I can't see email and I am seeing port 25 blocked. Why?

By default, the standard SMTP TCP port 25 is blocked due to the large amount of abuse that is targeted at this port. {{site.data.keyword.BluSoftlayer_notm}} offers a trusted third-party email relay service from {{site.data.keyword.SendGrid}} if you need to send outbound email from their domains or applications.
