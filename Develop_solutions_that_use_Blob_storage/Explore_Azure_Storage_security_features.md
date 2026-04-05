# Explore Azure Storage Security Features

## Core Security Feature

- Azure Storage uses service-side encryption (SSE) to encrypt data at rest automatically.
- Encryption is enabled by default for all storage accounts and cannot be disabled.
- No code changes are required to use it.

## Data at Rest Encryption

- Uses 256-bit AES encryption.
- FIPS 140-2 compliant.
- Encryption and decryption happen transparently.
- No extra cost.

## What Gets Encrypted

- Block blobs
- Append blobs
- Page blobs
- Archive tier blobs
- Azure Files
- Queues
- Tables
- Managed disks / storage disks
- Object metadata

## Coverage Notes

- Works across all performance tiers.
- Works across all access tiers.
- Works across all deployment models.
- Works with all redundancy options.
- If geo-replication is enabled, data in both primary and secondary regions is encrypted.

## Encryption Key Management Options

### Microsoft-Managed Keys

- Default option for new storage accounts.
- Microsoft handles key storage and rotation.
- Supported for all Azure Storage services.

### Customer-Managed Keys (CMK)

- Customer controls the key.
- Keys must be stored in Azure Key Vault or Azure Key Vault Managed HSM.
- Supported for Blob Storage and Azure Files.
- Customer is responsible for key rotation.

### Customer-Provided Keys (CPK)

- Customer supplies the key in a blob read/write request.
- Provides per-request control over encryption.
- Supported only for Blob Storage.
- Customer manages key storage and rotation.

## Key Option Comparison

| Option | Supported Services | Key Storage | Rotation Responsibility | Control |
|---|---|---|---|---|
| Microsoft-managed | All | Microsoft key store | Microsoft | Microsoft |
| Customer-managed | Blob Storage, Azure Files | Azure Key Vault / Managed HSM | Customer | Customer |
| Customer-provided | Blob Storage only | Customer-owned key store | Customer | Customer |

## Client-Side Encryption

- Client-side encryption encrypts data before upload and decrypts after download.
- Used when encryption must happen on the client instead of only in Azure.

### Supported SDKs

- Blob Storage: .NET, Java, Python
- Queue Storage: .NET, Python

### Client-Side Encryption Versions

- Version 2: AES-GCM
	- Supported by Blob Storage and Queue Storage SDKs
- Version 1: AES-CBC
	- Supported by Blob Storage, Queue Storage, and Table Storage SDKs

## Quick Memory Aid

- SSE = default, automatic, at rest
- AES-256 + FIPS 140-2
- CMK = Key Vault / Managed HSM
- CPK = per-request key for Blob Storage
- Client-side encryption = encrypt before upload
