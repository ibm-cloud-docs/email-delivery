---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 配置服务器以使用 IBM Cloud 电子邮件传递服务：CentOS、cPanel、Exim

## 概述

使用此信息来配置服务器，配置后即可使用 {{site.data.keyword.cloud}} 电子邮件服务。 

## 准备

1.  先确认是否能从设备发送电子邮件，然后再添加或更新智能主机设置。如果发送/接收过程中存在问题，请先修复问题，然后再继续。
2. 执行这些步骤以访问 Exim 配置编辑器：
  * 使用唯一凭证来访问 WHM。
  * 导航到**服务配置 > Exim 配置编辑器**。
  * 单击屏幕底部的**高级编辑器**按钮以打开编辑器。
  
**注：**
- 有关使用“高级编辑器”的特定指示信息位于 **Exim 配置编辑器**屏幕中。
- 此过程会导致 Exim 失败。
- **Exim 配置编辑器**屏幕中会显示 _exim.conf_ 文件的内容。可以使用 Exim 配置管理器来编辑 _exim.conf_。

## 使用 SendGrid 凭证进行认证

找到**开始鉴别符**部分，在标签为**部分：AUTH** 的相应文本框中输入以下命令 

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## 配置路由器

将以下命令添加到标签为**部分：PREROUTERS:** 的部分的**路由器配置**中
`send_via_sendgrid:`  

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## 配置传输

将以下命令添加到标签为**部分：TRANSPORTSTART** 的部分的**传输配置**中

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

单击页面底部的**保存**。

<em>**注：**为了接收转发到外部地址的 root/nobody/cpanel 邮件，cPanel 服务器的主机名需要在 /etc/localdomains 文件中。</em>

## 后续操作

系统对更新后的配置文件运行一系列检查，然后重新启动 Exim。如果您登录到任何 WebMail 页面，请先注销，并在重新启动完成后重新登录。发送测试电子邮件，以确保 [{{site.data.keyword.slportal_full}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window} 中的[电子邮件传递服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/services/emaildelivery){: new_window} 屏幕中所使用的信用值正确。
