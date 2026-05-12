❓ **Question 1:** You need to delete an image with the tag dev/nginx:latest from an Azure container registry named devregistry.

Which code segment should you use?

Select only one answer.

**Options:**
- `az acr repository delete --name devregistry --image dev/nginx:latest` ✅
- `az acr repository delete --name devregistry --suffix dev/nginx:latest`
- `az acr manifest delete --registry devregistry -n dev/nginx:latest`
- `az acr manifest delete --registry devregistry --suffix dev/nginx:latest --image dev/nginx:latest`

**Answer:** `az acr repository delete --name devregistry --image dev/nginx:latest` ✅

🔍 **Explanation:** This item tests the candidate's knowledge of publishing or deleting an image to Azure Container Registry.

The code segment `acr repository delete --name devregistry --image dev/nginx:latest` will delete the image from a container registry. The code segments that include the `suffix` parameter should be used if you are accessing the registry from a different subscription or have permission to access images but not permission to manage the registry resource. The code segments that include the `manifest` parameters delete the manifest of the artifact, not the image.

---

❓ **Question 2:** You are developing a .NET application that includes multiple container images. The application will be deployed to Azure Container Instances (ACI).

You need to ensure that an Azure file share can be mapped to each container of the application.

Which configuration should you use?

Select only one answer.

**Options:**
- pods
- confidential containers
- container group ✅
- virtual network deployment

**Answer:** container group ✅

🔍 **Explanation:** This item tests the candidate's knowledge of running containers by using Azure Container Instances (ACI).

The top-level resource in ACI is the container group. A container group is a collection of containers that get scheduled on the same host machine. You can specify external volumes to mount within a container group and map these volumes into specific paths within the individual containers in a group. A pod is a group of one or more containers with shared storage and network resources — pods can be used in Azure Kubernetes Service but not ACI. Confidential containers on ACI are used to ensure hardware-based confidentiality. A virtual network deployment cannot be used to map an Azure file share to each container in a multiple container scenario.

---

❓ **Question 3:** You need to deploy an Azure Files share along with a container group to Azure Container Instances (ACI).

Which deployment method should you use?

Select only one answer.

**Options:**
- YAML file
- Azure Resource Manager template ✅
- Docker Compose
- Azure CLI

**Answer:** Azure Resource Manager template ✅

🔍 **Explanation:** This item tests the candidate's knowledge of running containers by using Azure Container Instances (ACI).

There are two common ways to deploy a multi-container group: use an Azure Resource Manager template or a YAML file. An Azure Resource Manager template is recommended when you need to deploy additional Azure service resources (for example, an Azure Files share) when you deploy the container instances. A YAML file does not support the deployment of additional Azure service resources along with container groups in ACI. Docker Compose and Azure CLI do not support the deployment of an Azure Files share along with a container group to ACI.

---

❓ **Question 4:** You manage the deployment of an Azure Container Registry named registry1 for a company.

You need to ensure that registry1 can be shared across multiple groups in the company, enabling group isolation.

What should you use?

Select only one answer.

**Options:**
- artifact
- tag
- namespace ✅
- layer

**Answer:** namespace ✅

🔍 **Explanation:** This item tests the candidate's knowledge of publishing an image to Azure Container Registry.

A namespace enables the identification of related repositories and artifact ownership by using forward slash-delimited names. A repository is a collection of container images or other artifacts in a registry that have the same name but different tags. A tag for an image specifies its version. An artifact can be, for instance, a text file, a docker image, or a Helm chart stored in the registry with one or more tags. Layers are used to avoid transferring redundant information and to skip build steps that have not changed.

---

❓ **Question 5:** Your company is developing an application that includes a backend web API service. The development team has decided to use Azure Container Apps to host the API. They have a Dockerfile in the root of their repository that defines the containerized app.

You need to deploy the container app using the Dockerfile.

What should you do?

Select only one answer.

**Options:**
- Use the `az containerapp env create` command with the `--name` parameter.
- Use the `az containerapp create` command with the `--image` parameter.
- Use the `az containerapp create` command with the `--containername` parameter.
- Use the `az containerapp up` command with the `--source .` parameter. ✅

**Answer:** Use the `az containerapp up` command with the `--source .` parameter. ✅

🔍 **Explanation:** The `az containerapp up` command with the `--source .` parameter builds and deploys the container app using the Dockerfile in the root of the repository. The other options either do not exist or do not fulfill the requirement.

---

❓ **Question 6:** You develop a web application hosted on the Web Apps feature of Microsoft Azure App Service.

You need to enable and configure Azure Web Service Local Cache with 1.5 GB.

Which two code segments should you use? Each correct answer presents part of the solution.

Select all answers that apply.

**Options:**
- `"WEBSITE_LOCAL_CACHE_OPTION": "Always"` ✅
- `"WEBSITE_LOCAL_CACHE_SIZEINMB": "1500"` ✅
- `"WEBSITE_LOCAL_CACHE_OPTION": "Enable"`
- `"WEBSITE_LOCAL_CACHE_SIZEINMB": "1.5"`

**Answer:** `"WEBSITE_LOCAL_CACHE_OPTION": "Always"` ✅, `"WEBSITE_LOCAL_CACHE_SIZEINMB": "1500"` ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring the settings of the Web Apps feature of Azure App Service.

By using `WEBSITE_LOCAL_CACHE_OPTION = Always`, local cache will be enabled. `WEBSITE_LOCAL_CACHE_SIZEINMB` set to `"1500"` will properly configure Local Cache with 1.5 GB of size. `WEBSITE_LOCAL_CACHE_OPTION = Enable` is not a valid value. `"1.5"` will not configure 1.5 GB for the local cache.

---

❓ **Question 7:** You plan to develop an Azure App Service web app named app1 by using a Windows custom container.

You need to load a TLS/SSL certificate in application code.

Which app setting should you configure?

Select only one answer.

**Options:**
- `WEBSITE_LOAD_CERTIFICATES` ✅
- `WEBSITE_ROOT_CERTS_PATH`
- `WEBSITE_CORS_ALLOWED_ORIGINS`
- `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL`

**Answer:** `WEBSITE_LOAD_CERTIFICATES` ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring app settings, which is part of creating Azure App Service Web Apps.

The `WEBSITE_LOAD_CERTIFICATES` app setting makes the specified certificates accessible to Windows or Linux custom containers as files. The `WEBSITE_ROOT_CERTS_PATH` app setting is read-only and does not allow comma-separated thumbprint values to be loaded in the code. The `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL` app setting is used to instruct the auth module to store and load all encrypted tokens to the specified blob storage container — it cannot be used to load certificates inside a Windows custom container.

---

❓ **Question 8:** You create an Azure web app locally. The web app consists of a ZIP package.

You need to deploy the web app by using the Azure CLI. The deployment must reduce the likelihood of locked files.

What should you do?

Select only one answer.

**Options:**
- Run `az webapp deploy` specifying `--clean true`.
- Run `az webapp deploy` specifying `--restart true`.
- Run `az webapp deploy` to a staging slot with auto swap on. ✅
- Run `az webapp deploy` by using a high value for the `--timeout` parameter.

**Answer:** Run `az webapp deploy` to a staging slot with auto swap on. ✅

🔍 **Explanation:** This item tests the candidate's knowledge of deploying Azure Web Apps using the Azure CLI.

Using a production and staging slot with auto swap enabled reduces the likelihood of locked files. If `--clean true` is used, the target folder is cleaned, but this has no effect on the likelihood of locked files. Restarting the app after deployment is the default behavior of a ZIP deployment and has no effect on reducing locked files. The `--timeout` parameter has no effect on the likelihood of locked files.

---

❓ **Question 9:** You manage the staging and production deployment slots of an Azure App Service web app named app1.

You need to ensure a connection string is not swapped when swapping is performed.

Which configuration should you use?

Select only one answer.

**Options:**
- Deployment Center
- Deployment slot setting ✅
- Managed identity
- Scale up

**Answer:** Deployment slot setting ✅

🔍 **Explanation:** This item tests the candidate's knowledge of deploying code to Azure App Service, which is part of creating Azure App Service Web Apps.

Marking a setting as a deployment slot setting keeps it sticky to that deployment slot. For example, an app setting marked as a deployment slot setting on app1 will always stick with app1 and will never move to app1/staging during a swap. The Deployment Center setting is used to configure continuous and manual deployment. Managed identity provides an identity for applications to use when connecting to resources that support Microsoft Entra ID authentication. Scale up ensures the web app is entitled to CPU, memory, disk space, and extra features such as dedicated virtual machines. Deployment Center, Managed Identity, and Scale up cannot ensure a connection string is not swapped.

---

❓ **Question 10:** You need to configure a web app to allow external requests from https://myapps.com.

Which Azure CLI command should you use?

Select only one answer.

**Options:**
- `az webapp cors add -g MyResourceGroup -n MyWebApp --allowed-origins https://myapps.com` ✅
- `az webapp identity add -g MyResourceGroup -n MyWebApp --allowed-origins https://myapps.com`
- `az webapp traffic-routing set --distribution myapps=100 --name MyWebApp --resource-group MyResourceGroup`
- `az webapp config access-restriction add -g MyResourceGroup -n MyWebApp --rule-name external --action Allow --ids myapps --priority 200`

**Answer:** `az webapp cors add -g MyResourceGroup -n MyWebApp --allowed-origins https://myapps.com` ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring web app settings.

The code segment that includes `cors add` will configure CORS to allow requests from https://myapps.com. The code segment that includes `identity add` will add a managed identity to a web app. The code segment that includes `traffic-routing set` will configure traffic routing to a deployment slot named myapps. The code segment that includes `access-restriction add` will add an access restriction on a web app.

---

❓ **Question 11:** You manage a multi-instance deployment of an Azure App Service web app named app1.

You need to ensure a client application is routed to the same instance for the life of the session.

Which platform setting should you use?

Select only one answer.

**Options:**
- WebSocket
- Always on
- HTTP version
- ARR Affinity ✅

**Answer:** ARR Affinity ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring web app settings, which is part of creating Azure App Service Web Apps.

In a multi-instance deployment, the ARR Affinity setting ensures a client application is routed to the same instance for the life of the session. WebSocket is a standardized protocol that provides full-duplex communication. Always on keeps the app loaded even when there is no traffic. HTTP version allows use of persistent connections to service multiple simultaneous requests. WebSocket, Always on, and HTTP version are not used to ensure a client is routed to the same instance for the life of the session.

---

❓ **Question 12:** You plan to create an Azure Functions app named app1.

You need to ensure that app1 will satisfy the following requirements:

- Supports automatic scaling.
- Has event-based scaling behavior.
- Provides a serverless pricing model.

Which hosting plan should you use?

Select only one answer.

**Options:**
- App Service
- App Service Environment
- Consumption ✅
- Functions Premium

**Answer:** Consumption ✅

🔍 **Explanation:** This item tests the candidate's knowledge of selecting the appropriate hosting plan, which is part of the implementation of Azure Functions.

The Consumption hosting plan satisfies all requirements: it supports autoscaling, has event-based scaling behavior, and provides a serverless pricing model. The App Service, App Service Environment, and Functions Premium hosting plans support autoscaling but do not provide a serverless pricing model, and their scaling behavior is performance-based rather than event-based.

---

❓ **Question 13:** A company plans to implement a Microsoft Defender for Cloud solution.

The company has the following requirements:

- Notifies when DNS domains are not deleted when a new Azure Functions app is deleted.
- Use native alerting.
- Minimize costs.

You need to select a hosting plan.

Which hosting plan should you use?

Select only one answer.

**Options:**
- Consumption
- Standard ✅
- Premium
- Free

**Answer:** Standard ✅

🔍 **Explanation:** This item tests the candidate's knowledge about securing Azure Functions.

The Standard plan supports both custom domains and Microsoft Defender for Cloud, which can automatically alert on dangling DNS domains, while minimizing costs. The Consumption plan does not support Microsoft Defender for Cloud. The Premium plan supports custom domains and Microsoft Defender for Cloud with dangling DNS alerts, but it is not the lowest cost option. The Free plan does not support custom domains.

---

❓ **Question 14:** You create a batch routine by using a timer trigger in Azure Functions.

You need to configure the batch routine to execute every 15 minutes, from Monday through Friday.

Which code segment should you use?

Select only one answer.

**Options:**
- `[TimerTrigger("0 */15 * * * 1-5")]` ✅
- `[TimerTrigger("*/15 * * * 0-4")]`
- `[TimerTrigger("0 15 * * * ")]`
- `[TimerTrigger("* 15 * * 1-5")]`

**Answer:** `[TimerTrigger("0 */15 * * * 1-5")]` ✅

🔍 **Explanation:** This item tests the candidate's knowledge of working with timer triggers in Azure Functions.

The code segment `"0 */15 * * * 1-5"` executes the function every 15 minutes from Monday to Friday. The code segment `"*/15 * * * 0-4"` is missing the seconds field and uses an incorrect day-of-week range. The code segment `"0 15 * * * "` executes only once at 15:00 (3 PM). The code segment `"* 15 * * 1-5"` is missing the seconds attribute and the step (`/`) part for the minutes.

---

❓ **Question 15:** You are developing an Azure Functions app that will be deployed to a Consumption plan. The app consumes data from a database server that has limited throughput.

You need to use the `functionAppScaleLimit` property to control the number of instances of the app that will be created.

Which value should you use for the property setting?

Select only one answer.

**Options:**
- 0
- 10 ✅
- null

**Answer:** 10 ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring an Azure Functions app.

Imposing limits on the scaling out capacity of an Azure Functions app can help when the app connects to components that have limited throughput. The `functionAppScaleLimit` property lets you define the maximum number of instances. Setting it to a low value, such as 10, is appropriate in this scenario. Azure Functions apps in the Consumption plan can scale out to 200 instances by default. A value of `0` or `null` for the `functionAppScaleLimit` property means that an unrestricted number of instances will be created.

---

❓ **Question 16:** You are developing an Azure Functions app that will be deployed to a Dedicated plan.

When there is a resource shortage in the app, it must send a "429 Too Busy" response.

You need to apply the appropriate configuration to all functions in an Azure Functions app instance.

Which configuration should you set?

Select only one answer.

**Options:**
- `dynamicThrottlesEnabled` in the host.json file ✅
- `bindings` section in the function.json file
- `maxOutstandingRequests` in the host.json file
- `maxConcurrentRequests` in the function.json file

**Answer:** `dynamicThrottlesEnabled` in the host.json file ✅

🔍 **Explanation:** This item tests the candidate's knowledge of controlling scaling of functions.

Using the `dynamicThrottlesEnabled` property allows the system to respond dynamically to increased utilization, returning "429 Too Busy" errors. This property is defined in the host.json file. The `bindings` section in function.json is used to define bindings and triggers for a function. The `maxConcurrentRequests` property determines the maximum number of function instances to run in parallel and is defined in function.json. The `maxOutstandingRequests` property in host.json defines the maximum number of requests queued or in progress at any given time, but does not return "429 Too Busy".

---

❓ **Question 17:** You have an Azure resource group that contains an Azure Cosmos DB account named Account1 and an Azure function named Function1. Account1 contains a database named db1 and a container named Container1 that stores inventory data for a warehouse. The data in Container1 is updated frequently.

Function1 must process updates to Container1 whenever data changes occur. Users report that the inventory data is inaccurate, and you discover that Function1 sometimes fails to run.

You need to ensure that Function1 executes when data in Container1 is created or updated.

What should you do?

Select only one answer.

**Options:**
- Configure Azure Event Grid to send the change feed of Container1 to the Event Grid topic to which Function1 is subscribed.
- Configure Container1 to connect to an Azure Functions app. Connect the Azure Functions app to Function1.
- Ensure that Function1 is listening to the change feed of Container1 by using the Azure Cosmos DB trigger. ✅
- Ensure that the value of the LeaseCollectionPrefix property for Function1 is ALL.

**Answer:** Ensure that Function1 is listening to the change feed of Container1 by using the Azure Cosmos DB trigger. ✅

🔍 **Explanation:** The correct solution is to configure Function1 to use the Azure Cosmos DB trigger so that it automatically processes changes captured in the change feed of Container1. This ensures the function executes reliably whenever inserts or updates occur. Event Grid can integrate with Cosmos DB but does not provide guaranteed ordered processing of changes in the same way the change feed trigger does. Configuring Container1 to "connect" directly to Function1 is not a valid option. Setting the `LeaseCollectionPrefix` property to "ALL" only affects lease container partitioning for scaling, not the reliability of the trigger itself.

---

❓ **Question 18:** You manage a multiregion deployment of an Azure Cosmos DB account named account1.

You need to configure the default consistency level for account1. The consistency level must maximize throughput and minimize latency for write operations.

Which consistency level should you use?

Select only one answer.

**Options:**
- Bounded Staleness
- Consistent Prefix
- Eventual ✅
- Session

**Answer:** Eventual ✅

🔍 **Explanation:** This item tests the candidate's knowledge of selecting the consistency level, which is part of developing Azure Cosmos DB solutions.

The Eventual consistency level maximizes throughput and minimizes latency. Bounded Staleness provides lower throughput and higher latency compared to the remaining choices. Consistent Prefix provides higher throughput and lower latency for write operations than Session, but lower throughput and higher latency than Eventual. Session provides higher throughput and lower latency than Bounded Staleness but lower throughput and higher latency than Eventual and Consistent Prefix.

---

❓ **Question 19:** You manage an Azure Cosmos DB container named container1.

You need to use the `ReadItemAsync` method to read an item from the Azure Cosmos service.

Which two parameters should you provide? Each correct answer presents part of the solution.

Select all answers that apply.

**Options:**
- consistencyLevel
- eTag
- partitionKey ✅
- sessionToken
- id ✅

**Answer:** partitionKey ✅, id ✅

🔍 **Explanation:** This item tests the candidate's knowledge of setting the partition key, which is part of developing Azure Cosmos DB solutions.

The `ReadItemAsync` method of the container class of the .NET SDK for Azure Cosmos DB has two mandatory parameters: `partitionKey` and `itemId`. The `consistencyLevel`, `eTag`, and `sessionToken` parameters are part of the optional `requestOptions` parameter of the `ReadItemAsync` method.

---

❓ **Question 20:** You plan to implement a storage mechanism for managing state across multiple change feed consumers.

You need to configure the change feed processor in the .NET SDK for Azure Cosmos DB for NoSQL API.

Which component should you use?

Select only one answer.

**Options:**
- Delegate
- Compute instance
- Lease container ✅
- Monitored container

**Answer:** Lease container ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring the change feed processor as part of developing solutions that use Azure Cosmos DB.

The lease container component serves as a storage mechanism to manage state across multiple change feed consumers. The delegate component is the code within the client application that implements business logic for each batch of changes. The compute instance is a client application instance that listens for changes from the change feed. The monitored container is monitored for any insert or update operations — it does not serve as a storage mechanism to manage state across multiple change feed consumers.

---

❓ **Question 21:** A company implements a multi-region Azure Cosmos DB account.

You need to configure the default consistency level for the account. The consistency level must ensure that update operations made as a batch within a transaction are always visible together.

Which consistency level should you use?

Select only one answer.

**Options:**
- Bounded Staleness
- Session
- Consistent Prefix ✅
- Eventual

**Answer:** Consistent Prefix ✅

🔍 **Explanation:** This item tests the candidate's knowledge of selecting the appropriate consistency level for operations in Azure Cosmos DB.

The Consistent Prefix consistency level ensures that updates made as a batch within a transaction are returned consistently with the transaction in which they were committed — write operations within a transaction of multiple documents are always visible together. Bounded Staleness is used to manage the lag of data between any two regions. Session is used to ensure that within a single client session, reads honor the read-your-writes and write-follows-reads guarantees. Eventual is used when no ordering guarantee is required.

---

❓ **Question 22:** You have an Azure storage lifecycle policy for block blobs.

You need to create a prefixMatch filter rule that will contain an array of strings for prefixes to be matched.

What should be the first element of the prefix string?

Select only one answer.

**Options:**
- a block blob index tag
- a block blob name
- a container name ✅
- a storage account name

**Answer:** a container name ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring a prefixMatch filter, which is an essential part of setting up storage policy and is part of solution development for blob storage.

When creating a prefixMatch filter rule for an Azure storage lifecycle policy for block blobs, the first element of the prefix string must be a container name — not a block blob index tag, block blob name, or storage account name.

---

❓ **Question 23:** You create a retention policy for block blobs using a prefixMatch of `"sample-container/blob1"`. You need to transition blobs in the Hot access tier to an online tier if the blobs have not been modified in over 90 days.

Which code segment should you add to the `baseBlob` actions?

Select only one answer.

**Options:**
- `"tierToArchive": { "daysAfterCreationGreaterThan": 90 }`
- `"tierToCool": { "daysAfterCreationGreaterThan": 90 }`
- `"tierToCool": { "daysAfterModificationGreaterThan": 90 }` ✅
- `"tierToArchive": { "daysAfterModificationGreaterThan": 90 }`

**Answer:** `"tierToCool": { "daysAfterModificationGreaterThan": 90 }` ✅

🔍 **Explanation:** This item tests the candidate's knowledge of blob tiers.

The code segment `"tierToCool": { "daysAfterModificationGreaterThan": 90 }` moves blobs not modified after 90 days to the Cool tier, as defined by the requirement. The code segments that include `"tierToArchive"` move blobs to the Archive tier, which is not an online access tier — it is an offline tier. The code segment `"tierToCool": { "daysAfterCreationGreaterThan": 90 }` moves blobs to the Cool tier 90 days after creation, which does not meet the requirement to move blobs after 90 days without modification.

---

❓ **Question 24:** You need to implement an Azure Storage lifecycle policy for append blobs.

Which rule action should you use?

Select only one answer.

**Options:**
- delete ✅
- enableAutoTierToHotFromCool
- tierToArchive
- tierToCool

**Answer:** delete ✅

🔍 **Explanation:** This item tests the candidate's knowledge of configuring Azure Storage lifecycle policy for blobs, which is an essential part of developing solutions for blob storage.

The `delete` rule action supports both block blobs and append blobs. The `enableAutoTierToHotFromCool`, `tierToArchive`, and `tierToCool` rule actions only support block blobs.

---

❓ **Question 25:** You are developing an application.

You need to set the standard HTTP properties of containers in Azure Blob Storage.

Which two HTTP properties can you set? Each correct answer presents part of the solution.

Select all answers that apply.

**Options:**
- ETag ✅
- Last-Modified ✅
- Cache-Control
- Origin
- Range

**Answer:** ETag ✅, Last-Modified ✅

🔍 **Explanation:** This item tests the candidate's knowledge of setting and retrieving properties and metadata.

Metadata in Azure Storage objects is defined through headers starting with `x-ms-meta-`. Some standard HTTP properties are also available for both objects and containers. The only two HTTP properties available for containers are ETag and Last-Modified. Cache-Control, Origin, and Range are properties only available for blobs, not containers.
