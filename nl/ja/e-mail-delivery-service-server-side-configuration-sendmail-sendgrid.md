---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# E メール配信サービスのサーバー・サイド構成: Sendmail および SendGrid

## 概説

Sendmail で {{site.data.keyword.cloud}} E メール配信サービスを使用するためにサーバーを構成するには、以下の手順を使用してください。
以下の例は、Centos 6.5 と Ubuntu 14 のベア・インストールで行ったものです。

## 事前構成

Sendmail が {{site.data.keyword.SendGrid}} をスマート・ホストとして正しく使用するには、以下のパッケージのインストールが必要です。

### RHEL/Centos
RHEL/Centos の場合は、以下のコマンドを実行します。
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
Ubuntu/Debian の場合は、以下のコマンドを実行します。
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## 構成

1. ご使用の {{site.data.keyword.SendGrid}} ユーザー名とパスワードをファイル /etc/mail/access に次のように追加します。
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. 以下のコマンドを実行して、/etc/mail/access.db データベース・マップを生成します。
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. {{site.data.keyword.SendGrid}} をスマート・ホストとして使用するように、/etc/mail/sendmail.mc ファイルを編集します。

### RHEL/Centos での sendmail.mc の構成
1. sendmail.mc ファイルを見つけて開きます。
2. 以下の行をコメント化します。
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. また、sendmail.mc ファイルに、以下のコードの新規行を追加します。
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Ubuntu/Debian での sendmail.mc の構成
1. sendmail.mc ファイルを見つけて開きます。
2. ファイル下部で、「MAILER_DEFINITIONS」という行の上に以下のコードを挿入します。
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### sendmail.cf の再生成
sendmail.mc ファイルは、実際の (さらに複雑な) sendmail.cf 構成ファイルに展開可能なマクロの集合です。変更を sendmail から使用可能にするには、次の m4 コマンドを使用して sendmail.cf を再生成します。
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Sendmail の再始動
以下のコマンドを使用して Sendmail を再始動します。
`service sendmail restart`

## コマンド・ライン・メール・ユーティリティーを使用したテスト
以下のコマンドを使用して、変更をテストします。
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
