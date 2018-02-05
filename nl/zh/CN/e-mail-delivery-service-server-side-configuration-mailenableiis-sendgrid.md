---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 电子邮件传递服务服务器端配置：MailEnable/IIS、SendGrid

## 概述

使用此过程来配置服务器，配置后即可使用 {{site.data.keyword.cloud}} 电子邮件传递服务作为智能主机。下面的示例是针对标准 Windows 2008 或 2012 服务器以及 MailEnable 或 IIS 配置为 SMTP 服务的情况。

## IIS 配置

1.  在 Windows 中打开 IIS 管理器。
2.  单击站点。配置选项主页将显示在右侧。
3.  双击“SMTP 电子邮件”图标。
4.  在电子邮件地址字段中，输入发件人的电子邮件地址。
5.  单击“将电子邮件发送到 SMTP 服务器”单选按钮。
6.  在“SMTP 服务器”字段中，输入：smtp.sendgrid.net。
7.  在“端口”字段中，输入：587
8.  在“认证设置”下，选择“指定凭证”并单击“设置”。
9.  添加 {{site.data.keyword.SendGrid}} 用户名和密码，然后单击“保存”。

## MailEnable

1.  打开 MailEnableAdmin 应用程序。
2.  展开左侧导航窗格中的“服务器”选项卡。
3.  单击 localhost > 系统 > 右键单击 SMTP
4.  在“SMTP 属性”框中，单击“智能主机”选项卡。
5.  启用“智能主机已启用”旁边的框。
6.  在“IP/域”下，输入：smtp.sendgrid.net。 
7.  在“端口”字段中，输入：587
8.  选中内容为“远程服务器需要认证”的框
9.  输入 {{site.data.keyword.SendGrid}} 用户名和密码，然后单击“应用”。
10.  转至“Windows 服务”并重新启动 MailEnable。
