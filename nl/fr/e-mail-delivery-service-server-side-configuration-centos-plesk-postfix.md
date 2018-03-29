---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration du service de diffusion de courriers électroniques côté serveur : CentOS, Plesk et Postfix

Pour configurer votre serveur pour l'utilisation de {{site.data.keyword.SendGrid}}, le service de diffusion de courriers électroniques {{site.data.keyword.cloud}}, comme hôte actif, procédez comme comme indiqué ci-après. L'exemple ci-dessous a été réalisé avec un rechargement standard de système d'exploitation {{site.data.keyword.cloud}} de CentOS 6.5 avec Plesk 12 et Postfix.

## Configuration

1.  Localisez le fichier de configuration Postfix. Il se trouve souvent à cet emplacement : /etc/postfix/main.cf.
2.  Ouvrez le fichier main.cf dans un éditeur de texte et ajoutez les lignes suivantes dans la configuration.

  `smtp_sasl_auth_enable = yes`

  `smtp_sasl_password_maps = static:_Your SendGrid Username_:_Your SendGrid Password_`

  `smtp_sasl_security_options = noanonymous`

  `smtp_tls_security_level = encrypt`

  `header_size_limit = 4096000`

  `relayhost = [smtp.sendgrid.net]:587`

3.  Sauvegardez et fermez le fichier /etc/postfix/main.cf.
4.  Redémarrez Postfix avec la commande suivante :

  `/etc/init.d/postfix restart`

## Traitement des incidents

1.  Si vous obtenez l'erreur "no mechanism available" (aucun mécanisme disponible), vérifiez que vous disposez de toutes les bibliothèques nécessaires pour l'authentification et le chiffrement. Vous pouvez installer ces bibliothèques à l'aide des commandes suivantes :

  Pour Debian/Ubuntu :  `apt-get install libsasl2-modules`

  Pour Redhat/CentOS : `yum install cyrus-sasl-plain`

  Après avoir installé ces bibliothèques, relancez la même commande restart :

    /etc/init.d/postfix restart

2.  Si le port 587 ne fonctionne pas, utilisez le port 2525 dans la configuration Postfix. Il vous faudra peut-être également ouvrir le fichier de configuration /etc/postfix/main.cf et supprimer la mise en commentaire de la ligne suivante :

  `#tlsmgr unix - - n 1000? 1 tlsmgr`
