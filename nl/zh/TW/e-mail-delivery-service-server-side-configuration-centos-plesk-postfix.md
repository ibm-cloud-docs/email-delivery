---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 電子郵件遞送服務伺服器端配置：CentOS、Plesk 及 Postfix

## 概觀

下列步驟可配置您的伺服器以使用 {{site.data.keyword.SendGrid}}（{{site.data.keyword.cloud}} 電子郵件遞送服務）作為智慧型主機。下列範例是使用標準的 {{site.data.keyword.cloud}} OS Reload of CentOS 6.5 與 Plesk 12 和 Postfix 所執行。

## 配置

1.  找到您的 Postfix 配置檔。它通常位於：/etc/postfix/main.cf。
2.  使用文字編輯器開啟 main.cf 檔案，並在配置中新增下列內容。

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  儲存並關閉 /etc/postfix/main.cf 檔案。
4.  使用這個指令重新啟動 postfix：

  `/etc/init.d/postfix restart`

## 疑難排解

1.  如果您得到 "no mechanism available" 錯誤，請驗證您具有鑑別/加密用的所有必需檔案庫。您可以使用下列指令安裝這些檔案庫：

  若為 Debian/Ubuntu：`apt-get install libsasl2-modules`

  若為 Redhat/CentOS：`yum install cyrus-sasl-plain`

  安裝這些檔案庫之後，請發出相同的 restart 指令：

    /etc/init.d/postfix restart

2.  如果埠 587 無法運作，請在 postfix 配置中使用埠 2525。您也可能需要開啟配置檔 /etc/postfix/main.cf 並將下行解除註解：

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
