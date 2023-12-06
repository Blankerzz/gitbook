# Identification des Vuln

```
root@kali:/home/clehen38# nmap --script=vuln 192.168.10.34,184
Starting Nmap 7.91 ( https://nmap.org ) at 2023-09-13 09:00 UTC
Nmap scan report for 192.168.10.34
Host is up (0.00054s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
21/tcp open  ftp
| ftp-vsftpd-backdoor: 
|   VULNERABLE:
|   vsFTPd version 2.3.4 backdoor
|     State: VULNERABLE (Exploitable)
|     IDs:  CVE:CVE-2011-2523  BID:48539
|       vsFTPd version 2.3.4 backdoor, this was reported on 2011-07-04.
|     Disclosure date: 2011-07-03
|     Exploit results:
|       Shell command: id
|       Results: uid=1000(bthomson) gid=1000(bthomson) groups=1000(bthomson),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lpadmin),111(sambashare)
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2523
|       https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/unix/ftp/vsftpd_234_backdoor.rb
|       https://www.securityfocus.com/bid/48539
|_      http://scarybeastsecurity.blogspot.com/2011/07/alert-vsftpd-download-backdoored.html
|_sslv2-drown: 
22/tcp open  ssh
MAC Address: 02:4B:3A:77:7A:A4 (Unknown)

Nmap scan report for 192.168.10.184
Host is up (0.00031s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE
21/tcp open  ftp
|_sslv2-drown: 
22/tcp open  ssh
80/tcp open  http
| http-csrf: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=192.168.10.184
|   Found the following possible CSRF vulnerabilities: 
|     
|     Path: http://192.168.10.184:80/
|     Form id: ajax-form
|     Form action: #
|     
|     Path: http://192.168.10.184:80/services.htm
|     Form id: ajax-form
|     Form action: #
|     
|     Path: http://192.168.10.184:80/index.htm
|     Form id: ajax-form
|     Form action: #
|     
|     Path: http://192.168.10.184:80/about-us.htm
|     Form id: ajax-form
|_    Form action: #
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|   /private/sdc.tgz: IBM Bladecenter Management Logs (401 Unauthorized)
|   /css/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
|   /img/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
|   /js/: Potentially interesting directory w/ listing on 'apache/2.4.29 (ubuntu)'
|_  /private/: Potentially interesting folder (401 Unauthorized)
| http-sql-injection: 
|   Possible sqli for queries:
|     http://192.168.10.184:80/js/?C=S%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.184:80/js/?C=M%3bO%3dA%27%20OR%20sqlspider
|     http://192.168.10.184:80/js/?C=D%3bO%3dA%27%20OR%20sqlspider
|_    http://192.168.10.184:80/js/?C=N%3bO%3dD%27%20OR%20sqlspider
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
MAC Address: 02:D4:AD:A4:81:62 (Unknown)

Nmap done: 2 IP addresses (2 hosts up) scanned in 31.35 seconds
root@kali:/home/clehen38# 

```
