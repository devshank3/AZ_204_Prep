# Discover Blob Storage Lifecycle Policies

## Core Idea

- A lifecycle management policy is a JSON document.
- A policy contains one or more rules.
- Each rule has:
	- a filter set
	- an action set
- Filters decide which blobs the rule applies to.
- Actions define tiering or deletion behavior.

## Policy Structure

- Top-level property: `rules`
- `rules` is an array of rule objects.
- A policy must contain at least 1 rule.
- A policy can contain up to 100 rules.

## Rule Properties

### `name`

- Required
- Case-sensitive
- Must be unique within the policy
- Up to 256 alphanumeric characters

### `enabled`

- Optional
- Boolean
- Default is `true`
- Used to temporarily disable a rule

### `type`

- Required
- Valid value: `Lifecycle`

### `definition`

- Required
- Contains filters and actions

## Rule Filters

Filters narrow the rule scope to specific blobs. If multiple filters are used, Azure applies a logical AND.

### `blobTypes`

- Required
- Array of blob type values

### `prefixMatch`

- Optional
- Array of prefixes
- Up to 10 prefixes per rule
- Each prefix must start with a container name

### `blobIndexMatch`

- Optional
- Array of blob index tag conditions
- Up to 10 tag conditions per rule

## Rule Actions

At least one action must be defined for blobs or snapshots.

### Supported Actions

| Action | Current Version | Snapshot | Previous Versions |
|---|---|---|---|
| `tierToCool` | Block blob | Supported | Supported |
| `tierToCold` | Block blob | Supported | Supported |
| `enableAutoTierToHotFromCool` | Block blob | Not supported | Not supported |
| `tierToArchive` | Block blob | Supported | Supported |
| `delete` | Block blob, append blob | Supported | Supported |

## Important Rule Behavior

- If multiple actions apply to the same blob, Azure applies the least expensive action.
- Cost priority:
	- `delete` is cheaper than `tierToArchive`
	- `tierToArchive` is cheaper than `tierToCool`

## Action Run Conditions

### `daysAfterModificationGreaterThan`

- Used for base blob actions
- Based on last modified time

### `daysAfterCreationGreaterThan`

- Used for snapshot actions
- Based on snapshot creation time

### `daysAfterLastAccessTimeGreaterThan`

- Used for current blob versions
- Requires access tracking to be enabled

### `daysAfterLastTierChangeGreaterThan`

- Used with `tierToArchive`
- Ensures a rehydrated blob stays in hot, cool, or cold for a minimum number of days before returning to archive

## Example Rule Logic

A sample rule can:

- Move a blob to Cool after 30 days
- Move it to Archive after 90 days
- Delete it after 2,555 days
- Delete snapshots after 90 days

## Quick Memory Aid

- Policy = JSON document of rules
- Rule = filters + actions
- `blobTypes` = required filter
- Up to 100 rules per policy
- If multiple actions match, least expensive action wins
