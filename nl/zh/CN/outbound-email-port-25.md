---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 端口 25 上的出站电子邮件

## 概述

从 2015 年 10 月 28 日开始，{{site.data.keyword.BluSoftlayer_notm}} 不再允许新帐户通过 TCP 端口 25 (SMTP) 建立出站连接。

## 为什么阻止了标准电子邮件端口？

缺省情况下，由于存在以标准 SMTP TCP 端口 25 为目标的大量滥用情况，因此阻止了该端口。如果您需要发送来自 {{site.data.keyword.BluSoftlayer_notm}} 域或应用程序的电子邮件，那么它提供了来自 [SendGrid] 的受信任的第三方电子邮件中继服务。  

## 如果我要从我的服务器或应用程序发送电子邮件，那么有哪些选项？

如果您要从您的服务器发送电子邮件，那么需要使用 {{site.data.keyword.BluSoftlayer_notm}} 以外的智能主机。智能主机是能够中继来自 SMTP 服务器、邮件客户机或者能够处理 SMTP 的其他任何服务或编程语言的 SMTP 流量的主机。服务器通常会使用邮件提交 TCP 端口 465 或 587 来发送此类型的流量。您可以与上述端口或者除 TCP 端口 25 以外的其他任何定制端口进行通信。如果要在定制端口上使用您自己的电子邮件服务器，请使用特定于您电子邮件服务的文档来配置定制电子邮件端口。

## SoftLayer 提供智能主机服务吗？

{{site.data.keyword.BluSoftlayer_notm}} 现在提供采用 SendGrid 技术的电子邮件传递服务，这样客户机就可以使用智能主机来中继出站邮件服务。此服务有很多功能，如生成度量值、跟踪电子邮件列表、跟踪电子邮件活动、协助业务通讯、认证等。
