# Backup and recovery

| Item | Recorded status |
| --- | --- |
| Local restic backup | The October 27 manual full run processed roughly 540 GiB and created an encrypted snapshot on a dedicated internal backup disk. The owner confirmed a completed local backup on November 3. The first snapshot did not include the Pi-hole export. |
| Scheduled execution | A systemd backup timer was configured. The November 3 review saw a failed scheduled run. Its root cause and subsequent success were unverified. |
| Repository integrity | The November review did not have permission to enumerate snapshots or run a repository check. The latest snapshot and integrity status remain unverified. |
| NAS copy | A cold copy was attempted and stopped due to slow transfer. The copy remained incomplete and the NAS was in standby at the November review. |
| Restore drill | Outstanding. No measured recovery time or recovery point is available. |

The local repository is the recorded recovery source. It lives on a separate disk in the same host, so loss of Server1 can still affect both primary data and the backup.

## Backup design

The recorded job design checks that the backup disk is mounted, stages application database dumps, captures selected data and configuration with restic, and applies retention. Nextcloud recovery requires compatible database, configuration and file data. The successful manual run and failed scheduled run provide different evidence about this workflow.

## Restore drill procedure

1. Identify a readable snapshot and check that it contains the expected application data and database dump.
2. Restore a sample file tree and the matching Nextcloud database and configuration into an isolated scratch environment.
3. Check sample file integrity, application startup, sign-in and representative file access.
4. Record the snapshot age, elapsed recovery time and any missing inputs. Verify a complete NAS copy separately before relying on it for recovery.

[Back to overview](../README.md)
