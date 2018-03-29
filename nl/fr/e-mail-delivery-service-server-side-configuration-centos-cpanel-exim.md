---
copyright:
  years: 2014, 2018
lastupdated: "2018-03-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration de votre serveur pour l'utilisation du service de diffusion de courriers électroniques IBM Cloud : CentOS, cPanel et Exim

Utilisez ces informations pour configurer votre serveur pour l'utilisation du service de messagerie électronique {{site.data.keyword.cloud}}. 

## Préparation

1.  Confirmez que vous pouvez envoyer des courriers électroniques à partir de l'appareil avant d'ajouter ou de mettre à jour les paramètres de l'hôte actif. Corrigez tous les problèmes éventuels de processus d'envoi/réception avant de continuer.
2. Pour accéder à l'éditeur de configuration Exim, procédez comme suit :
  * Accédez à WHM en utilisant vos données d'identification uniques.
  * Accédez à **Service configuration > Exim Configuration Editor**.
  * Cliquez sur **Editeur avancé** pour ouvrir l'éditeur.
  
**Remarques :**
- Des instructions spécifiques pour l'utilisation de l'éditeur Advanced Editor se trouvent sur l'écran **Exim Configuration Editor**.
- Cette procédure peut entraîner l'échec d'Exim.
- L'écran **Exim Configuration Editor** affiche le contenu du fichier _exim.conf_. Vous pouvez éditer _exim.conf_ en utilisant Exim Configuration Manager.

## Authentification à l'aide des données d'identification SendGrid

Localisez la section **Begin Authenticators** et entrez les commandes suivantes dans la zone de texte correspondante intitulée **Section: AUTH**

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## Configuration des routeurs

Ajoutez les commandes suivantes dans la zone **Routers Configuration** à la section intitulée **Section: PREROUTERS:**
`send_via_sendgrid:`

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## Configuration des transports

Ajoutez les commandes suivantes dans la zone **Transports Configuration** à la section intitulée **Section: TRANSPORTSTART**

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

Cliquez sur **Save** au bas de la page.

<em>**Remarque :** Afin de recevoir le courrier électronique root/nobody/cpanel transféré à une adresse externe, le nom d'hôte des serveurs cPanel doit figurer dans le fichier /etc/localdomains.</em>

## Etapes suivantes

Le système exécute une série de vérifications par rapport au fichier de configuration mis à jour et redémarre Exim. Si vous êtes connecté à une page WebMail, déconnectez-vous puis reconnectez-vous après le redémarrage. Envoyez un courrier électronique de test pour vous assurer que les accréditations correctes sont utilisées depuis l'écran [Service de diffusion de courriers électroniques ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/services/emaildelivery){: new_window} dans le portail [{{site.data.keyword.slportal_full}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){: new_window}.
