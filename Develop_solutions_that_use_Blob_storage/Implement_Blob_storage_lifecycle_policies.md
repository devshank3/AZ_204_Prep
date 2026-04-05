# Implement Blob Storage Lifecycle Policies

## Ways to Manage Policies

You can add, edit, or remove lifecycle policies by using:

- Azure portal
- Azure PowerShell
- Azure CLI
- REST APIs

## Azure Portal

Two portal views are available:

- List view
- Code view

### Code View Steps

1. Open the storage account in Azure portal.
2. Under Data management, select Lifecycle Management.
3. Open the Code View tab.
4. Define or update the lifecycle policy in JSON.

## Sample Policy

This example moves block blobs whose name starts with `log` in `sample-container` to the Cool tier after 30 days since last modification.

```json
{
  "rules": [
    {
      "enabled": true,
      "name": "move-to-cool",
      "type": "Lifecycle",
      "definition": {
        "actions": {
          "baseBlob": {
            "tierToCool": {
              "daysAfterModificationGreaterThan": 30
            }
          }
        },
        "filters": {
          "blobTypes": [
            "blockBlob"
          ],
          "prefixMatch": [
            "sample-container/log"
          ]
        }
      }
    }
  ]
}
```

## Azure CLI

- Write the lifecycle policy to a JSON file.
- Use Azure CLI to apply it to the storage account.

```bash
az storage account management-policy create \
    --account-name <storage-account> \
    --policy @policy.json \
    --resource-group <resource-group>
```

## Important Note

- Lifecycle policies must be read or written as a full document.
- Partial updates are not supported.

## Quick Memory Aid

- Portal: Lifecycle Management -> Code View -> JSON
- CLI: `management-policy create`
- Policy file is passed with `@policy.json`
- Update requires full policy, not partial changes