---
description: Linux | easy | RCE bypass | sqlite3
---

# Perfection

ip : 10.129.6.30

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<%= File.open('/etc/passwd').read %>

on encode les caractere speciaux en URL&#x20;

%0A<%25%3d+File.open('/etc/passwd').read+%25>&

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

when we try to sudo -l we can see that we need the password in order to see our permissions.

then we found in the migration folder a sqlite3 database  lets check it&#x20;

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

we found some hashes lets try to find our password !&#x20;

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

abeb6f8eb5722b8ca3b45f6f72a0cf17c7028d62a15a30199347d9d74f39023f

cant crack it using hashcat



we found an instersting file in /var/mail/

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

so we have now the structure of the password lets try again with hashcat&#x20;

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

susan got all rights on the machine lets just cat the root flag with the sudo command.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
