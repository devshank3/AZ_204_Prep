## Configuration of App settings, 

App settings are variables passed as environment variables to the application code

### LO

- Application settings that are bound to deployment slots 
- Options installing SSL/TLS certificate 
- Diagnostic logging for monitoring and debugging 
- Virtual app to directory mappings

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



