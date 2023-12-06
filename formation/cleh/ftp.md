# FTP

```
On retourne sur la .34 et on cherche dans l'historique :
root@Invictus-Bank:/home/olivier# history | grep ftp | grep 192.168
  864  ftp 192.168.168.10.54 bthomson@BtH0mS0n
  865  ftp 192.168.168.10.184 bthomson@BtH0mS0n
  866  ftp 192.168.10.184 bthomson@BtH0mS0n
  867  ftp 192.168.10.184  bthomson@BtH0mS0n
  868  ftp 192.168.10.184 21
 1404  ftp 192.168.168.54 bthomson@password
 1405  ftp 192.168.10.54 bthomson@password
 1406  ftp 192.168.168.10.184 bthomson@password
 1407  ftp 192.168.10.184 bthomson@password
 1412  history | grep ftp | grep 192.168


On identifie des tentatives de connexions ftp, avec un login bthomson et un mot de passe “BtH0mS0n” ou “password”.
On essaye les deux sur le serveur FTP :
┌──(olivier㉿kali)-[~]
└─$ ftp 192.168.10.184
Connected to 192.168.10.184.
220 ProFTPD 1.3.5e Server (Debian) [::ffff:192.168.10.184]
Name (192.168.10.184:olivier): bthomson
331 Password required for bthomson
Password:
230 User bthomson logged in
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 

Nous sommes maintenant connectés et pouvons entrer des commandes FTP (lister les fichiers, se déplacer dans l'arborescence, télécharger des fichiers)
ftp> dir
200 PORT command successful
150 Opening ASCII mode data connection for file list
drwxrwxr-x   2 bthomson bthomson     4096 Nov  5  2019 Documents
drwxrwxr-x   2 bthomson bthomson     4096 Nov  5  2019 Downloads
drwxrwxr-x   3 bthomson bthomson     4096 Nov  5  2019 Pictures
226 Transfer complete

On ne trouve rien d'intéressant, mais en cherchant dans les fichiers cachés, on finit par trouver quelque chose :
ftp> cd Pictures/
250 CWD command successful
ftp> ls -la
200 PORT command successful
150 Opening ASCII mode data connection for file list
drwxrwxr-x   3 bthomson bthomson     4096 Nov  5  2019 .
drwxr-xr-x   9 bthomson bthomson     4096 Sep 14 20:12 ..
drwxrwxr-x   2 bthomson bthomson     4096 Dec 14  2020 .backup
226 Transfer complete
ftp> 

Dans ce dossier, il y a plein de fichier que nous allons télécharger pour les ouvrir en local sur la machine Kali :
ftp> mget *
mget office-1571931__480.jpg? 
200 PORT command successful
150 Opening BINARY mode data connection for office-1571931__480.jpg (68234 bytes)
226 Transfer complete
68234 bytes received in 0.00 secs (252.2210 MB/s)
mget Image.jpeg? 
...
..
.

On ouvre les images une à une pour finir par trouver quelque chose d'intéressant :



En zoomant sur le post-it, on peut lire :
	SSH 192.168.168.97
	blythe
	EblytheBB2017

Attention l'adresse IP n'est pas la bonne.
Mais on peut tout de même noté qu'il s'agit d'une connexion sur une machine dans le réseau 192.168.168.0/24 en SSH.
Nous allons donc tester la connexion avec ce compte.




```
