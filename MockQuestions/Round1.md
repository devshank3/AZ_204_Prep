❓ **Question 1:** A company uses Azure API Management to expose some of its services.

Each developer consuming APIs must use a single key to obtain access to various APIs without requiring approval from the API publisher.

You need to recommend a solution.

Which solution should you recommend?

Select only one answer.

**Options:**
- Define a subscription with all APIs scope.
- Define a subscription with product scope. ✅
- Restrict access based on caller IPs.
- Restrict APIs based on client certificate.

**Answer:** Define a subscription with product scope. ✅

🔍 **Explanation:** This item tests the candidate's knowledge of Azure API Management subscriptions.

When creating a product, several APIs can be added to the product and a subscription can be associated with it. Access should not be granted to all APIs. Developer access should be granted regardless of the caller IP. A client certificate would require a policy to validate the certificate and specific logic to map the client to specific APIs.

Secure APIs by using subscriptions - Training | Microsoft Learn

---

❓ **Question 2:** An e-commerce platform is planning to expand its services globally. The platform is hosted on Azure and utilizes various Azure services and third-party integrations.

You need to design and create a robust monitoring solution that can scale with the expansion and provide insights into the performance of the platform across different regions.

What should you do?

Select only one answer.

**Options:**
- Deploy multiple Application Insights instances for each region and use Azure Monitor to aggregate the data. ✅
- Implement a single Application Insights instance with default settings to monitor the entire platform.
- Create web tests and alerts for each region within a single Application Insights instance.
- Use manual instrumentation to log user activities and store them in Azure Blob Storage for later analysis.

**Answer:** Deploy multiple Application Insights instances for each region and use Azure Monitor to aggregate the data. ✅

🔍 **Explanation:** Option A is correct because deploying multiple Application Insights instances for each region allows for localized monitoring, and using Azure Monitor to aggregate the data provides a centralized view of global performance. Option B is incorrect as a single instance may not scale effectively for global monitoring. Option D is incorrect because manual instrumentation and storage in Azure Blob Storage do not provide real-time monitoring and analysis capabilities. Option C is incorrect web tests and alerts are just part of a robust monitoring solution.

Monitor app performance - Training | Microsoft Learn
Analyze metrics with Azure Monitor metrics explorer - Training | Microsoft Learn

---

❓ **Question 3:** You have an ASP.NET Core app named App1 that you deploy to Azure App Service web app.

You enable and configure Application Insights for App1.

You need to view detailed information from Application Insights about App1 transactions. The solution must minimize administrative effort.

What should you use?

Select only one answer.

**Options:**
- Application Insights resource ✅
- Azure Advisor recommendations
- live stream metrics
- performance metrics

**Answer:** Application Insights resource ✅

🔍 **Explanation:** The correct solution is to use the Application Insights resource, because it provides access to end-to-end transaction details including request traces, dependencies, exceptions, and telemetry collected from App1. This allows you to drill into detailed transaction diagnostics with minimal configuration once Application Insights is enabled. Azure Advisor recommendations provide optimization guidance but not transaction data. Live stream metrics show real-time telemetry such as request rate and failure rate but not full transaction traces. Performance metrics focus on aggregated system statistics like CPU and memory, not transaction-level diagnostics. Therefore, only the Application Insights resource delivers detailed transaction information with minimal administrative effort.

---

❓ **Question 4:** Practice Assessment for Exam AZ-204: Developing Solutions for Microsoft Azure
Question 3 of 50

You have a web service in Azure that uses an Azure SQL Database instance and is instrumented by using Application Insights.

You need to write a query to identify how long it takes for a specific web service call to retrieve data from the database.

Which type of data should you query in Application Insights?

Select only one answer.

**Options:**
- customEvents
- dependencies ✅
- performanceCounters
- requests

**Answer:** dependencies ✅

🔍 **Explanation:** The correct solution is to query dependencies, because Application Insights tracks external calls made by your service, including SQL Database queries, REST APIs, and storage operations. Dependency telemetry includes duration, success/failure, and target resource, making it ideal for measuring how long a web service call takes to retrieve data from the database. customEvents capture user-defined actions in the application but do not include database timings. performanceCounters provide system-level metrics such as CPU or memory usage, and requests represent incoming calls to the web service, not outbound database calls. Therefore, dependency data is the right source for identifying query durations to Azure SQL Database.

Use Azure Application Insights
Monitor Azure resources with Azure Monitor
Describe Azure Monitor
Monitor your networks using Azure Monitor

---

❓ **Question 5:** You deploy a web app named App1 by using Azure DevOps. App1 includes releases for a mobile app and a desktop app.

You need to perform a root cause analysis (RCA) to monitor the performance of App1. The solution must meet the following requirements:

Identify related code that causes load.
Ensure that you can view logs and identify any failures that cause issues with the desktop app.
Minimize administrative effort.
What should you use?

Select only one answer.

**Options:**
- Application Insights ✅
- Azure Analytics
- Azure Monitor
- Log Analytics

**Answer:** Application Insights ✅

🔍 **Explanation:** The correct solution is Application Insights, because it is designed to provide deep application performance monitoring, transaction traces, exception logging, and telemetry that links failures directly to code, making it ideal for root cause analysis of both web and desktop components. It integrates easily with DevOps pipelines and requires minimal setup once enabled. Azure Monitor provides high-level observability across Azure resources but lacks the detailed code-level diagnostics needed for RCA. Log Analytics is used to query and analyze log data, often from Application Insights or Azure Monitor, but by itself it does not capture application telemetry. Azure Analytics is not a valid Azure monitoring service. Therefore, Application Insights best satisfies the requirements with the least administrative effort.

Explore Application Insights
Monitor Azure Functions and Event Hubs
Monitor Azure resources with Azure Monitor
Use Azure Application Insights 
Implement Application Insights
Summary

---

❓ **Question 6:** You have an Azure Storage account container named container1.

You need to configure access to the container to meet the following requirements:

The shared access signature (SAS) token should be secured with Microsoft Entra ID credentials.
Role-based access control (RBAC) should be used.
The SAS token should support granting access to containers.
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

Secure your Azure Storage account - Training | Microsoft Learn

---

❓ **Question 7:** You have an Azure Storage account.

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

The Write permission will allow users to create and update blobs. The Add permission is only applicable for append blobs. The Create permission only allows users to create blobs. It does not allow users to update blobs. The Read permission does not allow users to create and update blobs.

---

❓ **Question 8:** You develop an application. The application will be accessed by a supplier.

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

The recommendation of always using HTTPS is valid and should be followed. Azure Monitor and storage analytics logging should be used to observe any spike in these types of authorization failures. Stored access policies will give the option to revoke permissions for a service SAS without having to regenerate the storage account keys. A security best practice is to provide a user with the minimum required privileges. It is best to use near-term expiration times on an ad-hoc SAS service or account SAS so that even if a SAS is compromised it is valid only for a short time.

Grant limited access to Azure Storage resources using shared access signatures (SAS)

---

❓ **Question 9:** You develop a multitenant web application named App1. You plan to register App1 with multiple Microsoft Entra ID tenants.

You need to identify the relationship between the application objects and security principals associated with App1.

Which relationship should you identify?

Select only one answer.

**Options:**
- App1 will have multiple application objects and multiple service principals.
- App1 will have multiple application objects and a single service principal.
- App1 will have a single application object and multiple service principals. ✅
- App1 will have a single application object and a single service principal.

**Answer:** App1 will have a single application object and multiple service principals. ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring authentication of multitenant applications, which is a common scenario when implementing authentication.

App1 will have a single application object and multiple service principals. App1 will not have multiple application objects. multiple application objects and a single service principal., or a single service principal.

Explore service principals - Training | Microsoft Learn

---

❓ **Question 10:** You need to generate a shared access signature token that grants the Read permission to a blob container.

Which code segment should you use?

Select only one answer.

**Options:**
- BlobSasBuilder sasBuilder = new BlobSasBuilder()  
  {  
  BlobContainerName = containerClient.Name,  
  Resource = "b"  
  };  
  sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);  
  sasBuilder.SetPermissions(BlobContainerSasPermissions.Read);  
  Uri sasUri = containerClient.GenerateSasUri(sasBuilder);
- BlobSasBuilder sasBuilder = new BlobSasBuilder()  
  {  
  BlobContainerName = containerClient.Name,  
  Resource = "c"  
  };  
  sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);  
  sasBuilder.SetPermissions(BlobContainerSasPermissions.Read);  
  Uri sasUri = containerClient.GenerateSasUri(sasBuilder); ✅
- BlobSasBuilder sasBuilder = new BlobSasBuilder()  
  {  
  BlobContainerName = containerClient.Name,  
  Resource = "c"  
  };  
  sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);  
  sasBuilder.SetPermissions(BlobContainerSasPermissions.Create);  
  Uri sasUri = containerClient.GenerateSasUri(sasBuilder);
- BlobSasBuilder sasBuilder = new BlobSasBuilder()  
  {  
  BlobContainerName = containerClient.Name,  
  Resource = "b"  
  };  
  sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);  
  sasBuilder.SetPermissions(BlobContainerSasPermissions.Create);  
  Uri sasUri = containerClient.GenerateSasUri(sasBuilder);

**Answer:** BlobSasBuilder sasBuilder = new BlobSasBuilder()  
{  
BlobContainerName = containerClient.Name,  
Resource = "c"  
};  
sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);  
sasBuilder.SetPermissions(BlobContainerSasPermissions.Read);  
Uri sasUri = containerClient.GenerateSasUri(sasBuilder); ✅

🔍 **Explanation:** This item tests the candidate's knowledge of creating and implementing shared access signatures.

The code segment that includes Resource = "c" and sasBuilder.SetPermissions(BlobContainerSasPermissions.Read); will generate the shared access signatures token that grants the Read permission to a blob container. The code segment that includes resource = 'b' will generate a shared access signatures token at the blob level. The code segments that include sasBuilder.SetPermissions(BlobContainerSasPermissions.Create); will generate a shared access signatures token with the Create permission at the blob level.

Store data in Azure learning path - Training | Microsoft Learn

---

📝 **Additional Notes:** Managed identities for Azure resources eliminate the need to manage credentials in code. A system-assigned managed identity is restricted to one per resource and is tied to the lifecycle of the resource. Once enabled for app1, it will automatically create a service principal without the need to manage credentials and cannot be explicitly deleted.

A Microsoft Entra ID application is defined by its one and only application object, which resides in the Microsoft Entra ID tenant where the application was registered (known as the application's home tenant). It cannot be used by app1 to access a storage account without managing credentials. A user-assigned managed identity can be created and assigned to one or more instances of an Azure service. Once enabled for app1, a user-assigned managed identity will automatically create a service principal without the need to manage but will need to be explicitly deleted. The legacy service principal represents a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences. The legacy service principal cannot be used to access a storage account without managing credentials.

---

❓ **Question 11:** You manage an Azure App Service web app named app1 and an Azure Key Vault named vault1.

You need to ensure app1 can authenticate and conduct operations with vault1 without managing the rotation of a secret. The resource required to implement the solution must be deleted automatically when the app is deleted

Which authentication method should you use for app1?

Select only one answer.

**Options:**
- user-assigned managed identity
- service principal and secret
- service principal and certificate
- system-assigned managed identity ✅

**Answer:** system-assigned managed identity ✅

🔍 **Explanation:** This item tests the candidate's knowledge of implementing Azure Key Vault, which is part of implementing Secure Cloud solutions.

A system-assigned managed identity can be used to ensure app1 can authenticate and perform operations with vault1 without managing rotation of a secret. A user-assigned managed identity can be used to ensure app1 can authenticate and perform operations with vault1, but the secret rotation needs to be managed. A service principal and a secret can be used to authenticate to the key vault, but it is difficult to automatically rotate the secret that is used to authenticate to the key vault. A service principal and an associated certificate with access to the key vault can be used for authentication but would require managing the rotation of a secret.

---

❓ **Question 12:** You need to generate a new version of a key stored in Azure Key Vault.

Which code segment should you use?

Select only one answer.

**Options:**
- az keyvault key rotation-policy update -n mykey --vault-name mykeyvault --value path/to/policy.json
- az keyvault key purge --name mykey --vault-name mykeyvault
- az keyvault key rotate --vault-name mykeyvault --name mykey ✅
- az keyvault key set-attributes --vault-name mykeyvault --name mykey –policy path/to/policy.json

**Answer:** az keyvault key rotate --vault-name mykeyvault --name mykey ✅

🔍 **Explanation:** This item tests the candidate's knowledge of setting key rotation by using the Azure CLI.

The Rotate operation will generate a new version of the key based on the key policy. The Rotation Policy operation updates the rotation policy of a key vault key. The Purge Deleted Key operation is applicable for soft-delete enabled vaults or HSMs. The Set Attributes operation changes specified attributes of a stored key.

Tutorial: Host a RESTful API with CORS in Azure App Service