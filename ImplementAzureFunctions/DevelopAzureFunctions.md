# Develop Azure Functions

## Learning Objectives
- Explain the key components of a function
- Create triggers and bindings to control when a function runs and where output is directed
- Connect a function to Azure services
- Create a function using VS Code and Azure Functions Core Tools

---

## Function App
- **Unit of deployment and management** for functions
- All functions in a function app share: pricing plan, deployment method, runtime version
- In **Functions 2.x+**: all functions in a function app must use the **same language**

---

## Local Development
- Develop and debug functions locally using your preferred editor
- Local functions can connect to **live Azure services**
- Prefer local development over the Azure portal editor (portal has limitations)
- Publish your local project to Azure when ready

---

## Local Project Files

| File | Purpose |
|------|---------|
| `host.json` | Configuration affecting **all functions** in the app; bindings config applies to every function |
| `local.settings.json` | App settings and local dev tool settings; **only used locally** |

### host.json
- Settings can be overridden per environment via **application settings**

### local.settings.json
- Used only when running locally
- May contain **secrets** (connection strings) — **never commit to a remote repository**
- Must mirror required settings in Azure **app settings** when deploying

---

## Synchronize Settings
- Local settings required by the app must also exist in the deployed function app's **app settings**
- You can **download current settings** from Azure to your local project

---

## Triggers and Bindings

### Trigger
- Defines **how a function is invoked**
- A function must have **exactly one trigger**
- Trigger data is often the **function payload**

### Binding
- Declaratively connects another resource to the function
- Types: **input**, **output**, or both
- Data from bindings is provided as **function parameters**
- Bindings are **optional**; a function can have multiple input/output bindings
- Avoids hardcoding access to other services

---

### Local Testing Options for Non-HTTP Triggers
| Option | Use Case |
|--------|----------|
| Connection strings in `local.settings.json` → `Values` | Target live Azure services |
| **Azurite emulator** | Queue, Blob, Table Storage bindings without remote services |
| Admin endpoints | Manually invoke non-HTTP triggered functions |

> Use **separate services** for dev/test vs production.

---

### Trigger & Binding Configuration by Language

| Language | How |
|----------|-----|
| C# | Attributes on methods/parameters (in-process or isolated worker) |
| Java | Annotations on methods/parameters |
| JS/TS v4 | Code using `@azure/functions` (no function.json) |
| JS/TS v3 | `function.json` |
| Python v2 | Decorators (runtime generates function.json) |
| Python v1 | `function.json` |
| PowerShell | `function.json` |

> **Note:** Cannot mix programming models (v3/v4 or v1/v2) within the same function app.  
> For `function.json`-based languages, the portal **Integration tab** provides a UI for bindings.  
> For code-first models (Node.js v4, Python v2), configure in code and republish — don't edit portal directly.

---

### Binding Direction (`direction` property in function.json)
- **Triggers:** always `in`
- **Input bindings:** `in`
- **Output bindings:** `out`
- Special: `inout` (requires Advanced editor in portal)
- In C#/Java, direction is inferred from attribute constructor or parameter type

### `dataType` property (dynamically typed languages — JS v3, PowerShell)
```json
{ "dataType": "binary" }   // options: binary | stream | string
```

---

### Example: HTTP Trigger → Queue Output

**Scenario:** Write a queue message on every HTTP request received.

#### function.json (legacy — Node.js v3, Python v1, PowerShell)
```json
{
  "bindings": [
    { "type": "httpTrigger", "direction": "in", "name": "req", "authLevel": "function", "methods": ["get","post"] },
    { "type": "queue", "direction": "out", "name": "outqueue", "queueName": "outqueue", "connection": "AzureWebJobsStorage" }
  ]
}
```
> Disable a function via app setting `AzureWebJobs.<FunctionName>.Disabled=true` (not via `disabled` in function.json — legacy).

#### C# Isolated Worker
```csharp
[Function("HttpToQueue")]
public static MultiResponse Run(
    [HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req) { ... }

public class MultiResponse {
    [QueueOutput("outqueue", Connection = "AzureWebJobsStorage")]
    public string[] Messages { get; set; }
    public HttpResponseData HttpResponse { get; set; }
}
```

#### Node.js v4
```js
const queueOutput = output.storageQueue({ queueName: "outqueue", connection: "AzureWebJobsStorage" });
app.http("HttpToQueue", {
  extraOutputs: [queueOutput],
  handler: async (request, context) => {
    context.extraOutputs.set(queueOutput, "Processed request");
    return { status: 200 };
  }
});
```

#### Python v2
```python
@app.route(route="HttpToQueue", auth_level=func.AuthLevel.FUNCTION)
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpToQueue(req: func.HttpRequest, msg: func.Out[str]) -> func.HttpResponse:
    msg.set(req.get_body().decode("utf-8") or "Processed request")
    return func.HttpResponse("Queued", status_code=200)
```

---

## Connect Functions to Azure Services

### Storing Connection Secrets
- Azure Functions uses **App Service application settings** to securely store connection strings, keys, and tokens
- Settings are **stored encrypted** and exposed at runtime as **environment variables**
- For triggers/bindings with a `connection` property → set the **app setting name**, not the actual connection string
- Cannot configure a binding directly with a connection string or key

| Context | Where settings are defined |
|---------|---------------------------|
| Running in Azure | Application settings |
| Local development | `local.settings.json` |

---

### Identity-Based Connections
- Some connections use a **managed identity** instead of a secret (support depends on the extension)
- When hosted in Azure Functions: uses **managed identity** by default
  - **System-assigned identity** used by default
  - **User-assigned identity** can be specified via `credential` and `clientID` properties
  - Configuring user-assigned identity with a resource ID is **not supported**
- When running locally: uses your **developer identity** (customizable)

> **Note:** Apps on **Consumption or Elastic Premium** plans use `WEBSITE_AZUREFILESCONNECTIONSTRING` and `WEBSITE_CONTENTSHARE` for Azure Files — Azure Files **does not support managed identity** for file share access.

---

### Grant Permission to the Identity
- Identities must have permissions for the intended actions
- Assign permissions via:
  - **Azure RBAC** (role assignment), or
  - **Access policy** (depending on the target service)
- Follow **principle of least privilege** — grant only required permissions

---

