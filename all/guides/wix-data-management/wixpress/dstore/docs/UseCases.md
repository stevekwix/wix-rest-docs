SortOrder: 1
# Use cases

## Backup

* Take a one-off backup
  * Submit a `take` request. Segment property should be set to "MANUAL", which indicates that user requested a backup ("AUTO" would indicate that backup was initiated automatically after collection was modified)

* Check if your backup has been successfully created
  * Send `listBackups` request. In response, validate if relevant backup has `SUCCESSFUL`
  status which indicates it is ready to use.

* Find most recent backup of instance data and use it to restore
  * Find the ID of backup you want use with `listBackups` request. Send `restore` request
  using the ID of your selected backup.

* Check if your data restoration has successfully completed
  * Send `listRestorations` request. Restoration has been completed if its status is
  * `SUCCESSFUL`.

* Remove backups you no longer need
  * Use `listBackups` to check existing backups. Send a `delete` request with a backup ID
  that you want to remove.
