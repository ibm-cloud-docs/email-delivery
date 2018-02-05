---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuração do lado do servidor do serviço de entrega de e-mail: MailEnable/IIS e SendGrid

## Visão geral

Use este procedimento para configurar seu servidor para usar o serviço de entrega de e-mail do
{{site.data.keyword.cloud}} como um host inteligente. Os exemplos a seguir são para um servidor Windows
2008 ou 2012 padrão com o MailEnable ou IIS configurados como seu serviço SMTP.

## Configuração do IIS

1.  Abra o IIS Manager no Windows.
2.  Clique em seu site. A página de opções de configuração principal é exibida à direita.
3.  Dê um clique duplo no ícone E-mail SMTP.
4.  No campo de endereço de e-mail, digite o endereço de e-mail que será o remetente.
5.  Clique no botão de opções Entregar e-mail ao servidor SMTP.
6.  No campo Servidor SMTP, digite: smtp.sendgrid.net.
7.  No campo Porta, digite: 587
8.  Em Configurações de autenticação, escolha Especificar credenciais e clique em Configurar.
9.  Inclua seu nome de usuário e senha do {{site.data.keyword.SendGrid}} e clique em Salvar.

## MailEnable

1.  Abra o aplicativo MailEnableAdmin.
2.  Expanda a guia Servidores na área de janela de navegação à esquerda.
3.  Clique em Host local > Sistema > Clique com o botão direito em SMTP
4.  Na caixa Propriedades do SMTP, clique na guia Host inteligente.
5.  Ative a caixa próxima a Host inteligente ativado.
6.  Em IP/Domínio, digite: smtp.sendgrid.net. 
7.  No campo Porta, digite: 587
8.  Selecione a caixa que diz 'O servidor remoto requer autenticação'
9.  Insira seu nome do usuário e senha do {{site.data.keyword.SendGrid}} e clique em Aplicar.
10.  Acesse Serviços do Windows e reinicie o MailEnable.
