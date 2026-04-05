# Azure Blob Storage Client Library

## Core Points

- Use Azure Storage client library for .NET version `12.x` for new applications.
- Authentication commonly uses `DefaultAzureCredential` with a Microsoft Entra security principal.
- The principal must have an Azure RBAC role that grants blob data access.
- SDK access usually starts by creating a client object with a storage endpoint URI and credential.

## Main Classes

| Class | Purpose |
| --- | --- |
| `BlobServiceClient` | Works at the storage account level. Manage service resources and containers. |
| `BlobContainerClient` | Works at the container level. Create/delete containers and manage blobs inside them. |
| `BlobClient` | Works at the individual blob level. Read, upload, delete, and manage one blob. |
| `BlobClientOptions` | Configures client behavior for Blob Storage connections. |
| `BlobUriBuilder` | Helps build or modify Blob Storage resource URIs. |

## Packages

- `Azure.Storage.Blobs`: Primary client types for service, container, and blob operations.
- `Azure.Storage.Blobs.Specialized`: Specialized blob operations, such as block blob operations.
- `Azure.Storage.Blobs.Models`: Supporting models, enums, and utility types.

## Client Creation Pattern

### 1. Create `BlobServiceClient`

Use when starting from the storage account level.

```csharp
BlobServiceClient client = new(
	new Uri($"https://{accountName}.blob.core.windows.net"),
	new DefaultAzureCredential());
```

### 2. Create `BlobContainerClient`

Use a `BlobServiceClient` when you already have the service client.

```csharp
BlobContainerClient client = blobServiceClient.GetBlobContainerClient(containerName);
```

You can also create it directly if you only need one container.

```csharp
BlobContainerClient client = new(
	new Uri($"https://{accountName}.blob.core.windows.net/{containerName}"),
	new DefaultAzureCredential(),
	clientOptions);
```

### 3. Create `BlobClient`

Use when working with a specific blob.

```csharp
BlobClient client =
	blobServiceClient.GetBlobContainerClient(containerName).GetBlobClient(blobName);
```

## Container Properties vs Metadata

### System Properties

- Built into Blob Storage resources.
- Some are read-only, some can be set.
- Many map to standard HTTP headers.
- The .NET client library handles these headers for you.

### User-Defined Metadata

- Stored as name/value pairs.
- Used for your own labeling or categorization.
- Does not change resource behavior.
- Metadata names:
  - must be valid HTTP header names
  - must be valid C# identifiers
  - must contain ASCII characters only
  - are case-insensitive
- Metadata values with non-ASCII content should be Base64-encoded or URL-encoded.

## Read Container Properties

Methods:

- `GetProperties`
- `GetPropertiesAsync`

Common values returned:

- `PublicAccess`
- `LastModified`
- `Metadata`

## Set Container Metadata

Methods:

- `SetMetadata`
- `SetMetadataAsync`

Typical pattern:

```csharp
IDictionary<string, string> metadata = new Dictionary<string, string>
{
	{ "docType", "textDocuments" },
	{ "category", "guidance" }
};

await container.SetMetadataAsync(metadata);
```

Important behavior:

- Metadata is written as a full replacement.
- Partial metadata updates are not supported.
- Setting metadata overwrites existing metadata.

## Read Container Metadata

Metadata is retrieved through container properties.

```csharp
var properties = await container.GetPropertiesAsync();
var metadata = properties.Value.Metadata;
```

## REST Metadata Rules

### Metadata Header Format

```http
x-ms-meta-name: string-value
```

### Rules

- Metadata names follow C# identifier naming rules.
- Names are case-insensitive.
- If duplicate metadata names are submitted, Blob service returns `400 Bad Request`.
- Total metadata size limit is up to `8 KB`.

## REST Operations for Metadata

### Retrieve metadata

- Container:

```http
GET/HEAD https://myaccount.blob.core.windows.net/mycontainer?restype=container&comp=metadata
```

- Blob:

```http
GET/HEAD https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=metadata
```

### Set metadata

- Container:

```http
PUT https://myaccount.blob.core.windows.net/mycontainer?comp=metadata&restype=container
```

- Blob:

```http
PUT https://myaccount.blob.core.windows.net/mycontainer/myblob?comp=metadata
```

Important behavior:

- `PUT` metadata replaces existing metadata.
- `PUT` with no metadata headers clears all existing metadata.

## Standard HTTP Properties

### Container properties

- `ETag`
- `Last-Modified`

### Blob properties

- `ETag`
- `Last-Modified`
- `Content-Length`
- `Content-Type`
- `Content-MD5`
- `Content-Encoding`
- `Content-Language`
- `Cache-Control`
- `Origin`
- `Range`

## Exam-Focused Takeaways

- `BlobServiceClient` = account scope.
- `BlobContainerClient` = container scope.
- `BlobClient` = blob scope.
- `DefaultAzureCredential` is the recommended authentication pattern in modern SDK usage.
- Metadata is custom, case-insensitive, and overwritten as a whole.
- Properties are standard system-defined HTTP header values.
- `GetPropertiesAsync` can return both properties and metadata.
