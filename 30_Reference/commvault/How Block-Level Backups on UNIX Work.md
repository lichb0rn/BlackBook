---
created: 2025-12-14 14:17
up:
  - "[[Commvault]]"
related:
  - "[[Linux]]"
aliases:
tags:
  - type/note
summary:
---
[https://kb.commvault.com/article/?id=54301](https://kb.commvault.com/article/?id=54301)  

## Specifying the Volume to Back Up

To perform block-level backup operations on a snapshot-capable volume, configure the volume as subclient content. The volume that you back up can be a from a local disk or from a hardware snapshot engine that is supported by Commvault.

## The Phases of Block-Level Backup Operations

Block-level backup operations have the following phases:

- Snapshot copy phase
- Backup copy phase

Both of these phases have several sub-phases. For native (CVBF/LVMs) backup operations, both the phases run as a single job. For hardware snapshots, the snapshot copy phase and the backup copy phase run separately as two jobs.  

## Snapshot Copy Sub-Phases

1. Backup sub-phase: A snapshot is created. For native disks, CVBF snapshots are taken. The snapshots are created in the /dev/CVBF directory. For native LVMs, Commvault uses the LVM snapshot capability for snapshot creation. For hardware backups, Commvault uses the vendor-specific snapshots. The CVBF driver monitors the device and creates a bitmap by tracking the changed blocks while writes are being performed on the volume being monitored. A block device config file is also created which holds the volume details and properties.
2. Cleanup sub-phase: The temporary files that were created under the Job Results directory are removed.

## Backup Copy Sub-Phases

1. Scan sub-phase: The volume bitmaps and the block device config file are downloaded from the index. Extent collect files that have data-only blocks are generated.
2. Backup sub-phase: The snapshots are mounted, and the extents are moved from the snapshot to the media.
3. Archive index sub-phase: The index for the backup job is backed up to the media.

For native backup operations, a spool copy is automatically configured, and the snapshots are deleted after the backup copy job completes. For hardware backups, the snapshots are deleted according to the storage policy settings.

## File Indexing After Block-Level Backup Job Completion

If you enable the Index files after backup option, files are cataloged offline as a separate job after the block-level backup completes.