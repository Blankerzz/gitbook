# Active Directory

**History** :  Introduced  in RFCs in 1971, predated by the X.500 and created by Novell and Lotus. Released in 1993 as Novell Directory Services.

AD came on Windows Server 2000 and Windows NT 3.0.

AD : Distributed, hierarchical. &#x20;

**Management Centralisé des ressources d'une organisation  comprennant :**&#x20;

* Utilisateurs&#x20;
* PC
* Groups
* Network Devices&#x20;
* Files Shares&#x20;
* Group policies&#x20;
* Devices&#x20;
* Trust&#x20;

**Forest**  :  Allows sysadmins to create "containers" of serparate domaines, users, computers and other object all under the same umbrella. **Active Directory Federation Services** (ADFS) was introduced in Server 2008 to provide **Single Sign-On** (SSO). Tree are collectioctions of AD trees.

**Group Managed Service Accounts** (gMSA) :  Came with Server 2016,offers a more secure way to run specific automated tasks, applications and services. (mitigation against the infamous Kerberoasting attack).

**Active Directory Domain Services** (AD DS) : Ways to store Directory data and make it available to both standart users and administrators on the same network.&#x20;

**Domain** : Structure within which contaides objects ( users, compurters and groups) are accessible. it has many built-in **Organizational Units** (OUs), such as _Domain Controllers, Users, Computers_.New OUs can be created as required.&#x20;

```shell-session
INLANEFREIGHT.LOCAL/
├── ADMIN.INLANEFREIGHT.LOCAL
│   ├── GPOs
│   └── OU
│       └── EMPLOYEES
│           ├── COMPUTERS
│           │   └── FILE01
│           ├── GROUPS
│           │   └── HQ Staff
│           └── USERS
│               └── barbara.jones
├── CORP.INLANEFREIGHT.LOCAL
└── DEV.INLANEFREIGHT.LOCAL
```

**Object** : Any resource present within an Active Directory encironment such as Ous, printers, users, domain controllers, etc.

**Global Unique Identifier** (GUID) :  Unique 128-bit value assigned when a domain user or group is created. Every single object ceated by Active Directory is assigned a GUID.&#x20;

**Security principals** :  Anything that the operation system can autenticate, including users, computer, accounts, or even threads/processes that run in the context of a user or computer account.  In AD, security priciples are domain objects that can manage access to other resources within the domain.&#x20;

**Security identifier** (SID) :  Unique identifier for a security principal or security group. its issued by the domain controller and stored in a secure database. A SID can only be used once.&#x20;

**Distinguished Name** (DN) :  Describes the full path to an object in AD ( ex : cn = jzerbib, ou=INFRA, ou=Employé, dc=packsolutions, dc = local). Must be unique in the directory.&#x20;

**Relative Distinguished Name** (RDN) :  Single component of the DN that identifies the object as unique from other objects at the current level in the naming hierarchy.  Must be unique in an Organizational  Unit.

**sAMAccountName** : User's logon name. It must be a unique value and 20 or fewer characters.&#x20;

**userPrincipalName** :  Prefix (the user account name) and suffix (the domain name)  ex (bjones@inlanefreight.local). This attribute is not mandatory.&#x20;

**Flexible Single Master Operation** (FSMO)  :  Give Domain Controller (DC) the ability to continue authenticating users and granting permissions without interruption. There are five FMSO roles :  **Schema Master** and **Domain Naming Master** (one of each per forest), **Relative ID (RID) Master** ( one per Domain), **Primary Domain Controller (PDC) Emulator**  (one per Domain) and **Infrastructure Master** (one per domain).   All five roles are assigned to the first DC in the forest root domain in a new AD forest.&#x20;

**Global Catalog  :**  Domain controller that stores copies of ALL objects in an Active Directory forest.   full copy of all objects in the current domain and a partial copy of objects that belong to others forest. GC is a feature that is enablesd on a domain controller and performs  anthentication and object search.&#x20;

**Read-Only Domain Controller** (RODC)  :&#x20;

