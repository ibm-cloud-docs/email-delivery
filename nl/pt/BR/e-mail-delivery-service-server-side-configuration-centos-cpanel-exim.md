---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurando seu servidor para usar o serviço de entrega de e-mail do IBM Cloud: CentOS, cPanel e Exim

## Visão geral

Use estas informações para configurar seu servidor para usar o serviço de e-mail do {{site.data.keyword.cloud}}. 

## Preparação

1.  Confirme que é possível enviar e-mails por meio do dispositivo antes de incluir ou de atualizar as configurações do host inteligente. Corrija quaisquer problemas existentes no processo de envio/recebimento antes de continuar.
2. Execute estas etapas para acessar o Editor de configuração do Exim:
  * Acesse o WHM usando suas credenciais exclusivas.
  * Navegue para **Configuração de serviço > Editor de configuração do Exim**.
  * Clique no botão **Editor Avançado** na parte inferior da tela para abrir o editor.
  
**Notas:**
- Instruções específicas para uso do Editor Avançado estão localizadas na tela **Editor de configuração do Exim**.
- Este procedimento pode fazer com que o Exim falhe.
- A tela **Editor de configuração do Exim** exibe o conteúdo do arquivo
_exim.conf_. É possível editar o _exim.conf_ usando o Gerenciador de configuração do Exim.

## Autenticar usando credenciais do SendGrid

Localize a seção **Iniciar autenticadores** e insira os comandos a seguir na caixa de texto correspondente rotulada **Seção: AUTH**

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## Configure os roteadores

Inclua os comandos a seguir em **Configuração de roteadores** na seção rotulada **Seção: PREROUTERS:**
`send_via_sendgrid:`

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## Configure os transportes

Inclua os comandos a seguir em **Configuração de transportes** na seção rotulada **Seção: TRANSPORTSTART**

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

Clique em **Salvar** na parte inferior da página.

<em>**Nota:** para receber o e-mail root/nobody/cpanel encaminhado para o endereço externo, o nome do host dos servidores cPanel precisa estar no arquivo /etc/localdomains.</em>

## O que acontece em seguida

O sistema executa uma série de verificações com relação ao arquivo de configuração atualizado e reinicia o Exim. Se você estiver com login efetuado em quaisquer páginas do WebMail, efetue logout e login novamente após a reinicialização ser concluída. Envie um e-mail de teste para assegurar-se de que os créditos apropriados estão sendo usados na tela [Serviço de entrega de e-mail ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/services/emaildelivery){: new_window} no [{{site.data.keyword.slportal_full}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window}.
