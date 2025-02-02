# Backup Strategy

### Full Backups
A full backup is a complete snapshot of your PostgreSQL database at a specific point in time.
Frequency: Weekly (e.g., every Sunday night).

### Incremental Backups (WAL Archiving)
Write-Ahead Logging (WAL): PostgreSQL uses WAL files to record all changes made to the database.
Incremental Backups involve archiving WAL files, allowing you to restore to any point in time by replaying these logs.
Frequency: Continuous (as new WAL files are generated).
### Regular Dump Backups
Use pg_dump to create logical backups that are easy to restore and portable across different PostgreSQL versions.
Frequency: Daily (e.g., every night).

### Offsite and Cloud Backups
Store backups in multiple locations to ensure availability in case of local hardware failure.
Locations: Local disk, remote server, cloud storage (e.g., AWS S3, Google Cloud Storage).



### Example Backup Strategy Schedule

| Time	     | Task                                        |	Tool        |
| ---------- | ------------------------------------------- | -------------- |
| 1:00 AM    |	Daily logical backup (pg_dump)             | pg_dump        |
| 2:00 AM    |	Weekly full backup (Sunday)	               | pg_basebackup  |
| Continuous |	Incremental backups (WAL archiving)	       | WAL Archiving  |
| 3:30 AM    |	Upload backups to AWS S3	               | AWS CLI        |
| 4:00 AM    |	Cleanup old backups (older than 30 days)   | Shell Script   |

