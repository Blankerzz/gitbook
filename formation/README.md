# Information Gathering

## Active Information Gathering



DNSRecon :  [https://github.com/darkoperator/dnsrecon](https://github.com/darkoperator/dnsrecon)

```
dnsrecon -d megacorpone.com -t std
```

```
dnsrecon -d megacorpone.com -D ~/list.txt -t brt
```



Netcat Scan  TCP&#x20;

```
nc -nvv -w 1 -z 192.168.198.151 1-10000 2>&1 | grep -v "Connection refused"

```



Windows port scan&#x20;

```
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null
```



SMB OS discovery

```
nmap -v -p 139,445 --script smb-os-discovery 192.168.50.152
```



SMB discovery

```
enum4linux -a 192.168.224.13
```



Windows SMB discovery&#x20;

```
net view \\dc01 /all
```



SMTP enumeration

```
nc -nv 192.168.224.8 25
```

```
#!/usr/bin/python

import socket
import sys

if len(sys.argv) != 3:
        print("Usage: vrfy.py <username> <target_ip>")
        sys.exit(0)

# Create a Socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connect to the Server
ip = sys.argv[2]
connect = s.connect((ip,25))

# Receive the banner
banner = s.recv(1024)

print(banner)

# VRFY a user
user = (sys.argv[1]).encode()
s.send(b'VRFY ' + user + b'\r\n')
result = s.recv(1024)

print(result)

# Close the socket
s.close()
```

```
python3 smtp.py root 192.168.50.8
```



SNMP discovery



Windows SNMP MIB values

| 1.3.6.1.2.1.25.1.6.0   | System Processes |
| ---------------------- | ---------------- |
| 1.3.6.1.2.1.25.4.2.1.2 | Running Programs |
| 1.3.6.1.2.1.25.4.2.1.4 | Processes Path   |
| 1.3.6.1.2.1.25.2.3.1.4 | Storage Units    |
| 1.3.6.1.2.1.25.6.3.1.2 | Software Name    |
| 1.3.6.1.4.1.77.1.2.25  | User Accounts    |
| 1.3.6.1.2.1.6.13.1.3   | TCP Local Ports  |

```
sudo nmap -sU --open -p 161 192.168.50.1-254 -oG open-snmp.txt
```

```
for ip in $(seq 1 254); do echo 192.168.50.$ip; done > ips
onesixtyone -c community -i ips
```

```
snmpwalk -c public -v1 192.168.50.151 1.3.6.1.4.1.77.1.2.25
```

```
snmpwalk -c public -v1 -t 10 192.168.50.151
```

