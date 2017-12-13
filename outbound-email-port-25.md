---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Outbound email on port 25

## Overview

As of October 28th, 2015, {{site.data.keyword.BluSoftlayer_notm}} no longer allows outbound connections through TCP port 25 (SMTP) on new accounts.

## Why is a standard email port blocked?

By default, the standard SMTP TCP port 25 is blocked due to the large amount of abuse that is targeted at this port. {{site.data.keyword.BluSoftlayer_notm}} offers a trusted third party email relay service from [SendGrid] if you need to send outbound email from their domains or applications.  

## What options do I have if I want to send email from my server or application?

If you need send email from your servers, you will need to use a smart host outside of {{site.data.keyword.BluSoftlayer_notm}} A smart host is a host that relays SMTP traffic from an SMTP server, mail client, or any other service or programming language capable of handling SMTP. Servers typically send this type of traffic using the mail submission TCP ports 465 or 587.  You can communicate with those or any custom port other than TCP port 25. If you want to use your own email server on a custom port, use the documentation specific to your email service to configure a custom email port.

## Does SoftLayer offer a smart host service?

{{site.data.keyword.BluSoftlayer_notm}} now offers an email delivery service powered by SendGrid that allows clients to use a smart host to relay your outbound mail services. This service has many other functions such as generating metrics, tracking email lists, tracking email activity, assisting with newsletters, and authenticating.
