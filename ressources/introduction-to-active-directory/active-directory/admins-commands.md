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
