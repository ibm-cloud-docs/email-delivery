---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration du service de diffusion de courriers électroniques côté serveur : Sendmail et SendGrid

Pour configurer votre serveur pour l'utilisation du service de diffusion de courriers électroniques {{site.data.keyword.cloud}} avec Sendmail, procédez comme comme indiqué ci-après. L'exemple ci-dessous a été réalisé sur une installation bare metal de Centos 6.5 et Ubuntu 14 sur un serveur bare metal.

## Configuration préalable

Vous devez installer les packages suivants pour que Sendmail utilise correctement {{site.data.keyword.SendGrid}} en tant qu'hôte actif.

### RHEL/Centos
Pour RHEL/Centos, exécutez cette commande :
`yum install cyrus-sasl-plain sendmail sendmail-cf`

### Ubuntu/Debian
Pour Ubuntu/Debian, exécutez cette commande :
`apt-get install libsasl2-modules sendmail sendmail-cf heirloom-mailx`

## Configuration

1. Ajoutez votre nom d'utilisateur (YOUR_SENDGRID_USER) et votre mot de passe (YOUR_SENDGRID_PASSWORD) {{site.data.keyword.SendGrid}} dans le fichier /etc/mail/access :
`AuthInfo:smtp.sendgrid.net "U:YOUR_SENDGRID_USER" "P:YOUR_SENDGRID_PASSWORD" "M:PLAIN"`
2. Exécutez la commande suivante pour générer la mappe de base de données /etc/mail/access.db :
`makemap hash /etc/mail/access.db < /etc/mail/access`
3. Editez le fichier /etc/mail/sendmail.mc pour utiliser {{site.data.keyword.SendGrid}} comme hôte actif.

### Configurez sendmail.mc dans RHEL/Centos
1. Localisez et ouvrez le fichier sendmail.mc.
2. Mettez en commentaire la ligne suivante :
`dnl define('SMART_HOST', 'smtp.your.provider')dnl`
3. Ajoutez des nouvelles lignes avec le code suivant :
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Configurez sendmail.mc dans Ubuntu/Debian
1. Localisez et ouvrez le fichier sendmail.mc.
2. A la fin du fichier, placez le code suivant au-dessus de la ligne contenant 'MAILER_DEFINITIONS'
`define('SMART_HOST', 'smtp.sendgrid.net')dnl`
`FEATURE('access_db')dnl`
`define('RELAY_MAILER_ARGS', 'TCP $h 587')dnl`
`define('ESMTP_MAILER_ARGS', 'TCP $h 587')dnl`

### Générez à nouveau le fichier sendmail.cf
Le fichier sendmail.mc est une collection de macros pouvant être développée dans le fichier de configuration sendmail.cf réel (et plus complexe). Pour que vos modifications accessibles à Sendmail, générez à nouveau le fichier sendmail.cf avec la commande m4 :
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

## Redémarrage de Sendmail
Redémarrez Sendmail avec la commande suivante :
`service sendmail restart`

## Test du résultat à l'aide de l'utilitaire mail sur la ligne de commande
Testez les modifications en utilisant la commande suivante :
`echo "Sendgrid and Sendmail" | mail -s "mail subject here" you@yourdomain.com`
