---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration du service de diffusion de courriers électroniques côté serveur : MailEnable/IIS et SendGrid

Pour configurer votre serveur pour l'utilisation du service de diffusion de courriers électroniques {{site.data.keyword.cloud}} en tant qu'hôte actif, procédez comme comme indiqué ci-après. Les exemples ci-dessous concernent Windows Server 2008 ou 2012 avec MailEnable ou IIS configurés comme service SMTP.

## Configuration IIS

1.  Ouvrez le Gestionnaire des services IIS dans Windows.
2.  Cliquez sur votre site. La page des options de configuration principales s'affiche à droite.
3.  Cliquez deux fois sur l'icône **Courrier électronique SMTP**.
4.  Dans la zone d'adresse e-mail, indiquez l'adresse e-mail correspondant à l'expéditeur.
5.  Cliquez sur le bouton d'option **Remettre les messages électroniques au serveur SMTP**.
6.  Dans la zone **Serveur SMTP**, entrez : smtp.sendgrid.net.
7.  Dans la zone **Port**, entrez : 587
8.  Sous **Paramètres d'authentification**, sélectionnez **Spécifier les informations d'identification**, puis cliquez sur **Définir**.
9.  Ajoutez vos nom d'utilisateur et mot de passe {{site.data.keyword.SendGrid}}, puis cliquez sur **Sauvegarder**.

## MailEnable

1.  Ouvrez l'application MailEnableAdmin.
2.  Développez l'onglet **Servers** dans le panneau de navigation situé à gauche.
3.  Cliquez sur localhost > System > puis cliquez avec le bouton droit de la souris sur SMTP.
4.  Dans la zone **SMTP Properties**, cliquez sur **Smart Host**.
5.  Cochez la case **Smart Host Enabled**.
6.  Sous **IP/Domain**, entrez : smtp.sendgrid.net. 
7.  Dans la zone **Port**, entrez : 587
8.  Cochez la case "The remote server requires authentication".
9.  Ajoutez vos nom d'utilisateur et mot de passe {{site.data.keyword.SendGrid}}, puis cliquez sur **Apply**.
10.  Accédez aux **services Windows** et redémarrez MailEnable.
