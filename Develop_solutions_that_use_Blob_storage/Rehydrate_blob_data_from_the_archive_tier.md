# Rehydrate Blob Data from the Archive Tier

## Core Idea

- Blobs in the Archive tier are offline.
- Archived blobs cannot be read or modified directly.
- To use the data, the blob must first be rehydrated to an online tier:
  - Hot
  - Cool

## Rehydration Options

### 1. Copy Archived Blob to an Online Tier

- Use `Copy Blob` or `Copy Blob From URL`.
- Creates a new blob in Hot or Cool tier.
- Source blob remains in Archive tier.
- Recommended by Microsoft for most scenarios.

Important rules:

- Destination must be a new blob.
- You cannot overwrite the source blob by copying to the same blob.
- You must use a different blob name or a different container.

### 2. Change Blob Tier Directly

- Use `Set Blob Tier`.
- Changes the archived blob to Hot or Cool tier.
- Once started, the operation cannot be canceled.
- Until rehydration completes, the blob still shows as `archived`.

## Rehydration Time

- Rehydration can take several hours.
- Large blobs are generally better candidates for rehydration.
- Rehydrating many small blobs at the same time can take longer.

## Rehydration Priority

Priority is set using the optional `x-ms-rehydrate-priority` header.

### Standard

- Processed in normal request order
- May take up to 15 hours

### High

- Prioritized over standard requests
- Can complete in under 1 hour for blobs smaller than 10 GB

## Check Rehydration Priority

- Use `Get Blob Properties`
- Check the `x-ms-rehydrate-priority` header
- Returned value is either:
  - `Standard`
  - `High`

## Copy Rehydration Scope

- For service versions earlier than `2021-02-12`, copy-based rehydration is supported only within the same storage account.
- Starting with service version `2021-02-12`, you can copy to a different storage account if the destination account is in the same region as the source account.

## Important Caution

- `Set Blob Tier` does not change the blob's last modified time.
- If a lifecycle management policy exists, the blob may be moved back to Archive after rehydration.
- This happens if the last modified time is already beyond the lifecycle policy threshold.

## Quick Memory Aid

- Archive = offline
- Rehydrate to Hot or Cool
- Best option: copy to a new online blob
- `Set Blob Tier` cannot be canceled
- Priority header: `x-ms-rehydrate-priority`
- Lifecycle policy can archive it again