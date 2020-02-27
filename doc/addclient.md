# Procédure d'ajout d'un nouveau client  

Naviguez dans le dossier EasyRSA et exécutez le script `easyrsa` avec les options `gen-req`, `nopass` et du nom désiré pour le client :
```
$ cd ~/EasyRSA-3.0.4/
$ ./easyrsa gen-req [nomDuClient] nopass
```

Appuyez sur `Entrée` pour confirmer le nom du client puis copiez le fichier `[nomDuClient].key` dans le dossier `/client-configs/keys/`:
```
$ cp pki/private/[nomDuClient].key ~/client-configs/keys/
```

Ensuite, transférez le fichier `[nomDuClient].req` sur le CA en utilisant la méthode sécurisée suivante:
```
$ scp pki/reqs/[nomDuClient].req [yourUser]@your_CA_ip:/tmp
```

<hr>

Connectez-vous sur votre CA, allez dans le dossier EasyRSA et importez le certificat de requête:
```
$ cd EasyRSA-3.0.4/
$ ./easyrsa import-req /tmp/[nomDuClient].req [nomDuClient]
```

Signez ensuite la requête avec la clé privée du CA, spécifiez le type de requête `client`:
```
$ ./easyrsa sign-req client [nomDuClient]
```

Entrez sur `yes` pour confirmer la signature:
```
Type the word 'yes' to continue, or any other input to abort.
  Confirm request details: yes
```

Vous venez de créer le certificat `[nomDuClient].crt`. 
Transférez ce fichier sur le serveur VPN:
```
$ scp pki/issued/[nomDuClient].crt [yourUser]@your_server_ip:/tmp
```

<hr>

Retournez sur la console de votre serveur VPN et copiez le certificat du client vers le répertoire `/client-configs/keys/` : 
```
$ cp /tmp/[nomDuClient].crt ~/client-configs/keys/
```

Enfin, copiez les fichiers `ca.crt` et `ta.key` dans le répertoire `/client-configs/keys/` comme suivant:
```
$ cp ~/EasyRSA-3.0.4/ta.key ~/client-configs/keys/
$ sudo cp /etc/openvpn/ca.crt ~/client-configs/keys/
```
