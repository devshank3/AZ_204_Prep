# Manage the Azure Blob Storage Lifecycle

## Core Idea

- Data access patterns change over time.
- New data is usually accessed more often.
- Older data is usually accessed less often.
- Azure Blob Storage access tiers help reduce cost by matching storage to usage patterns.

## Access Tiers

### Hot

- Online tier
- Best for frequently accessed data
- Highest storage cost, lower access cost

### Cool

- Online tier
- Best for infrequently accessed data
- Minimum storage period: 30 days

### Cold

- Online tier
- Best for infrequently accessed data stored longer than cool-tier scenarios
- Minimum storage period: 90 days
- Lower storage cost than cool, but higher access cost

### Archive

- Offline tier
- Best for rarely accessed data
- Minimum storage period: 180 days
- Retrieval latency is typically hours

## Important Note

- Storage limits are set at the storage account level, not per tier.
- You can use one tier only, or distribute data across multiple tiers.

## Lifecycle Management

- Azure Blob Storage lifecycle management uses rule-based policies.
- Policies can automatically move data to a more cost-effective tier or delete it when no longer needed.

## What Lifecycle Policies Can Do

- Move blobs from cool to hot immediately when accessed.
- Move current blob versions to cooler tiers based on age or inactivity.
- Move previous blob versions to cooler tiers.
- Move blob snapshots to cooler tiers.
- Delete current versions, previous versions, or snapshots at the end of their lifecycle.

## Policy Scope and Filters

- Can apply to the entire storage account.
- Can target specific containers.
- Can target a subset of blobs using:
	- name prefixes
	- blob index tags

## Example Lifecycle Pattern

- Early stage: use Hot tier for frequent access.
- After about 2 weeks: use Cool tier for occasional access.
- After about 1 month: use Archive tier for rarely accessed data.

This reduces cost by moving data to the cheapest appropriate tier as it ages.

## Quick Memory Aid

- Hot = frequent access
- Cool = infrequent, 30 days
- Cold = less frequent, 90 days
- Archive = rare access, offline, 180 days
- Lifecycle policy = transition or delete automatically
