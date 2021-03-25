# Microsoft Graph Security Events (including MCAS) to Cisco SecureX create Casebook

Create SecureX Casebook base on Microsoft Graph Security Events (including MCAS).

Use cases : 
  - Track compromised Azure AD accounts
  - Track the potential source IP of guessing password scan in Azure AD tenant
  - Parse observables from Microsoft Graph Security Events.
  - Link Microsoft Graph Security Events (including MCAS) to other Cisco Secure Platform events


For any questions or comments/bugs please reach out to me at alexandre@argeris.net or aargeris@cisco.com

![image](./img/Screen_Shot_casebook.png)
<br/>

# Main workflows:

- Events - Microsoft Graph Security.json from this repo

This workflow will fetch Microsoft Graph Security Events every 1hour. Detail will be parse to create a casebook in SecureX platform and identifying observables when possible.
  
![image](./img/Screen_Shot_workflow.png)
<br/>  

# Prerequisites:
Refence for best practice and documentation https://ciscosecurity.github.io/sxo-05-security-workflows/

- Create a Azure Entreprise Application (https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/what-is-application-managemen)
-     
- Copy the credentials Tenant ID, Client ID, Client Secret into Cisco SecureX Orchestration variable section:

  - variables [Azure_Tenant ID], [Azure clientid], [Azure client_secret]

- Create (2) Azure Target based on the hostname in the Cisco SecureX Orchestration. 

  - Name: Azure_For_Access_Token
  - No account keys: True
  - HTTPS protocol, host/IP address: login.microsoftonline.com
  - Proxy: Ignore Proxy

  - Name: Azure_Grpah_API
  - No account keys: True
  - HTTPS protocol, host/IP address: graph.microsoft.com
  - Proxy: Ignore Proxy  


# Import these workflows into SecureX Orchestration as Atomic actions:
  
- Threat Response v2 - Generate Access Token.json from https://github.com/CiscoSecurity/sxo-05-security-workflows/tree/Main/Atomics
  
  This Atomic action will get CTR access token.

- Threat Response v2 - Create Casebook.json from https://github.com/CiscoSecurity/sxo-05-security-workflows/tree/Main/Atomics
  
  This Atomic action will create Casebook.  
  
-  Azure Graph - Get Access Token.json from https://github.com/CiscoSecurity/sxo-05-security-workflows/tree/Main/Atomics  

- This Atomic action will fetch Azure token.


# References 
https://docs.microsoft.com/en-us/graph/security-concept-overview  
https://docs.microsoft.com/en-us/graph/api/resources/alert?view=graph-rest-1.0
https://docs.microsoft.com/en-us/graph/permissions-reference
