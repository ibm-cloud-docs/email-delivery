---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 电子邮件传递服务服务器端配置：Sendmail、SendGrid

## 概述

使用此过程来配置服务器，配置后即可使用 {{site.data.keyword.cloud}} 电子邮件传递服务以及 Sendmail。下面的示例是在 Centos 6.5 和 Ubuntu 14 的裸机安装上执行的。

## 预配置

您需要安装以下软件包，Sendmail 才能正常使用 {{site.data.keyword.SendGrid}} 作为智能主机。

### RHEL/Centos
对于 RHEL/Centos，运行此命令：
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
对于 Ubuntu/Debian，运行此命令：
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## 配置

1. 将 {{site.data.keyword.SendGrid}} 用户名和密码添加到 /etc/mail/access 文件：
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. 运行以下命令以生成 /etc/mail/access.db 数据库映射：
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. 编辑 /etc/mail/sendmail.mc 文件以使用 {{site.data.keyword.SendGrid}} 作为智能主机。

### 在 RHEL/Centos 中配置 sendmail.mc
1. 找到并打开 sendmail.mc 文件。
2. 注释掉以下行：
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. 还是在 sendmail.mc 文件中，添加代码如下的新行：
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### 在 Ubuntu/Debian 中配置 sendmail.mc
1. 找到并打开 sendmail.mc 文件。
2. 在文件底部的“MAILER_DEFINITIONS”行上方放置下列代码：
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### 重新生成 sendmail.cf
sendmail.mc 文件是宏的集合，它可以扩展为真实的（更复杂的）sendmail.cf 配置文件。要让 Sendmail 可访问您所做的更改，请使用 m4 命令重新生成 sendmail.cf：
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## 重新启动 Sendmail
使用以下命令重新启动 Sendmail：
`service sendmail restart`

## 使用命令行邮件实用程序进行测试
使用以下命令测试更改：
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
