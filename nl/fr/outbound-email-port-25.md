---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Courrier sortant sur le port 25

Depuis le 28 octobre 2015, {{site.data.keyword.BluSoftlayer_notm}} ne permet plus les connexions sortantes via le port TCP 25 (SMTP) pour les nouveaux comptes.

## Pourquoi bloquer un port de messagerie standard ?

Par défaut, le port TCP SMTP 25 standard est bloqué en raison d'un grand nombre d'abus dont ce port est la cible. {{site.data.keyword.BluSoftlayer_notm}} offre un service de relais de messagerie tiers depuis SendGrid si vous devez envoyer du courrier sortant à partir de ses domaines ou de ses applications.  

## Quelles sont les options à ma disposition pour envoyer des messages à partir de mon serveur ou de mon application ?

Si vous voulez envoyer des messages à partir de vos serveurs, vous devez utiliser un hôte actif localisé en dehors de {{site.data.keyword.BluSoftlayer_notm}}. Un hôte actif est un hôte qui transmet le trafic SMTP à partir d'un serveur SMTP, d'un client de messagerie ou de tout autre service ou langage de programmation compatible avec SMTP. En principe, les serveurs envoient ce type de trafic en utilisant les ports TCP 465 ou 587 utilisés pour l'envoi de courrier électronique.  Vous pouvez communiquer via ces ports ou avec un port personnalisé différent du port TCP 25. Pour utiliser votre propre serveur de messagerie sur un port personnalisé, consultez la documentation de votre service de messagerie relative à la configuration d'un port de messagerie personnalisé.

## IBM Cloud propose-t-il un service d'hôte actif ?

{{site.data.keyword.BluSoftlayer_notm}} offre désormais un service de diffusion de courriers électroniques basé sur SendGrid qui permet aux clients d'utiliser un hôte actif pour relayer vos services de courrier sortant. Ce service dispose de nombreuses autres fonctions, par exemple la génération de métriques, le suivi des listes d'adresses électroniques et des activités de courrier électronique, ainsi qu'une assistance pour la diffusion de newsletters et l'authentification.
