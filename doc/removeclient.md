# Procédure de suppression d'un client 

Naviguez dans le dossier EasyRSA 
```
$ cd ~/EasyRSA-3.0.4/
```

Lancez le script  `easyrsa` avec l'option `revoke` suivie par le nom du client à supprimer :
```
$ ./easyrsa revoke client2
```
Vous devrez valider en écrivant  `yes` :
```
Output

Please confirm you wish to revoke the certificate with the following subject: 

subject= 
commonName = client2 


Type the word 'yes' to continue, or any other input to abort. 
Continue with revocation: yes
```
Après avoir confirmer le certificat du client va être supprimé et ne pourra plus être réutilisé mais le client pourra toujours accéder au VPN il va donc falloir créer un certificat pour révoquer l'accès :
```
$ ./easyrsa gen-crl
```
Cette commande va générer le fichier `crl.pem` et il va falloir le transférer sur notre serveur du VPN :

`$ scp ~/EasyRSA-3.0.4/pki/crl.pem sammy@your_server_ip:/tmp`

Sur le serveur du VPN copiez ce fichier dans ``/etc/openvpn/`` :

`$ sudo cp /tmp/crl.pem /etc/openvpn`

Ensuite, ouvrez la configuration du serveur OpenVpn  :

`sudo nano /etc/openvpn/server.conf`

Tout en haut de la configuration ajoutez `crl-verify crl.pem` ce qui donnera l'instruction au serveur de vérifier la révocation de certificat à chaque connexion.

Sauvegardez et fermez le fichier de configuration.

Pour finir, relancez OpenVpn pour prendre en compte vos modifications :
`$ sudo systemctl restart openvpn@server`

**  Félicitations vous venez de supprimer un client **


