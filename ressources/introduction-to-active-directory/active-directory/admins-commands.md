# Admins Commands

**Create New User :**&#x20;

```powershell
New-ADUser -Name "John Smith" -GivenName "John" -Surname "Smith" -UserPrincipalName "j.smith@inlanefreight.local" -SamAccountName "jsmith" -DisplayName "John Smith" -AccountPassword (ConvertTo-SecureString "Password123" -AsPlainText -Force) -ChangePasswordAtLogon $true
```

```powershell
New-ADUser -Name "Orion Starchaser" -Accountpassword (ConvertTo-SecureString -AsPlainText (Read-Host "Enter a secure password") -Force ) -Enabled $true -OtherAttributes @{'title'="Analyst";'mail'="o.starchaser@inlanefreight.local"}
```

**Remove User :**&#x20;

```powershell
Remove-ADUser -Identity pvalencia
```

**Unlock User :**&#x20;

```powershell
Unlock-ADAccount -Identity amasters 
```

**Reset User Password (Set-ADAccountPassword) :**

```powershell
Set-ADAccountPassword -Identity 'amasters' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "NewP@ssw0rdReset!" -Force)
```

**Force Password Change (Set-ADUser) :**

```powershell
Set-ADUser -Identity amasters -ChangePasswordAtLogon $true
```

**Create a New AD OU :**

```powershell
New-ADOrganizationalUnit -Name "Security Analysts" -Path "OU=IT,OU=HQ-NYC,OU=Employees,OU=CORP,DC=INLANEFREIGHT,DC=LOCAL"
```

**Create a New Group :**

```powershell
New-ADGroup -Name "Security Analysts" -SamAccountName analysts -GroupCategory Security -GroupScope Global -DisplayName "Security Analysts" -Path "OU=Security Analysts,OU=IT,OU=HQ-NYC,OU=Employees,OU=Corp,DC=INLANEFREIGHT,DC=LOCAL" -Description "Members of this group are Security Analysts under the IT OU"
```

**Add User to Group :**

```powershell
Add-ADGroupMember -Identity analysts -Members ACepheus,OStarchaser,ACallisto
```

**Duplicate the Object :**

```powershell
Copy-GPO -SourceName "Logon Banner" -TargetName "Security Analysts Control"
```

**Link the New GPO to an OU  :**

```powershell
New-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes
```

