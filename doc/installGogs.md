# Installation du serveur Go Git Server   

## Prérequis

**Windows 10 :**
- Assurez vous de posséder Wind

**WAMP :** 
- Téléchargez WampServer http://www.wampserver.com/en/download-wampserver-64bits/ 
- Lancez Wamp une fois installé et rendez vous sur votre panel PHP My Admin : http://localhost/phpmyadmin/
- Connectez vous avec le nom d'utilisateur `root` en laissant le champ de mot de passe vide et laissant le serveur par défaut soir MySql.
- Créez une nouvelle table nommée `gogs` en `utf8_general_ci`.

**Git :**
- Téléchargez simplement Git https://git-scm.com/download/win
- Télécharger sur Linux : `sudo apt-get install git`
- Télécharger sur Mac OS X : `brew install git`

**SSH :**
- Pour pouvoir se connecter en SSH au gogs du serveur le client devra posséder un serveur SSH.

**Gogs :**
- Téléchargez le dernière version de Gogs : https://dl.gogs.io/
- Décompressez la dans un dossier
- Accèder au dossier depuis un invité de commande avec `cd chemindudossier`
- Lancez gogs avec `./gogs web`
- Rendez vous sur l'adresse local `http://localhost:3000`
- Créez un compte administrateur puis cliquez sur suivant.
- Le serveur Gogs est prêt !



