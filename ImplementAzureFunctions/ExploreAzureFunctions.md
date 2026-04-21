# Explore Azure Functions

## Learning Objectives
- Explain functional differences between Azure Functions, Azure Logic Apps, and WebJobs
- Describe Azure Functions hosting plan options
- Describe how Azure Functions scale to meet business needs

---

## What is Azure Functions?
- **Serverless compute service** on Microsoft Azure — write only the code you need, no server management
- Ideal for: web APIs, reacting to database changes, processing IoT streams, managing message queues
- Supports **triggers** (ways to start code execution) and **bindings** (simplify input/output data coding)

---

## Azure Functions vs. Azure Logic Apps

Both are serverless services that can create complex **orchestrations** (collections of functions/steps to accomplish a complex task).

| Topic | Azure Functions | Logic Apps |
|---|---|---|
| Development | Code-first (imperative) | Designer-first (declarative) |
| Connectivity | ~12 built-in binding types; custom bindings via code | Large connector library; Enterprise Integration Pack (B2B); custom connectors |
| Actions | Each activity is an Azure function | Large collection of ready-made actions |
| Monitoring | Azure Application Insights | Azure portal, Azure Monitor logs |
| Management | REST API, Visual Studio | Azure portal, REST API, PowerShell, Visual Studio |
| Execution context | Azure or locally | Azure, locally, or on-premises |

**Key distinction:** Functions = code-first orchestrations (Durable Functions extension); Logic Apps = GUI/config-based orchestrations.

---

## Azure Functions vs. WebJobs (with WebJobs SDK)

Both are code-first integration services built on Azure App Service, sharing source control integration, authentication, and Application Insights monitoring.

> Azure Functions is **built on the WebJobs SDK**, so it shares many event triggers and Azure service connections.

| Factor | Azure Functions | WebJobs with WebJobs SDK |
|---|---|---|
| Serverless / auto-scaling | Yes | No |
| Develop & test in browser | Yes | No |
| Pay-per-use pricing | Yes | No |
| Logic Apps integration | Yes | No |
| Trigger events | Timer, Storage queues/blobs, Service Bus, Cosmos DB, Event Hubs, HTTP/WebHook, Event Grid | Timer, Storage queues/blobs, Service Bus, Cosmos DB, Event Hubs, File system |

**Conclusion:** Azure Functions provides more developer productivity, language options, development environments, Azure service integrations, and flexible pricing. It is the **preferred choice** for most scenarios over WebJobs.

---

## Hosting Plans

The hosting plan determines: scaling behavior, available resources per instance, advanced features (VNet, Linux containers), and cost.

| Hosting Option | Service | Container Support |
|---|---|---|
| Consumption plan | Azure Functions | None |
| Flex Consumption plan | Azure Functions | None |
| Premium plan | Azure Functions | Linux |
| Dedicated plan | Azure Functions | Linux |
| Container Apps | Azure Container Apps | Linux |

### Plan Summaries

**Consumption plan** (default)
- Pay-as-you-go — billed only when functions run
- Instances dynamically added/removed based on incoming events
- Simple and cost-effective for sporadic workloads

**Flex Consumption plan**
- Pay-as-you-go with per-function scaling (more deterministic scaling decisions)
- Supports **pre-provisioned (always ready) instances** to reduce cold starts
- Scales automatically based on per-instance concurrency + incoming events

**Premium plan** — choose when:
- Functions run continuously or near-continuously
- Need prewarmed workers (no cold start delay)
- Need Virtual Network connectivity
- Need more CPU/memory than Consumption offers
- Execution time exceeds Consumption plan's maximum
- Want a custom Linux image

**Dedicated plan (App Service plan)** — choose when:
- Need fully predictable billing or manual scaling
- Running multiple web apps and function apps on the same plan
- Need larger compute sizes or full isolation via App Service Environment (ASE)
- Long-running scenarios where Durable Functions can't be used

**Container Apps** — choose when:
- Need to package custom libraries with function code
- Migrating on-premises/legacy apps to cloud-native microservices
- Want to avoid managing Kubernetes clusters
- Need dedicated CPU compute resources

---

## Function App Timeout Duration

Configured via `functionTimeout` property in `host.json`. Applies to function execution time after the trigger fires.

| Plan | Default | Maximum |
|---|---|---|
| Flex Consumption | 30 min | Unbounded |
| Premium | 30 min | Unbounded |
| Dedicated | 30 min | Unbounded (requires Always On) |
| Container Apps | 30 min | Unbounded |
| Consumption | 5 min | **10 min** |

> **Important:** HTTP-triggered functions have a hard cap of **230 seconds** to respond, due to Azure Load Balancer's idle timeout. For longer processing, use **Durable Functions async pattern** or return an immediate response and defer work.

---

## Scaling Azure Functions

Max instances are per-function-app (Consumption) or per-plan (Premium/Dedicated).

| Plan | Scale Behavior | Max Instances |
|---|---|---|
| Consumption | Event-driven; auto-scales CPU & memory | Windows: 200 / Linux: 100 |
| Flex Consumption | Per-function event-driven scaling | Limited by total memory across region |
| Premium | Event-driven auto-scale | Windows: 100 / Linux: 20–100 |
| Dedicated | Manual or autoscale | 10–30 (up to 100 on ASE) |
| Container Apps | Event-driven auto-scale | 10–300 (subject to cores quota) |

> **Note:** During scale-out, Linux Consumption plan apps are limited to **500 new instances per subscription per hour**.
