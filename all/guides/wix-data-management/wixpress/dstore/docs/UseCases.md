SortOrder: 1
# Use cases

## Backups

### Take a one-off backup
Submit a `take` request. Segment property should be set to "MANUAL", which indicates that user requested a backup ("AUTO" would indicate that backup was initiated automatically after collection was modified)

### Check if your backup has been successfully created
Send `listBackups` request. In response, validate if relevant backup has `SUCCESSFUL` status which indicates it is ready to use.

### Find most recent backup of instance data and use it to restore
Find the ID of backup you want use with `listBackups` request. Send `restore` request using the ID of your selected backup.

### Check if your data restoration has successfully completed
Send `listRestorations` request. Restoration has been completed if its status is `SUCCESSFUL`.

### Remove backups you no longer need
Use `listBackups` to check existing backups. Send a `delete` request with a backup ID
  that you want to remove.

## Improve query performance by adding index
Consider a user who is experiencing performance issues when querying their Wix Data collection. Collection called "Paintings" contains 50 000 items, and when user tries to find paintings by a certain painter the query times out. Adding an index on "Author" field could fix the problem.

* List schemas to find IDs for "Paintings" schema and "Author" field inside it, e.g. "paintings" and "author" accordingly.
* Create the index. Specify `paintings` for `collectionName`, `author` for `fields.path`.
* List indexes to get the status of the newly created index. Index will be in "BUILDING" state initially and will transition into "ACTIVE" state once the indexing process is completed.
* Once index is in "ACTIVE" state, query paintings by author to see improved performance.
