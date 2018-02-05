---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 電子郵件遞送服務伺服器端配置：Sendmail 及 SendGrid

## 概觀

請使用此程序配置您的伺服器以使用 {{site.data.keyword.cloud}} 電子郵件遞送服務搭配 Sendmail。下列範例是在僅安裝 Centos 6.5 和 Ubuntu 14 的情況下執行。

## 配置前

您將需要安裝下列套件，Sendmail 才能適當地使用 {{site.data.keyword.SendGrid}} 作為智慧型主機。

### RHEL/Centos
若為 RHEL/Centos，請執行下列指令：
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
若為 Ubuntu/Debian，請執行下列指令：
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## 配置

1. 將您的 {{site.data.keyword.SendGrid}} 使用者名稱及密碼新增至 /etc/mail/access 檔案：
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. 執行下列指令，以產生 /etc/mail/access.db 資料庫對映：
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. 編輯 /etc/mail/sendmail.mc 檔案，以使用 {{site.data.keyword.SendGrid}} 作為我們的智慧型主機。

### 在 RHEL/Centos 中配置 sendmail.mc
1. 找到並開啟 sendmail.mc 檔案。
2. 註銷下行：
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. 同樣對 sendmail.mc 檔案，將下列程式碼新增為新行：
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### 在 Ubuntu/Debian 中配置 sendmail.mc
1. 找到並開啟 sendmail.mc 檔案。
2. 在檔案的底端，將下列程式碼放在 'MAILER_DEFINITIONS' 這行之上：
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### 重新產生 sendmail.cf
sendmail.mc 檔案是巨集的集合，可以展開成為真實（且更複雜）的 sendmail.cf 配置檔。若要讓您的變更可供 sendmail 存取，請使用 m4 指令重新產生 sendmail.cf：
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## 重新啟動 Sendmail
使用下列指令重新啟動 Sendmail：
`service sendmail restart`

## 使用指令行 mail 公用程式進行測試
使用下列指令測試變更：
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
