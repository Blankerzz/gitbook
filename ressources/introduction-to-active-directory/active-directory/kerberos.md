---
description: Kerberos Authentication Process
---

# Kerberos



| 1. The user logs on, and their password is converted to an NTLM hash, which is used to encrypt the TGT ticket. This decouples the user's credentials from requests to resources.                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2. The KDC service on the DC checks the authentication service request (AS-REQ), verifies the user information, and creates a Ticket Granting Ticket (TGT), which is delivered to the user.                             |
| 3. The user presents the TGT to the DC, requesting a Ticket Granting Service (TGS) ticket for a specific service. This is the TGS-REQ. If the TGT is successfully validated, its data is copied to create a TGS ticket. |
| 4. The TGS is encrypted with the NTLM password hash of the service or computer account in whose context the service instance is running and is delivered to the user in the TGS\_REP.                                   |
| 5. The user presents the TGS to the service, and if it is valid, the user is permitted to connect to the resource (AP\_REQ).                                                                                            |

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
