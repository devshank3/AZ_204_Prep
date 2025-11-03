# Azure App Service Lab Guide

## Overview
This lab covers creating and managing Azure App Service resources including App Service Plans, Web Apps, deployment slots, and monitoring capabilities.

---

## Lab 1: Creating an Azure App Service Plan

### Introduction
Azure App Service is a PaaS offering for building, deploying, and scaling Web, API, Mobile, and Function apps. It supports both Windows and Linux platforms with multiple languages (.NET, Java, Node.js, Python, PHP, Ruby, Docker).

### App Service Plan Tiers

| Tier | Description |
|------|-------------|
| **Free** | Windows only, limited apps |
| **Shared** | Windows only, custom domains support |
| **Basic** | Unlimited apps, up to 3 instances with load balancing |
| **Standard** | Production-ready, up to 10 instances, autoscaling, VNet integration |
| **Premium** | Up to 20 instances, additional storage |
| **Isolated** | Up to 100 instances, dedicated VNet, private access |

### Steps
1. Search for **App Service Plans** in Azure Portal
2. Click **+ Create**
3. Configure:
   - Resource Group: Select existing (cal-123)
   - Name: `ca-lab-plan`
   - OS: Windows
   - Location: West US
4. Select **S1 tier** from pricing options
5. Click **Review + Create** → **Create**
6. Navigate to resource after creation

### Key Features
- Monitor Apps/Slots usage
- View CPU, Memory, Data In/Out metrics
- Configure Scale up/Scale out options
- Set up Alerts for metric thresholds
- Manage Networking and File system storage

---

## Lab 2: Creating a Web App in Azure

### Introduction
Azure Web Apps are website/application instances hosted in App Service. They're DevOps-ready with support for continuous deployment from GitHub, BitBucket, VSTS, and more.

### Steps
1. Search for **App Services** in Azure Portal
2. Click **+ Create** → **+ Web App**
3. Configure:
   - Resource Group: Select lab resource group
   - Name: `ca-lab-app-######` (unique digits)
   - Secure unique default hostname: Deselect
   - Publish: Code
   - Runtime: .NET 8.x (LTS)
   - OS: Windows
   - Region: West US
   - App Service Plan: `ca-lab-plan`
4. Monitoring + secure section:
   - Application Insights: No
5. Click **Review + create** → **Create**
6. Navigate to resource and click **Browse**

### Notes
- Linux plans cost less than Windows but have fewer features
- Docker apps run on Linux plans
- Production slot is the default deployment slot

---

## Lab 3: Creating a Staging Deployment Slot

### Introduction
Deployment slots provide separate instances with unique hostnames for:
- Testing and staging workflows
- Zero-downtime production swaps
- Easy rollback capabilities
- Separate configurations per slot

### Steps
1. Navigate to App Service → **Deployment slots**
2. Click **+ Add Slot**
3. Configure:
   - Name: `staging`
   - Clone settings from: Do not clone settings
4. Click **Add**
5. Click the staging slot to view its blade
6. Click **Browse** to view default app

### URL Format
- Production: `ca-lab-app-######.azurewebsites.net`
- Staging: `ca-lab-app-######-staging.azurewebsites.net`

---

## Lab 4: Deploying Web Apps Using Deployment Slots

### Introduction
Deployment slot swaps enable pre-warmed deployments and easy rollbacks. 

### Swap Types

| Type | Description |
|------|-------------|
| **Auto Swap** | Automatic swap after deployment |
| **Swap** | Manual swap operation |
| **Swap with Preview** | Preview changes before completing swap |

### Sticky vs Swappable Settings

**Do NOT swap (sticky):**
- SSL certificates
- Custom domain names
- Scale settings

**DO swap:**
- Monitoring/diagnostic settings
- Framework versions
- App settings (unless marked as slot setting)
- Connection strings (unless marked as slot setting)

### Deployment Steps
1. Download the pre-built application zip file
2. Navigate to staging slot → **Advanced Tools**
3. Click **Go** to open Kudu
4. Click **Tools** → **Zip Push Deploy**
5. Drag and drop the zip file to deploy
6. Wait for "Deployment successful" message

### Configure Slot Settings
1. Open staging slot's **Environment variables**
2. Add app setting:
   - Name: `test-setting`
   - Value: `blue`
   - Deployment Slot Setting: ✓ Checked
3. Click **Apply** → **Confirm**

### Perform Swap with Preview
1. Navigate to **Deployment Slots** → **Swap**
2. Configure:
   - Source: `ca-lab-app-###(staging)`
   - Destination: `ca-lab-app-###`
   - Perform swap with preview: ✓ Checked
3. Click **Swap** to preview
4. Review changes
5. Click **Complete swap**

---

## Lab 5: Monitoring Azure Web Apps

### Introduction
Azure provides multiple monitoring tools for Web Apps through Azure Monitor.

### Monitoring Tools

#### 1. Metrics
Server-level information tracking:
- Failed requests
- Average response time
- Data in/out
- HTTP status codes
- Thread count
- Connections

**Retention Periods:**
- Per-minute: 30 hours
- Per-hour: 30 days
- Per-day: 30 days

#### 2. Diagnostic Logs
Application and web server logging with configurable detail levels.

**Log Types:**
- Application logs (custom logging)
- Web server logs (IIS logs)
- Detailed error messages
- Failed request tracing

**Storage Locations:**
- File System (limited space)
- Azure Storage (production recommended)

#### 3. Resource Health
Monitors Azure service issues affecting your Web App:
- Service outages
- Hardware issues
- SLA violation tracking
- 4-week health history

#### 4. Service Health
Reports broad Azure service outages (global scope).

### Monitoring Steps

#### View Metrics
1. Navigate to Web App **Overview** → **Monitoring** tab
2. Click **See all metrics**
3. Add metrics: Connections, HTTP 2xx, HTTP Server Errors, Thread Count
4. Configure chart title, type, and time range
5. Save to dashboard or create alerts

#### Enable Diagnostic Logs
1. Navigate to **Monitoring** → **App Service Logs**
2. Configure:
   - Application Logging (Filesystem): On
   - Level: Verbose
   - Web server logging: File System
   - Quota (MB): 35
   - Retention Period (Days): 0 (indefinite)
3. Click **Save**

#### View Log Stream
1. Click **Log stream** in sidebar
2. Refresh Web App to generate activity
3. Switch between Application and Web server logs
4. Logs appear within ~1 minute

**Log Locations:**
- Application logs: `D:\home\LogFiles\Application`
- Web server logs: `D:\home\LogFiles\http\RawLogs`

#### Check Resource Health
1. Navigate to **Support + Troubleshooting** → **Resource health**
2. Review current status
3. Check 4-week health history
4. Look for error/warning icons

### Performance Tips
- Enable **Always On** to prevent de-allocation delays
- Use alerts for proactive monitoring
- Store logs in Azure Storage for production
- Monitor metrics to determine when to scale

---

## Key Takeaways

1. **App Service Plans** are containers for multiple apps with shared resources
2. **Deployment Slots** enable zero-downtime deployments and easy rollbacks
3. **Slot Settings** allow environment-specific configurations
4. **Swap with Preview** reduces deployment risks
5. **Monitoring** includes Metrics, Diagnostic Logs, and Resource Health
6. **Kudu** (Advanced Tools) provides low-level deployment and diagnostic capabilities

---

## Additional Resources
- [App Service Plan Features](https://azure.microsoft.com/pricing/details/app-service/)
- [Linux vs Windows Plans Comparison](https://docs.microsoft.com/azure/app-service/)
- [Kudu Documentation](https://github.com/projectkudu/kudu/wiki)

