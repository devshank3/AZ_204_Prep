# Explore Azure Blob Storage

## Quick Summary

Azure Blob Storage is Microsoft's object storage service for the cloud. It is designed to store massive amounts of unstructured data such as text, images, video, audio, logs, backups, and binary files.

## Learning Objectives

- Understand Azure Blob Storage features, storage account types, and access tiers
- Understand the relationship between storage accounts, containers, and blobs
- Understand Azure Storage security and encryption features

## What Azure Blob Storage Is Used For

- Serve images or documents directly to a browser
- Store files for distributed access
- Stream video and audio
- Write application or system log files
- Store backup, restore, disaster recovery, and archive data
- Store data for analytics workloads on-premises or in Azure

## How Blob Storage Is Accessed

- HTTP or HTTPS from anywhere
- Azure Storage REST API
- Azure PowerShell
- Azure CLI
- Azure Storage client libraries

## Storage Account Basics

- A storage account is the top-level container for Azure Storage services
- It provides a unique namespace for your data
- Blob data is accessed through this account over HTTP or HTTPS

## Storage Account Performance Levels

### Standard

- General-purpose v2 account
- Recommended for most Azure Storage scenarios
- Supports Blob Storage, Queue Storage, Table Storage, and Azure Files

### Premium

- Uses solid-state drives for higher performance
- Best for low latency and high transaction workloads
- Available as:
	- Premium block blobs
	- Premium page blobs
	- Premium file shares

## Recommended Storage Account Types

### Standard general-purpose v2

- Services: Blob Storage, Data Lake Storage, Queue Storage, Table Storage, Azure Files
- Redundancy: LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS
- Use for: most common Azure Storage scenarios

### Premium block blobs

- Services: Blob Storage, including Data Lake Storage
- Redundancy: LRS, ZRS
- Use for: high transaction rates, smaller objects, consistently low latency

### Premium file shares

- Services: Azure Files only
- Redundancy: LRS, ZRS
- Use for: enterprise and high-performance scale apps

### Premium page blobs

- Services: Page blobs only
- Redundancy: LRS, ZRS
- Use for: premium page blob workloads

## Access Tiers for Block Blob Data

### Hot tier

- For data accessed frequently
- Highest storage cost
- Lowest access cost
- Default tier for new storage accounts

### Cool tier

- For infrequently accessed data
- Minimum storage period: 30 days
- Lower storage cost than Hot
- Higher access cost than Hot

### Cold tier

- For infrequently accessed data stored longer than Cool use cases
- Minimum storage period: 90 days
- Lower storage cost than Cool
- Higher access cost than Cool

### Archive tier

- For rarely accessed data
- Applies only to individual block blobs
- Retrieval may take several hours
- Minimum storage period: 180 days
- Lowest storage cost
- Highest retrieval cost

## Tier Selection Rule

- Choose tiers based on how often data is accessed
- Move data between Hot, Cool, Cold, and Archive when usage patterns change

## Blob Storage Structure

### Storage account

- Top-level Azure resource
- Owns the namespace for stored data

### Container

- Logical grouping of blobs inside a storage account
- Similar to a folder boundary for organization and access management

### Blob

- The actual object being stored
- Can contain text or binary data such as images, documents, media, and backups

## Security and Encryption Notes

- Azure Storage supports secure access over HTTPS
- Access can be controlled at the storage account and data level
- Azure Storage includes encryption features to protect data at rest
- Security is a core part of protecting containers and blobs from unauthorized access

## Exam-Focused Takeaways

- Blob Storage is for unstructured data
- A storage account is the top-level namespace
- Standard GPv2 is the default recommendation for most scenarios
- Premium accounts are for higher performance and lower latency
- Hot, Cool, Cold, and Archive tiers are cost/performance choices based on access frequency
- Archive storage has the lowest storage cost but the highest retrieval delay and cost
