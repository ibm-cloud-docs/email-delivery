---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# E-mail de saída na porta 25

A partir de 28 de outubro de 2015, o {{site.data.keyword.BluSoftlayer_notm}} não permite mais
conexões de saída por meio da porta TCP 25 (SMTP) em novas contas.

## Por que uma porta de e-mail padrão é bloqueada?

Por padrão, a porta TCP SMTP 25 padrão é bloqueada por conta da grande quantia de abuso que é destinada a
essa porta. O {{site.data.keyword.BluSoftlayer_notm}} oferece um serviço confiável de retransmissão de e-mail de terceiros do SendGrid quando é necessário enviar e-mail de saída dos seus domínios ou aplicativos.  

## Quais opções eu terei se quiser enviar e-mail do meu servidor ou aplicativo?

Se você precisar enviar um e-mail de seus servidores, será necessário usar um host inteligente fora do {{site.data.keyword.BluSoftlayer_notm}}. Um host inteligente é um host que retransmite o tráfego SMTP de um servidor SMTP, cliente de correio ou qualquer outro serviço ou linguagem de programação capaz de manipular SMTP. Os servidores geralmente enviam esse tipo de tráfego usando as portas TCP 465
ou 587 de envio de e-mail.  É possível comunicar-se com essas ou com qualquer outra porta customizada diferente da
porta TCP 25. Se você deseja usar seu próprio servidor de e-mail em uma porta customizada, use a documentação
específica para seu serviço de e-mail para configurar uma porta de e-mail customizada.

## O IBM Cloud oferece um serviço de host inteligente?

O {{site.data.keyword.BluSoftlayer_notm}} agora oferece um serviço de entrega de e-mail
desenvolvido pela SendGrid que permite que os clientes usem um host inteligente para retransmitir seus
serviços de e-mail de saída. Esse serviço possui muitas outras funções, como geração de métricas, rastreio
de listas de e-mail, rastreio de atividade de e-mail, ajuda com newsletters e autenticação.
