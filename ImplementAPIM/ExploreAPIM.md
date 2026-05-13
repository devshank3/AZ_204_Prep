# Explore Azure API Management (APIM)

## Learning Objectives

- Describe the components and functions of the API Management service
- Explain how API gateways help manage calls to APIs
- Secure access to APIs using subscriptions and certificates
- Import and configure an API

---

## APIM Components

Azure APIM consists of three main components, all Azure-hosted and fully managed:

### 1. API Gateway

The endpoint that handles all API traffic. Acts as a **reverse proxy** between clients and services.

**Core functions:**

- **Routes** API calls to appropriate backends
- **Verifies** API keys and credentials
- **Enforces** usage quotas and rate limits
- **Transforms** requests/responses via policy statements
- **Caches** responses to reduce latency and backend load
- **Emits** logs, metrics, and traces for monitoring

**Why use a gateway?** Without one, clients talk directly to backends, causing:

- Complex client code (tracking multiple endpoints, handling failures)
- Tight coupling between client and backend (harder to refactor)
- Single operations may require calls to multiple services
- Every public service must independently handle auth, SSL, rate limiting
- Public endpoints increase the attack surface

A gateway **decouples clients from services** and handles cross-cutting concerns centrally.

**Gateway types:**

| Type | Description |
|---|---|
| **Managed** | Default gateway deployed in Azure for every APIM instance. All API traffic flows through Azure, regardless of where backends are hosted. |
| **Self-hosted** | Optional containerized version for **hybrid/multicloud** scenarios. Runs where backends are hosted (on-prem or other clouds) while managed from a single APIM instance in Azure. |

### 2. Management Plane

The admin interface to configure your API program:

- Provision and configure APIM settings
- Define or import API schemas
- Package APIs into **products**
- Set up **policies** (quotas, transformations)
- View analytics

### 3. Developer Portal

Auto-generated, customizable website for API consumers:

- Read API documentation
- Test APIs via interactive console
- Create accounts and get API keys
- View usage analytics
- Download API definitions

---

## Key Concepts

### Products

- Products **surface APIs to developers** (one or more APIs per product)
- **Open products** — no subscription needed
- **Protected products** — require subscription before use
- Subscription approval can be admin-approved or auto-approved

### Groups

Manage visibility of products to developers:

| Group | Role |
|---|---|
| **Administrators** | Manage APIM instances, create APIs/operations/products |
| **Developers** | Authenticated portal users who build apps using APIs |
| **Guests** | Unauthenticated users with read-only access (view, not call) |

- Admins can also create **custom groups** or use **external groups** from Microsoft Entra ID

### Developers

- User accounts in an APIM instance
- Can be created by admins, invited, or self-sign-up via Developer Portal
- Belong to one or more groups; subscribe to products for API access

### Policies

Statements executed sequentially on API request or response:

- **Common policies:** XML-to-JSON conversion, rate limiting
- **Policy expressions** can be used as attribute values or text values
- **Scopes** (from broadest to narrowest):
  1. **Global** — all APIs
  2. **Product** — all APIs in a product
  3. **API** — all operations in a specific API
  4. **Operation** — a single API operation

---

## Quick Recall

| Concept | Key Point |
|---|---|
| API Gateway | Entry point — routes, secures, transforms, caches |
| Management Plane | Admin config — schemas, products, policies, analytics |
| Developer Portal | Consumer-facing — docs, test console, keys |
| Products | Group APIs for developer consumption (open vs protected) |
| Groups | Control product visibility (Admins, Developers, Guests) |
| Policies | Sequential rules on requests/responses at 4 scope levels |
