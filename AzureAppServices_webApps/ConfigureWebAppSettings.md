## Configuration of App settings

App settings are variables passed as environment variables to the application code

### LO

- Application settings that are bound to deployment slots 
- Options installing SSL/TLS certificate 
- Diagnostic logging for monitoring and debugging 
- Virtual app to directory mappings

---

### Configure Application Settings

#### App Settings Overview
- **Environment Variables**: App settings are passed as environment variables to application code
- **Linux/Containers**: Passed using `--env` flag to set environment variables in the container
- **Injection**: Variables are injected into app environment at startup
- **Restart Trigger**: Adding, removing, or editing app settings triggers an app restart
- **Encryption**: App settings are always encrypted when stored (encrypted-at-rest)

#### Naming Conventions
- **Allowed Characters**: Letters, numbers (0-9), periods ("."), and underscores ("_")
- **Linux Apps**: Replace `:` with `__` (double underscore) in nested JSON structures
  - Example: `ApplicationInsights:InstrumentationKey` → `ApplicationInsights__InstrumentationKey`
- **Periods**: Replaced with `_` (single underscore) in app setting names

#### Framework-Specific Behavior
- **ASP.NET/ASP.NET Core**: App Service values override `Web.config` or `appsettings.json`
- **Development vs Production**: Keep dev settings in config files, production secrets in App Service
- **Code Compatibility**: Same code works for local debugging and Azure deployment

#### Managing Settings
- **Navigation**: App management page → Environment variables → Application settings
- **Adding Settings**: Use `+ Add` button, specify slot-specific settings if using deployment slots
- **Bulk Editing**: Use Advanced edit button with JSON format:

```json
[
  {
    "name": "<key-1>",
    "value": "<value-1>",
    "slotSetting": false
  }
]
```

#### Connection Strings
- **ASP.NET/Core**: Override `<connectionStrings>` in Web.config
- **Other Languages**: Better to use app settings due to special formatting requirements
- **Database Backup**: Some Azure databases only backed up if configured as connection strings
- **JSON Format**:

```json
[
  {
    "name": "name-1",
    "value": "conn-string-1",
    "type": "SQLServer",
    "slotSetting": false
  }
]
```

#### Runtime Environment Variable Prefixes
- **SQLServer**: `SQLCONNSTR_`
- **MySQL**: `MYSQLCONNSTR_`
- **SQLAzure**: `SQLAZURECONNSTR_`
- **PostgreSQL**: `POSTGRESQLCONNSTR_`
- **Custom**: `CUSTOMCONNSTR_`
- **Redis Cache**: `REDISCACHECONNSTR_`
- **Service Bus**: `SERVICEBUSCONNSTR_`
- **Event Hub**: `EVENTHUBCONNSTR_`
- **Document DB**: `DOCDBCONNSTR_`
- **Notification Hub**: `NOTIFICATIONHUBCONNSTR_`

#### Custom Container Configuration
- **Azure CLI**: 
  ```bash
  az webapp config appsettings set --resource-group <group-name> --name <app-name> --settings key1=value1
  ```
- **PowerShell**:
  ```powershell
  Set-AzWebApp -ResourceGroupName <group-name> -Name <app-name> -AppSettings @{"DB_HOST"="server.com"}
  ```
- **Verification**: Check environment variables at `https://<app-name>.scm.azurewebsites.net/Env`

#### Special Notes
- **.NET PostgreSQL**: Set connection string type to "Custom" as workaround for known issue
- **Slot Settings**: Can be configured to stick to specific deployment slots
- **Apply Changes**: Always select "Apply" to save changes in Environment variables page

---

### Configure General Settings

#### Overview
General settings are configured in **Configuration > General settings** section. Some settings require higher pricing tiers.

#### Stack Settings
- **Software Stack**: Configure programming language and SDK versions
- **Linux/Container Apps**: Optional startup command or file configuration
- **Platform Support**: Language-specific runtime environments

#### Platform Settings

**Basic Platform Configuration:**
- **Platform Bitness**: 32-bit or 64-bit (Windows apps only)
- **FTP State**: Allow FTPS only or disable FTP completely
- **HTTP Version**: Set to 2.0 for HTTPS/2 protocol support
- **Web Sockets**: Enable for ASP.NET SignalR or socket.io applications

**Performance & Availability:**
- **Always On**: Keeps app loaded without traffic (prevents 20-min unload timeout)
  - Required for continuous WebJobs or CRON-triggered WebJobs
  - Sends GET request to app root every 5 minutes
  - Prevents high latency from cold starts
- **ARR Affinity**: Routes clients to same instance for session persistence
  - Set to "Off" for stateless applications

**Security Settings:**
- **HTTPS Only**: Redirects all HTTP traffic to HTTPS
- **Minimum TLS Version**: Set minimum required TLS encryption version
- **Incoming Client Certificates**: Enable mutual authentication with client certificates

**Development Tools:**
- **Remote Debugging**: Enable for ASP.NET, ASP.NET Core, or Node.js
  - Automatically disables after 48 hours
  - Available for development/testing scenarios

#### Key Notes
- **HTTP/2**: Requires HTTPS and custom DNS name for optimal browser support
- **Always On**: Essential for production apps to avoid cold start delays
- **Mutual Authentication**: TLS mutual auth restricts access through certificate validation
- **Pricing Dependency**: Advanced features may require higher App Service plan tiers

---

### Configure Path Mappings

#### Overview
Path mappings are configured in **Configuration > Path mappings** section. Options vary based on OS type (Windows vs Linux/containerized).

#### Windows Apps (Uncontainerized)

**Handler Mappings:**
- **Purpose**: Add custom script processors for specific file extensions
- **Configuration**:
  - **Extension**: File extension to handle (e.g., `*.php`, `handler.fcgi`)
  - **Script Processor**: Absolute path to script processor
  - **Arguments**: Optional command-line arguments
- **Root Reference**: Use `D:\home\site\wwwroot` for app's root directory

**Virtual Applications & Directories:**
- **Default Root**: Path `/` maps to `D:\home\site\wwwroot`
- **Custom Mapping**: Configure virtual directories with physical paths relative to website root
- **Web Application**: Uncheck "Directory" checkbox to mark virtual directory as web application
- **Use Cases**: Multiple applications in repository or different app root folder

#### Linux & Containerized Apps

**Custom Storage Mounting:**
- **Purpose**: Add external storage to containerized apps (includes all Linux apps and custom containers)
- **Configuration Options**:
  - **Basic**: For standard storage accounts without service endpoints/private endpoints
  - **Advanced**: For storage with service endpoints, private endpoints, or Azure Key Vault

**Storage Configuration:**
- **Name**: Display name for the mount
- **Storage Account**: Target storage account with desired container
- **Storage Types**:
  - **Azure Blobs**: Read-only access only
  - **Azure Files**: Full access (Windows containers support only Azure Files)
- **Mount Path**: Absolute path in container for storage mounting
- **Deployment Slots**: Option to apply settings to deployment slots

**Advanced Settings:**
- **Storage Container/Share Name**: Specific container or file share
- **Access Key**: Authentication key for advanced configurations
- **Slot Settings**: Can be configured to persist across deployment slots

#### Key Notes
- **OS-Specific**: Different configuration options for Windows vs Linux/containerized apps
- **Storage Limitations**: Azure Blobs are read-only; Windows containers limited to Azure Files
- **Path References**: Windows apps use `D:\home\site\wwwroot` as standard root reference
- **Custom Handlers**: Enable processing of non-standard file types through custom script processors

---

### Enable Diagnostic Logging

#### Overview
Built-in diagnostics assist with debugging App Service apps. Configure logging through **App Service logs** section.

#### Logging Types & Platforms

| Type | Platform | Location | Description |
|------|----------|----------|-------------|
| **Application Logging** | Windows, Linux | File system / Azure Storage blobs | Messages from application code with categories: Critical, Error, Warning, Info, Debug, Trace |
| **Web Server Logging** | Windows | File system / Azure Storage blobs | Raw HTTP request data in W3C extended log format |
| **Detailed Error Messages** | Windows | File system | HTML error pages for HTTP 400+ errors |
| **Failed Request Tracing** | Windows | File system | Detailed IIS component tracing for failed requests |
| **Deployment Logging** | Windows, Linux | File system | Automatic logging for deployment failures |

#### Application Logging Configuration

**Windows Apps:**
- **Navigation**: App → App Service logs
- **Options**: 
  - **Filesystem**: Temporary debugging (12-hour auto-disable)
  - **Blob Storage**: Long-term logging (requires storage container)
- **Log Levels**:
  - **Disabled**: None
  - **Error**: Error, Critical
  - **Warning**: Warning, Error, Critical
  - **Information**: Info, Warning, Error, Critical
  - **Verbose**: All categories (Trace, Debug, Info, Warning, Error, Critical)

**Linux/Container Apps:**
- **Option**: File System only
- **Quota**: Disk quota in MB
- **Retention**: Days to retain logs

#### Web Server Logging
- **Storage Options**: Blob storage or file system
- **Retention Period**: Configurable retention days
- **Platform**: Windows only

#### Code Implementation
- **ASP.NET**: Use `System.Diagnostics.Trace` class
  ```csharp
  System.Diagnostics.Trace.TraceError("Error message");
  ```
- **ASP.NET Core**: Uses `Microsoft.Extensions.Logging.AzureAppServices` provider
- **Python**: Use OpenCensus package for application diagnostics

#### Log Streaming
**Prerequisites**: Enable desired log type first

**Methods**:
- **Azure Portal**: Navigate to app → Log stream
- **Azure CLI**: 
  ```bash
  az webapp log tail --name appname --resource-group myResourceGroup
  ```
- **Local Console**: Install Azure CLI and sign in

#### Accessing Log Files

**Azure Storage Blobs**: Use Azure Storage client tools

**File System Logs**: Download ZIP file via browser
- **Windows Apps**: `https://<app-name>.scm.azurewebsites.net/api/dump`
- **Linux/Container Apps**: `https://<app-name>.scm.azurewebsites.net/api/logs/docker/zip`

#### Key Notes
- **Storage Keys**: Regenerating storage keys requires resetting logging configuration
- **Stream Buffering**: Some log types may show out-of-order events due to buffering
- **File Location**: Logs stored in `/LogFiles` directory (`d:/home/logfiles`)
- **Scaled Apps**: ZIP files contain logs for each instance
- **Security**: Detailed error pages shouldn't be sent to production clients



