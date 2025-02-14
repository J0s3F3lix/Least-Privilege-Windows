### Configuración para la protección de Seguridad para WorkShops 'Atacando & Defendiendo Windows Active Directory'
### Basado en CIS Benchmark con amor NickGitHub: J0s3F3lix

1. **SMB Security Hardening**

   - **Disable SMBv1:**
     - `Computer Configuration -> Policies -> Administrative Templates -> Network -> Lanman Server -> Enable SMB1 Protocol: Disabled`
   
   - **Disable Anonymous Access to SMB:**
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Network access: Shares that can be accessed anonymously: (None)`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Network access: Do not allow anonymous enumeration of SAM accounts: Enabled`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Network access: Do not allow anonymous enumeration of SAM accounts and shares: Enabled`
   
   - **Enable SMB Signing:**
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Microsoft network server: Digitally sign communications (always): Enabled`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Microsoft network client: Digitally sign communications (always): Enabled`

2. **Name Resolution Hardening**

   - **Disable LLMNR & NBT-NS:**
     - `Computer Configuration -> Policies -> Administrative Templates -> Network -> DNS Client -> Turn off smart multi-homed name resolution: Enabled`
     - `Computer Configuration -> Policies -> Administrative Templates -> Network -> DNS Client -> Turn off multicast name resolution: Enabled`

3. **NTLM Relay Protection**

   - **Restrict NTLM Usage:**
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Network security: Restrict NTLM: NTLM authentication in this domain: Deny all`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Network security: LDAP client signing requirements: Require signing`

4. **LDAP Security Hardening**

   - **Enforce LDAP Signing & Channel Binding:**
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Domain controller: LDAP server signing requirements: Require signing`

5. **Lateral Movement & Privilege Escalation Protection**

   - **Restrict Local Administrator & RDP Access:**
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> User Rights Assignment -> Deny access to this computer from the network: Add Guests, Everyone`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> User Rights Assignment -> Deny log on through Remote Desktop Services: Add Guests, Everyone`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> Security Options -> Network access: Restrict anonymous access to Named Pipes and Shares: Enabled`

6. **Windows Auditing Configuration (CIS Benchmark Recommendations)**

   - **Enable Auditing for Critical Events:**
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Advanced Audit Policy Configuration -> Audit Policies -> Account Logon -> Audit Credential Validation: Success and Failure`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Advanced Audit Policy Configuration -> Audit Policies -> Account Management -> Audit Security Group Management: Success and Failure`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Advanced Audit Policy Configuration -> Audit Policies -> Logon/Logoff -> Audit Logon: Success and Failure`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Advanced Audit Policy Configuration -> Audit Policies -> Object Access -> Audit File Share: Success and Failure`
     - `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Advanced Audit Policy Configuration -> Audit Policies -> System -> Audit System Integrity: Success and Failure`
