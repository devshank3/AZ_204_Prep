# Discover Azure Blob Storage Resource Types

## Core Resource Types

Azure Blob Storage has 3 main resource types:

1. Storage account
2. Container
3. Blob

## 1. Storage Account

- A storage account provides the unique namespace for all stored data.
- Every object stored in Azure Storage uses the storage account name as part of its address.
- The account name plus the Blob service endpoint creates the base URL.

Example:

```text
https://mystorageaccount.blob.core.windows.net
```

## 2. Container

- A container groups blobs, similar to a folder or directory.
- A storage account can contain unlimited containers.
- A container can contain unlimited blobs.

### Container Naming Rules

- Must be 3 to 63 characters long.
- Must start with a letter or number.
- Can contain only lowercase letters, numbers, and hyphens (`-`).
- Cannot contain consecutive hyphens.
- Must be a valid DNS name.

Example container URI:

```text
https://myaccount.blob.core.windows.net/mycontainer
```

## 3. Blob

- A blob is the actual data stored inside a container.
- Blob URI format:

```text
https://myaccount.blob.core.windows.net/mycontainer/myblob
```

Virtual directory-style path:

```text
https://myaccount.blob.core.windows.net/mycontainer/myvirtualdirectory/myblob
```

## Blob Types

### Block Blob

- Stores text and binary data.
- Made of blocks that can be managed independently.
- Best for general-purpose file storage.
- Maximum size is about 190.7 TiB.

### Append Blob

- Similar to block blobs but optimized for append operations.
- Best for logging scenarios, such as VM log data.

### Page Blob

- Designed for random read/write access.
- Supports files up to 8 TB.
- Used for VHDs and Azure VM disks.

## Quick Memory Aid

- Storage account = namespace
- Container = grouping of blobs
- Blob = actual file/data
- Block blob = general storage
- Append blob = logging
- Page blob = disks / random access
