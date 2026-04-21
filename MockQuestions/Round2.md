❓ **Question 1:** You have an Azure Storage account container named container1.

You need to configure access to the container to meet the following requirements:

- The shared access signature (SAS) token should be secured with Microsoft Entra ID credentials.
- Role-based access control (RBAC) should be used.
- The SAS token should support granting access to containers.

Which type of SAS should you use?

Select only one answer.

**Options:**
- account
- user delegation ✅
- service
- stored access policy

**Answer:** user delegation ✅

🔍 **Explanation:** This item tests the candidate's knowledge of securing an Azure Storage account, which is part of developing solutions that use blob storage.

User delegation SAS fulfills all the requirements, including securing the SAS token with Microsoft Entra ID credentials, RBAC support, and granting access to containers. Azure Storage supports creating a new type of SAS at the level of the storage account. A service SAS delegates access to a resource in just one of the storage services (i.e., Blob, Queue, Table, or File). A stored access policy serves to group shared access signatures and to provide additional restrictions for signatures that are bound by the policy. The account, service, and stored access policy SAS types do not fulfill the requirement of securing the SAS token with Microsoft Entra ID credentials and RBAC support to manage permissions.

---

❓ **Question 2:** You manage an Azure App Service web app named app1. App1 is registered as an application in Microsoft Entra ID.

You need to ensure that Microsoft Entra ID signed-in user information can be retrieved by app1 by using Microsoft Graph.

What should you configure?

Select only one answer.

**Options:**
- appRoles
- application permissions
- groupMembershipClaims
- delegated permissions ✅

**Answer:** delegated permissions ✅

🔍 **Explanation:** This item tests the candidate's knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.

Delegated permissions are used by apps that have a signed-in user present. For these apps, either the user or an administrator consents to the permissions that the app requests and the app can function as the signed-in user when making calls to Microsoft Graph. appRoles is an attribute in the application manifest of the registered application that specifies the collection of roles that an app may declare. These roles can be assigned to users, groups, or service principals. Application permissions are used by apps that run without a signed-in user present. For example, apps that run as background services or daemons. An administrator can only permit application permissions. groupMembershipClaims is an attribute in the application manifest of the registered application that configures the groups claim issued in a user or OAuth 2.0 access token that the app expects. AppRoles, application permissions, and groupMembershipClaims will not allow signed-in user information to be retrieved in the code.

---

❓ **Question 3:** You plan to use Microsoft Graph to retrieve a list of users in a Microsoft Entra ID tenant.

You need to optimize query results.

Which two query options should you use? Each correct answer presents part of the solution.

Select all answers that apply.

**Options:**
- $filter ✅
- $count
- $orderby
- $select ✅
- $expand

**Answer:** $filter ✅, $select ✅

🔍 **Explanation:** This item tests the candidate's knowledge of Microsoft Graph query options.

The `$filter` query option must be used to limit the results returned. The `$select` query option limits the attributes projected from the result set, making the query more efficient. The `$count` query option is meant to retrieve the total count of matching resources. The `$expand` query option is used to retrieve related resources. Neither `$count` nor `$expand` directly optimize query results.

---

❓ **Question 4:** You have an Azure Storage account.

You need to provide external users the ability to create and update blobs.

Which enum value of BlobSasPermissions should you use?

Select only one answer.

**Options:**
- Add
- Create
- Read
- Write ✅

**Answer:** Write ✅

🔍 **Explanation:** This item tests the candidate's knowledge of creating and implementing blobs.

The Write permission will allow users to create and update blobs. The Add permission is only applicable for append blobs. The Create permission only allows users to create blobs — it does not allow users to update blobs. The Read permission does not allow users to create and update blobs.

---

❓ **Question 5:** You develop an application. The application will be accessed by a supplier.

The supplier requires a shared access signature (SAS) to access Azure services in your company's subscription.

You need to secure the SAS.

Which three actions should you take? Each correct answer presents a complete solution.

Select all answers that apply.

**Options:**
- Always use HTTPS. ✅
- Grant permission to multiple resources.
- Use Azure Monitor and Azure Storage logs to monitor the application. ✅
- Define a stored access policy for a service SAS. ✅
- Set a long expiration time.

**Answer:** Always use HTTPS. ✅  
Use Azure Monitor and Azure Storage logs to monitor the application. ✅  
Define a stored access policy for a service SAS. ✅

🔍 **Explanation:** This item tests the candidate's knowledge of creating and implementing shared access signatures (SAS).

The recommendation of always using HTTPS is valid and should be followed. Azure Monitor and storage analytics logging should be used to observe any spike in authorization failures. Stored access policies give the option to revoke permissions for a service SAS without having to regenerate the storage account keys. A security best practice is to provide a user with the minimum required privileges. It is best to use near-term expiration times on an ad-hoc SAS so that even if a SAS is compromised it is valid only for a short time. Granting permission to multiple resources violates least privilege principles.

---

❓ **Question 6:** You manage a Microsoft Entra ID registered application named app1. App1 calls a web API, which then calls Microsoft Graph.

You need to ensure the signed-in user identity is delegated through the request chain.

Which authentication flow should you use?

Select only one answer.

**Options:**
- Authorization code
- On-Behalf-Of ✅
- Client credentials
- Implicit

**Answer:** On-Behalf-Of ✅

🔍 **Explanation:** This item tests the candidate's knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.

OAuth 2.0 On-Behalf-Of flow (OBO) is used when an application invokes a service or web API, which in turn needs to call another service or web API. The idea is to propagate the delegated user identity and permissions through the request chain. The OAuth 2.0 authorization code grant can be used in apps that are installed on a device to gain access to protected resources, such as web APIs. The OAuth 2.0 client credentials grant flow permits a web service (confidential client) to use its own credentials, instead of impersonating a user, to authenticate when calling another web service. Implicit is a redirection-based flow and does not propagate user identity through a service-to-service chain.

---

❓ **Question 7:** You plan to generate a shared access signature (SAS) token for read access to a blob in a storage account.

You need to secure the token from being compromised.

What should you use?

Select only one answer.

**Options:**
- Primary account key
- Secondary account key
- Microsoft Entra ID credentials assigned the Contributor role ✅
- Microsoft Entra ID credentials assigned the Reader role

**Answer:** Microsoft Entra ID credentials assigned the Contributor role ✅

🔍 **Explanation:** This item tests the candidate's knowledge of Azure Storage shared access signatures (SAS).

Microsoft Entra ID credentials are required to generate the SAS token. The account used must have the `Microsoft.Storage/storageAccounts/blobServices/generateUserDelegationKey` permission, which is present in the following built-in roles: Contributor, Storage Account Contributor, Storage Blob Data Contributor, Storage Blob Data Owner, Storage Blob Data Reader, and Storage Blob Delegator. The Reader role does not include the `generateUserDelegationKey` permission. Using account keys (primary or secondary) can generate the SAS token but they can be more easily compromised.

---

❓ **Question 8:** You are developing a solution that stores secrets in an Azure Key Vault named myvault.

You need to retrieve the value for a secret named mysecret that is stored in myvault.

Which CLI command should you use?

Select only one answer.

**Options:**
- `az keyvault secret recover --name mysecret --vault-name myvault`
- `az keyvault secret recover --id myvault/mysecret`
- `az keyvault secret show --id myvault/mysecret`
- `az keyvault secret show --name mysecret --vault-name myvault` ✅

**Answer:** `az keyvault secret show --name mysecret --vault-name myvault` ✅

🔍 **Explanation:** This item tests the candidate's knowledge of developing code that uses keys, secrets, and certificates stored in Azure Key Vault.

The CLI command `az keyvault secret` offers several commands to work with secrets. The most commonly used commands are `set` for storing a secret and `show` to get the secret's value. When using these commands, either an `--id` specifying the full secret identification (in the format `https://keyvaultname.vault.azure.net/secrets/secret-name/secret-version`) or the `--name` and `--vault-name` must be specified. The `recover` subcommand is used to restore a deleted secret, not retrieve an existing one. The `--id` value of `myvault/mysecret` is not a valid full secret URI.

---

❓ **Question 9:** You have an Azure web app named WebApp1. WebApp1 has a system-assigned managed identity enabled.

You need to ensure that WebApp1 can write data to an Azure SQL database named SQLDb1. The solution must follow the principle of least privilege.

Which role should you assign to WebApp1?

Select only one answer.

**Options:**
- Contributor role for WebApp1.
- db_datawriter role for WebApp1. ✅
- Reader role for WebApp1.
- SQL Server Contributor role for WebApp1.

**Answer:** db_datawriter role for WebApp1. ✅

🔍 **Explanation:** This item tests the candidate's knowledge of implementing Managed Identities for Azure resources.

Assigning the `db_datawriter` database role allows the web app's managed identity to write data to the Azure SQL database, while granting only the permissions required for that operation — satisfying the principle of least privilege. The other options are incorrect because Azure RBAC roles such as Contributor, Reader, and SQL Server Contributor apply to Azure resource management and do not grant permissions to read or write data within an Azure SQL database.

---

❓ **Question 10:** You manage APIs in production by using Azure API Management.

You need to remove `X-Powered-By` and `X-AspNet-Version` headers from a response.

Which code segment should you use?

Select only one answer.

**Options:**
- Outbound section with `exists-action="append"` for both headers.
- Backend section with `exists-action="delete"` for both headers.
- Outbound section with `exists-action="delete"` for both headers. ✅
- Backend section with `exists-action="append"` for both headers.

**Answer:** Outbound section with `exists-action="delete"` for both headers. ✅

```xml
<policies>
  <inbound>
    <base />
  </inbound>
  <backend>
    <base />
  </backend>
  <outbound>
    <set-header name="X-Powered-By" exists-action="delete" />
    <set-header name="X-AspNet-Version" exists-action="delete" />
    <base />
  </outbound>
  <on-error>
    <base />
  </on-error>
</policies>
```

🔍 **Explanation:** This item tests the candidate's knowledge of defining policies for APIs using Azure API Management.

The `set-header` policy with `exists-action="delete"` placed in the **outbound** section removes the specified headers from the HTTP response before it is returned to the client. Using `append` instead of `delete` would add additional header values rather than removing them. Placing the policy in the **backend** section instead of **outbound** targets the forwarded request to the backend service, not the response — so headers would not be removed from the response visible to consumers.
