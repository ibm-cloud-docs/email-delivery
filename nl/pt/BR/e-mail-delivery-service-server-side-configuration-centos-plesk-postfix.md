---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuração do lado do servidor do serviço de entrega de e-mail: CentOS, Plesk e Postfix

Siga estas etapas para configurar o servidor para usar o {{site.data.keyword.SendGrid}}, o serviço de entrega de e-mail do {{site.data.keyword.cloud}}, como um host inteligente. O exemplo abaixo foi executado com um Recarregamento de S.O. padrão
do {{site.data.keyword.cloud}} do CentOS 6.5 com Plesk 12 e Postfix.

## Configuração

1.  Localize seu arquivo de configuração do Postfix. Geralmente ele está localizado aqui:
/etc/postfix/main.cf.
2.  Abra o arquivo main.cf com um editor de texto e inclua o seguinte na configuração.

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  Salve e feche o arquivo /etc/postfix/main.cf.
4.  Reinicie o Postfix usando este comando:

  `/etc/init.d/postfix restart`

## Resolução de problemas

1.  Se receber um erro "Nenhum mecanismo disponível", verifique se você possui todas as
bibliotecas necessárias para autenticação/criptografia. É possível instalar essas bibliotecas usando os
comandos a seguir:

  Para Debian/Ubuntu: `apt-get install libsasl2-modules`

  Para Redhat/CentOS: `yum install cyrus-sasl-plain`

  Após instalar essas bibliotecas, emita o mesmo comando de reinicialização:

    /etc/init.d/postfix restart

2.  Se a porta 587 não funcionar, use a porta 2525 na configuração do Postfix. Também pode ser necessário abrir o arquivo de configuração /etc/postfix/main.cf e remover o comentário da linha a seguir:

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
