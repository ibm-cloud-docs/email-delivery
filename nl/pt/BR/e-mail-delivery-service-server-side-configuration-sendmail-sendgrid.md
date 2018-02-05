---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuração do lado do servidor do serviço de entrega de e-mail: Sendmail e SendGrid

## Visão geral

Use este procedimento para configurar seu servidor para usar o serviço
de entrega de e-mail do {{site.data.keyword.cloud}} com Sendmail. O exemplo abaixo foi executado em
uma instalação simples do Centos 6.5 e do Ubuntu 14.

## Pré-configuração

Será necessário instalar os pacotes a seguir para Sendmail para usar corretamente o
{{site.data.keyword.SendGrid}} como um host inteligente.

### RHEL/Centos
Para RHEL/Centos, execute este comando: `yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
Para Ubuntu/Debian, execute este comando:
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Configuração

1. Inclua seu nome de usuário e senha do {{site.data.keyword.SendGrid}} no arquivo
/etc/mail/access: `AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD"
"M:PLAIN"`
2. Execute o comando a seguir para gerar o mapa de banco de dados /etc/mail/access.db: `makemap
hash /etc/mail/access.db < /etc/mail/access`
3. Edite o arquivo /etc/mail/sendmail.mc para usar o {{site.data.keyword.SendGrid}} como o nosso
host inteligente.

### Configure o sendmail.mc no RHEL/Centos
1. Localize e abra o arquivo sendmail.mc.
2. Comente a linha a seguir:
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. Também no arquivo sendmail.mc, inclua novas linhas com o código a seguir:
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Configure o sendmail.mc no Ubuntu/Debian
1. Localize e abra o arquivo sendmail.mc.
2. Na parte inferior do arquivo, coloque o código a seguir na linha que lê 'MAILER_DEFINITIONS'
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Gere novamente o sendmail.cf
O arquivo sendmail.mc é uma coleção de macros que podem ser expandidas para o arquivo de configuração
sendmail.cf real (e mais complexo). Para tornar suas mudanças acessíveis para o sendmail, gere novamente
o sendmail.cf usando o comando m4: `m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Reinicie o Sendmail
Reinicie o Sendmail usando o comando a seguir: `service sendmail restart`

## Teste usando o utilitário de e-mail da linha de comandos
Teste as mudanças usando o comando a seguir: `echo "Sendgrid and Sendmail" | mail -s "mail
subject here" you@yourdomain.com`
