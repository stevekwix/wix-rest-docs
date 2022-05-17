SortOrder: 0
# About Pro Gallery


With Wix Pro Gallery, you can help site owners manage their Pro Galleries.

The Pro Gallery API allows your app to:

*   Get, and update Pro Galleries
*   Create, get, update, and delete media items

Read more about how site owners can manage their [Pro Galleries](https://support.wix.com/en/article/wix-pro-gallery-about-the-wix-pro-gallery).


## Terminology
+ **Pro Gallery:** A responsive, and customizable gallery that displays media items.
+ **Media Items:** Images, videos, and text files uploaded to a Pro Gallery. You can read more about [supported media](https://support.wix.com/en/article/wix-pro-gallery-adding-media-to-the-gallery).

## Sort Order
In order to preserve a defined order of galleries/items, Wix uses the sortOrder field.  

* You can update the `sortOrder` field using your own logic using the relevant **Update** endpoint.  
* If sortOrder is not given on creation, the `sortOrder` field will automatically be populated with the current timestamp ([Epoch time](https://en.wikipedia.org/wiki/Unix_time)).  
* In order to prevent updating the all previous/next items when reordering a single item, the Wix UI uses the following calculation:  
  `new_sortOrder = (next_item.sortOrder + previous_item.sortOrder)/2`   
  
> **Note**: Your app can choose other forms of logic to reorder items.


## Limitations
+ Currently, you can't create or delete a Pro Gallery via the API.
+ The [Gallery Created](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-created-webhook) and [Gallery Updated](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-updated-webhook) webhooks don't return the media items included in the gallery. To retrieve these items or their IDs you need to listen to the [Gallery Item Created](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-item-created-webhook) and [Gallery Item Updated](https://dev.wix.com/api/rest/site-content/pro-gallery/gallery-item-updated-webhook) webhooks in addition.
