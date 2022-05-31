SortOrder: 0
# About Site Actions API

![Site Folders](../docs/site-actions.jpg)

Sites Actions API enables management of Wix sites, by performing actions that are accessible to the site's owner, such as duplicating a site and moving it to trash.

Third party resellers, agencies and others can use the Site Actions API to sync their external platform with Wix and manage their Wix sites.

## Terminology
* **Site**:  A website in the account. Sites are accessible to site owners and contributors according to the specific permissions they hold on a specific site or on the entire account.
* **Trash**: A Wix site can be "moved to trash", but not deleted.

## Limitations
* Up to 20 sites can be trashed by ‘bulk move to trash’
* When duplicating a site, the new site name has to be up to 20 characters, and unique in the account level.

## Related APIs

* Move site to folder - [Moves sites into a specific folder](https://dev.wix.com/api/rest/account-level-apis/site-folders/move-sites-to-folder)

> **Note**: When you duplicate a site, some business-related content such as store orders, contacts, invoices and third party app settings will not be included.
