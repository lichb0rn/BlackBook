---
created: 2025-12-03 10:51
up:
  - "[[Восстановление БД из бекапа через snap]]"
related: "[[Commvault]]"
aliases:
tags:
  - type/note
summary:
---

# DumpBased backup
### Creating Subclients
As a best practice, it is recommended that you create separate subclients to back up data that undergo frequent changes.

### Subclient Content
As a best practice, it is recommended that you **add only a few small databases to each subclient** and add **larger databases into separate subclients**. On a restart condition, the system will back up all databases in the subclient from the beginning. For this reason, you would not want a large database that has completed its backup successfully to be backed up again only because a smaller one has caused a restart to occur.

### Better performance for dumpbased backup
To achieve better performance for dumpbased backups, enable Commvault compression.

## Using Parallel Jobs to Dump the PostgreSQL Database
You can use parallel jobs to dump the databases for DumpBasedBackupset subclients. To back up the database, parallel jobs use the `pg_dump -j` option.
https://documentation.commvault.com/2023e/commcell-console/using_parallel_jobs_to_dump_postgresql_database_04.html

## Configuring Streams for PostgreSQL Backups
For DumpBased backup set, the number of streams for data backup is set to two by default. However, you can change the number of streams based on the streams configured in the subclient's storage policy.

Each database dump will use one stream. If you have 4 databases to back up and the number of streams is 2, the Commvault software will dump two databases and invokes two pg_dump processes at the same time. **If you select the Use parallel jobs to dump the database check box, the number of pg_dump child processes that will initiate is equal to the result of multiplying number of streams with number of parallel jobs.**

# FSBased backup

## Configuring Streams for PostgreSQL Backups
For FSBased backup set, the number of streams for data backup is set to one by default. However, you can change the number of streams based on the streams configured in the subclient's storage policy.
https://documentation.commvault.com/2023e/commcell-console/configuring_streams_for_postgresql_backups.html

# General

**Tune Commvault Streams and Transfer Size**: For large databases, increasing the number of data streams and the maximum transfer size (e.g., to 4 MB) in the subclient properties can improve read/write speeds, though this requires more memory per stream.