---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# E メール配信サービスのサーバー・サイド構成: CentOS、Plesk、および Postfix

{{site.data.keyword.SendGrid}} の {{site.data.keyword.cloud}} E メール配信サービスをスマート・ホストとして使用するには、これらのステップに従ってサーバーを構成します。以下の例は、CentOS 6.5 の標準 {{site.data.keyword.cloud}} OS 再ロードと、Plesk 12 および Postfix で行ったものです。

## 構成

1.  Postfix 構成ファイルを見つけます。 多くの場合、以下にあります。/etc/postfix/main.cf
2.  テキスト・エディターで main.cf ファイルを開き、以下を構成に追加します。

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  /etc/postfix/main.cf ファイルを保存して閉じます。
4.  次のコマンドを使用して Postfix を再始動します。

  `/etc/init.d/postfix restart`

## トラブルシューティング

1.  「no mechanism available」のエラーが発生した場合は、認証/暗号化に必要なすべてのライブラリーがあることを確認します。 これらのライブラリーは、以下のコマンドでインストールできます。

  Debian/Ubuntu の場合:  `apt-get install libsasl2-modules`

  Redhat/CentOS の場合: `yum install cyrus-sasl-plain`

  これらのライブラリーをインストールしたら、以下の同じ restart コマンドを実行します。

    /etc/init.d/postfix restart

2.  ポート 587 でうまく動作しない場合は、Postfix 構成でポート 2525 を使用します。また、構成ファイル /etc/postfix/main.cf を開いて、以下の行のコメントを外す必要がある場合もあります。

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
