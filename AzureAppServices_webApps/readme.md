## Learning objectives


- Describe Azure App Service key components and value.
- Explain how Azure App Service manages authentication and authorization.
- Identify methods to control inbound and outbound traffic to your web app.
- Deploy an app to App Service using Azure CLI commands.

## Azure App Service Overview

Azure App Service is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. Applications run and scale with ease on both Windows and Linux-based environments across multiple programming languages and frameworks.

### Key Features

#### Built-in Auto Scale Support
- **Scale Up/Down**: Adjust resources (CPU cores, RAM) of the underlying machine
- **Scale Out/In**: Increase or decrease the number of machine instances running your web app
- Scaling capabilities are built directly into the Azure App Service platform

#### Container Support
- Deploy and run containerized web apps on Windows and Linux
- Pull container images from Azure Container Registry or Docker Hub
- Support for multi-container apps, Windows containers, and Docker Compose orchestration

#### Continuous Integration/Deployment
- Out-of-the-box CI/CD integration with:
  - Azure DevOps Services
  - GitHub
  - Bitbucket
  - FTP
  - Local Git repository
- Auto-sync code and future changes into the web app
- CI/CD support for containerized apps using Azure Container Registry or Docker Hub

#### Deployment Slots
- Available in Standard App Service Plan tier or higher
- Use separate deployment slots instead of production slot
- Live apps with their own host names
- Swap app content and configurations between slots, including production

### App Service on Linux

#### Supported Features
- Native Linux hosting for supported application stacks
- Custom Linux containers (Web App for Containers)
- Language-specific built-in images for: .NET Core, Java (Tomcat, JBoss EAP, Java SE), Node.js, Python, PHP
- Deploy custom containers for unsupported runtimes

#### Check Supported Runtimes
```bash
az webapp list-runtimes --os-type linux
```

#### Limitations
- Not supported on Shared pricing tier
- Azure portal shows only currently working Linux features
- Built-in images use Azure Storage-backed volume (higher disk latency)
- Apps with heavy read-only access may benefit from custom containers

### App Service Environment
- Fully isolated and dedicated environment for App Service apps
- Improved security at high scale
- Dedicated compute resources for single customer (vs. shared infrastructure in standard App Service)
- Provides enhanced isolation and security features

## Azure App Service Plans

An App Service plan defines the compute resources for web apps to run. Multiple apps can share the same App Service plan and its resources.

### Plan Configuration
Each App Service plan defines:
- **Operating System**: Windows or Linux
- **Region**: Geographic location (West US, East US, etc.)
- **VM Instances**: Number and size (Small, Medium, Large)
- **Pricing Tier**: Determines features and cost

### Pricing Tiers

#### Shared Compute
- **Free/Shared**: Apps run on shared Azure VMs with other customers
- CPU quotas allocated per app
- Cannot scale out
- Development/testing only

#### Dedicated Compute
- **Basic, Standard, Premium (V2/V3)**: Apps run on dedicated VMs
- Only apps in same plan share resources
- Higher tiers = more VM instances for scale-out

#### Isolated
- **Isolated/IsolatedV2**: Dedicated VMs on dedicated Virtual Networks
- Network + compute isolation
- Maximum scale-out capabilities

### Scaling Behavior
- **Free/Shared**: Receives CPU minutes, no scale-out
- **Other tiers**: Apps run on all VM instances in the plan
- Multiple apps in same plan share all VM instances
- Deployment slots, logs, backups, WebJobs use same VM resources

### When to Create Separate Plans
Isolate apps into new App Service plans when:
- App is resource-intensive
- Need independent scaling from other apps
- Require resources in different geographical region

### Key Points
- App Service plan is the **scale unit** for apps
- All apps in plan scale together with autoscaling
- Can scale up/down by changing pricing tier
- Multiple apps in one plan can save money but share resources

## App Service Deployment

App Service supports both automated and manual deployment methods to meet diverse development team requirements.

### Automated Deployment (Continuous Deployment)
Fast, repetitive deployment with minimal end-user impact.

**Supported Sources:**
- **Azure DevOps Services**: Build, test, and deploy pipeline in the cloud
- **GitHub**: Auto-deploy from production branch changes
- **Bitbucket**: Similar configuration to GitHub

### Manual Deployment Options
- **Git**: Use App Service Git URL as remote repository
- **Azure CLI**: `az webapp up` command (can create new web apps)
- **Zip Deploy**: Upload ZIP file using curl or HTTP utilities
- **FTP/FTPS**: Traditional file transfer methods

### Deployment Best Practices

#### Use Deployment Slots
- Available with Standard App Service Plan or higher
- Deploy to staging environment, then swap with production
- Swap operation warms worker instances to match production scale
- **Eliminates downtime**

#### Continuous Deployment Strategy
- Deploy testing/QA/staging branches to separate staging slots
- Enables stakeholder assessment and testing
- Each branch continuously deployed to its own slot

#### Container Deployment
**Process:**
1. **Build & Tag**: Tag images with git commit ID, timestamp, or identifiable info
2. **Push**: Upload tagged image to container registry (avoid "latest" tag)
3. **Update Slot**: Update deployment slot with new image tag (triggers auto-restart)

**Benefits:**
- Deploy to staging slot first, then swap to production
- Prevents downtime during container updates

### Sidecar Containers
- Add up to **9 sidecar containers** per sidecar-enabled app
- Deploy additional services without tight coupling to main container
- **Use cases**: Monitoring, logging, configuration, networking services
- Managed through Deployment Center in app management page

### Key Takeaways
- Use deployment slots to eliminate downtime
- Avoid "latest" tags for containers (use identifiable tags)
- Continuous deployment enables faster, safer releases
- Sidecar containers provide modular service architecture


