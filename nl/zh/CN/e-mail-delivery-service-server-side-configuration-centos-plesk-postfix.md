---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 电子邮件传递服务服务器端配置：CentOS、Plesk、Postfix

执行以下步骤以将服务器配置为使用 {{site.data.keyword.cloud}} 电子邮件传递服务 {{site.data.keyword.SendGrid}} 作为智能主机。下面的示例是使用标准 {{site.data.keyword.cloud}} OS Reload of CentOS 6.5 以及 Plesk 12 和 Postfix 执行的。

## 配置

1.  找到 Postfix 配置文件。该文件通常位于：/etc/postfix/main.cf。
2.  用文本编辑器打开 main.cf 文件，将下列内容添加到配置中。

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  保存并关闭 /etc/postfix/main.cf 文件。
4.  使用此命令重新启动 Postfix：

  `/etc/init.d/postfix restart`

## 故障诊断

1.  如果收到“无可用机制”错误，请验证是否已具有认证/加密所需的所有库。您可以使用下列命令来安装这些库：

  对于 Debian/Ubuntu：`apt-get install libsasl2-modules`

  对于 Redhat/CentOS：`yum install cyrus-sasl-plain`

  安装这些库之后，请发出相同的重新启动命令：

    /etc/init.d/postfix restart

2.  如果端口 587 不好用，请在 Postfix 配置中使用端口 2525。可能还需要打开配置文件 /etc/postfix/main.cf，并取消注释以下行：

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
