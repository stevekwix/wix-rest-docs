SortOrder: 2
# Use cases

This article shares some possible uses of the Blog API endpoints and their responses.

## Post API

### Get a Post by ID or by Slug

To get a specific post, use [Get Post](https://dev.wix.com/api/rest/wix-blog/blog/post/get-post) to retrieve a post by its ID:

```
curl 'http://www.wixapis.com/blog/v3/posts/894a58a2-dc75-422d-9ca6-00a489750dfd' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

Another option for retrieving a specific post is [Get Post by Slug](https://dev.wix.com/api/rest/wix-blog/blog/post/get-post-by-slug):

```
curl 'http://www.wixapis.com/blog/v3/posts/slugs/my-vacation' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

An example response to both [Get Post](https://dev.wix.com/api/rest/wix-blog/blog/post/get-post) and [Get Post by Slug](https://dev.wix.com/api/rest/wix-blog/blog/post/get-post-by-slug) will look this:

```json
{
  "post": {
    "id": "894a58a2-dc75-422d-9ca6-00a489750dfd",
    "title": "My vacation",
    "firstPublishedDate": "2020-08-06T09:18:07.839Z",
    "lastPublishedDate": "2020-08-06T09:18:07.839Z",
    "featured": true,
    "pinned": false,
    "categoryIds": [
      "5f2bcaa0879ad500173577f3",
      "5f2bcaa5940a02003488af3e"
    ],
    "memberId": "5ee77ebfffeab500188f496b",
    "hashtags": [
      "sea",
      "sun"
    ],
    "commentingEnabled": true,
    "minutesToRead": 1,
    "tagIds": [
      "5f2bcaa0879a4400173577f1",
      "5f2bc445940a02003488af3a"
    ],
    "pricingPlanIds": [
      "5f2bc445940a02003498af3e"
    ],
    "relatedPostIds": [
      "111a58a2-dc75-422d-0015-00a489750dfd", 
      "211a58a2-dc75-422d-1512-00a489750dfd"
    ],
    "language": "en",
    "translationId": "111a58a2-dc75-422d-9ca6-00a489750dfd"
  }
}
```

### Get a Post's Metrics

To get post metrics (the number of comments, likes, and views) use [Get Post Metrics](https://dev.wix.com/api/rest/wix-blog/blog/post/get-post-metrics), passing the post ID:

```
curl 'http://www.wixapis.com/blog/v3/posts/894a58a2-dc75-422d-9ca6-00a489750dfd/metrics' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will look like this:

```json
{
  "metrics": {
    "comments": 5,
    "likes": 8,
    "views": 31
  }
}
```

### Bulk Get Post Metrics

To get post metrics for multiple posts, use [Bulk Get Post Metrics](https://dev.wix.com/api/rest/wix-blog/blog/post/get-post-metrics) and pass the post IDs:

```
curl 'http://www.wixapis.com/blog/v3/posts/metrics' --data-binary '{"post_ids": ["894a58a2-dc75-422d-9ca6-00a489750dfd"]}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>' -X PUT
```

The response will look like this:

```json
{
  "894a58a2-dc75-422d-9ca6-00a489750dfd": {
      "metrics": {
        "comments": 5,
        "likes": 8,
        "views": 31
      }
  }
}
```

### Retrieving Multiple Posts

To retrieve more than one post, use either the [List Posts](https://dev.wix.com/api/rest/wix-blog/blog/post/list-posts) or [Query Posts](https://dev.wix.com/api/rest/wix-blog/blog/post/query-posts) endpoints.

#### List Posts

Using the [List Posts](https://dev.wix.com/api/rest/wix-blog/blog/post/list-posts) endpoint, you can list all posts belonging to a category by providing the category ID:

```
curl 'http://www.wixapis.com/blog/v3/posts?categoryIds=5f2bcaa5940a02003488af3e' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

An example response to the call above will look like this:

```json
{
  "posts": [
    {
      "id": "894a58a2-dc75-422d-9ca6-00a489750dfd",
      "title": "My vacation",
      "firstPublishedDate": "2020-08-06T09:18:07.839Z",
      "lastPublishedDate": "2020-08-06T09:18:07.839Z",
      "featured": true,
      "pinned": false,
      "categoryIds": [
        "5f2bcaa0879ad500173577f3",
        "5f2bcaa5940a02003488af3e"
      ],
      "memberId": "5ee77ebfffeab500188f496b",
      "hashtags": [
        "sea",
        "sun"
      ],
      "commentingEnabled": true,
      "minutesToRead": 1,
      "tagIds": [
        "5f2bcaa0879a4400173577f1",
        "5f2bc445940a02003488af3a"
      ],
      "pricingPlanIds": [
        "5f2bc445940a02003498af3e"
      ],
      "relatedPostIds": [
        "111a58a2-dc75-422d-0015-00a489750dfd",
        "111a58a2-dc75-422d-1512-00a489750dfd"
      ],
      "language": "en",
      "translationId": "111a58a2-dc75-422d-9ca6-00a489750dfd"
    }
  ],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```

### Query Posts

If you need a more detailed query, use [Query Posts](https://dev.wix.com/api/rest/wix-blog/blog/post/query-posts).

In the example below we're going to request only posts that have a title starting with "My vacation".

Note that we're also requesting to include the `"URL"`, `"COUNTERS"`, and `"CONTENT_TEXT"` fields in the response:

```
curl 'https://www.wixapis.com/blog/v3/posts/query' --data-binary '{"fieldsToInclude": ["URL", "COUNTERS", "CONTENT_TEXT"], "filter":{"title":{"$startsWith": "My vacation"}}}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will look like this:

```json
{
  "posts": [
    {
      "id": "894a58a2-dc75-422d-9ca6-10a489750dfd",
      "title": "My vacation",
      "contentText": "This is my post of my holidays #sea #sun",
      "firstPublishedDate": "2020-08-01T09:18:07.839Z",
      "lastPublishedDate": "2020-08-06T09:18:07.839Z",
      "url": {
        "base": "https://some.wixsite.com/something-to-prod/blog",
        "path": "/blog/post/my-vacation"
      },
      "featured": true,
      "pinned": false,
      "categoryIds": [
        "5f2bcaa0879ad500173577f3",
        "5f2bcaa5940a02003488af3e"
      ],
      "memberId": "5ee77ebfffeab500188f4961",
      "hashtags": [
        "sea",
        "sun"
      ],
      "commentingEnabled": true,
      "metrics": {
        "comments": 5,
        "likes": 2,
        "views": 25
      },
      "minutesToRead": 1,
      "tagIds": [
        "5f2bcaa0879a4400173577f1",
        "5f2bc445940a02003488af3a"
      ],
      "pricingPlanIds": [
        "5f2bc445940a02003498af3e"
      ],
      "relatedPostIds": [
        "111a58a2-dc75-422d-0015-00a489750dfd", 
        "211a58a2-dc75-422d-1512-00a489750dfd"
      ],
      "language": "en",
      "translationId": "111a58a2-dc75-422d-9ca6-00a489750dfd"
    }
  ],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```

## Draft Post API

Draft post API differs from regular posts API that it enables working with unpublished drafts and their draft state, making drafts edits possible.
Post state becomes equals to draft and visible to external users only after the draft post is published, any changes made after post publication are not visible to external world until the post is not published again.

### Create a Draft Post
To create a new draft post use [Create Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/create-draft-post) API.
For create action it is needed to only specify `title` field value and other fields will be assigned default values,
however it is possible to specify other draft post fields values in request body:
```
curl -X POST \
  'http://www.wixapis.com/blog/v3/draft-posts/' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <AUTH>'
  -d '{
        "draftPost": {
          "title": "Places to visit in europe",
          "excerpt": "Most interesting places to visit in europe",
        }
      }'
```

The response is an unpublished draft post with its values:
```json
{
  "draftPost": {
    "id": "448d1238-0072-4458-a280-bf81c2dd8af1",
    "title": "Places to visit in europe",
    "featured": false,
    "categoryIds": [],
    "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a39",
    "hashtags": [],
    "commentingEnabled": true,
    "minutesToRead": 0,
    "tagIds": [],
    "relatedPostIds": [],
    "pricingPlanIds": [],
    "language": "en",
    "changeOrigin": "AUTO_SAVE",
    "contentId": "622f285f7952527f485bc138",
    "editingSessionId": "0aca7f65-1237-482e-bf51-6d14102ee691",
    "status": "UNPUBLISHED",
    "mostRecentContributorId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
    "hasUnpublishedChanges": true,
    "editedDate": "2022-03-14T11:34:55.121Z",
    "seoData": {
      "tags": []
    },
    "seoShowInSearch": true,
    "seoShowSnippetInSearch": true,
    "slugs": [],
    "createdDate": "2022-03-14T11:34:55.121Z"
  }
}
```
If you want to publish draft post right away after the creation you need to specify that explicitly by passing `shouldPublish` property set to `true`.

### Update a Draft Post

To update a specific draft post, use [Update Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/update-draft-post) to update a draft post fields like title, cover image or hashtags, but not limited:

```
curl 'http://www.wixapis.com/blog/v3/draft-posts/73464daf-beb2-4d3c-a681-7ded7d0a9c3f' --data-binary '{
  "fieldsToInclude": [
    "URL"
  ],
  "fieldMask": "draftPost.coverMedia,draftPost.hashtags",
  "draftPost": {
    "categoryIds": [],
    "slugs": [],
    "pricingPlanIds": [],
    "relatedPostIds": [],
    "tagIds": [],
    "hashtags": [
      "vacation",
      "dream",
      "summer"
    ],
    "id": "73464daf-beb2-4d3c-a681-7ded7d0a9c3f",
    "coverMedia": {
      "enabled": true,
      "displayed": true,
      "custom": true,
      "image": {
        "height": 773,
        "width": 602,
        "id": "4b9f4b_e6e2042ad2d949ba82c635f1b05c567c~mv2.jpeg"
      }
    }
  }
}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>' -X PATCH
```


The updated draft post will not be published after the update, unless you specify that explicitly by passing `shouldPublish` property set to `true`.
All updatable fields should be listed in `fieldmask` field. An example response to [Update Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/update-draft-post) will look something like this:

```json
{
  "draftPost": {
    "id": "73464daf-beb2-4d3c-a681-7ded7d0a9c3f",
    "title": "When expecting, expect the unexpected",
    "excerpt": null,
    "featured": false,
    "categoryIds": [],
    "coverMedia": {
      "enabled": true,
      "image": {
        "id": "4b9f4b_e6e2042ad2d949ba82c635f1b05c567c~mv2.jpeg",
        "url": "https://static.wixstatic.com/media/4b9f4b_e6e2042ad2d949ba82c635f1b05c567c~mv2.jpeg",
        "height": 773,
        "width": 602,
        "altText": null,
        "urlExpirationDate": null,
        "filename": null,
        "sizeInBytes": null
      },
      "displayed": true,
      "custom": true
    },
    "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
    "hashtags": [
      "vacation",
      "dream",
      "summer"
    ],
    "commentingEnabled": true,
    "minutesToRead": 1,
    "heroImage": null,
    "tagIds": [],
    "relatedPostIds": [],
    "pricingPlanIds": [],
    "translationId": null,
    "language": "en",
    "changeOrigin": "AUTO_SAVE",
    "richContent": {
      "nodes": [
        {
          "type": "PARAGRAPH",
          "id": "foo",
          "nodes": [
            {
              "type": "TEXT",
              "id": "",
              "nodes": [],
              "style": null,
              "textData": {
                "text": "Create a blog post subtitle that summarizes your post in a few short, punchy sentences and entices your audience to continue reading.",
                "decorations": []
              }
            }
          ],
          "style": null,
          "paragraphData": {
            "textStyle": {
              "textAlignment": "AUTO",
              "lineHeight": null
            },
            "indentation": 0
          }
        }
      ],
      "metadata": {
        "version": 1,
        "createdTimestamp": "2022-01-22T22:00:41.282Z",
        "updatedTimestamp": "2022-01-22T22:00:41.282Z",
        "id": "37dcb4d8-ace3-4d13-96de-553583b9aab7"
      },
      "documentStyle": {
        "headerOne": null,
        "headerTwo": null,
        "headerThree": null,
        "headerFour": null,
        "headerFive": null,
        "headerSix": null,
        "paragraph": null
      }
    },
    "status": "UNPUBLISHED",
    "moderationDetails": null,
    "hasUnpublishedChanges": true,
    "editedDate": "2022-01-22T22:00:39.694Z",
    "scheduledPublishDate": null,
    "firstPublishedDate": null,
    "seoData": {
      "tags": [],
      "settings": null
    },
    "seoShowInSearch": true,
    "seoShowSnippetInSearch": true,
    "paidContentParagraph": null,
    "slugs": [],
    "url": {
      "base": "https://some.wixsite.com/my-site-1",
      "path": "/post/when-expecting-expect-the-unexpected"
    },
    "createdDate": "2022-01-20T23:28:30.672Z"
  }
}
```

### Get a Draft Post by ID

To get a specific draft post, use [Get Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/get-draft-post) to retrieve a draft post by its ID:

```
curl 'http://www.wixapis.com/blog/v3/draft-posts/2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```


An example response to [Get Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/get-draft-post) will look something like this:

```json
{
  "draftPost": {
    "id": "2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5",
    "title": "When expecting, expect the unexpected",
    "excerpt": null,
    "featured": false,
    "categoryIds": [],
    "coverMedia": {
      "enabled": true,
      "image": {
        "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
        "url": "https://static.wixstatic.com/media/75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
        "height": 773,
        "width": 602,
        "altText": null,
        "urlExpirationDate": null,
        "filename": null,
        "sizeInBytes": null
      },
      "displayed": true,
      "custom": false
    },
    "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
    "hashtags": [
      "vacation",
      "dream",
      "summer"
    ],
    "commentingEnabled": true,
    "minutesToRead": 1,
    "heroImage": null,
    "tagIds": [],
    "relatedPostIds": [],
    "pricingPlanIds": [],
    "translationId": null,
    "language": "en",
    "changeOrigin": "NEW_EDIT_SESSION",
    "richContent": {
      "nodes": [
        {
          "type": "PARAGRAPH",
          "id": "foo",
          "nodes": [
            {
              "type": "TEXT",
              "id": "",
              "nodes": [],
              "style": null,
              "textData": {
                "text": "Create a blog post subtitle that summarizes your post in a few short, punchy sentences and entices your audience to continue reading.",
                "decorations": []
              }
            }
          ],
          "style": null,
          "paragraphData": {
            "textStyle": {
              "textAlignment": "AUTO",
              "lineHeight": null
            },
            "indentation": 0
          }
        },
        {
          "type": "IMAGE",
          "id": "f19jt",
          "nodes": [],
          "style": null,
          "imageData": {
            "containerData": {
              "width": {
                "size": "CONTENT"
              },
              "alignment": "CENTER",
              "spoiler": null,
              "height": null,
              "textWrap": true
            },
            "image": {
              "src": {
                "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
                "private": null
              },
              "width": 602,
              "height": 773,
              "duration": null
            },
            "link": null,
            "disableExpand": null,
            "altText": "A cat looking at a window",
            "caption": "",
            "disableDownload": null
          }
        },
        {
          "type": "PARAGRAPH",
          "id": "9lomm",
          "nodes": [
            {
              "type": "TEXT",
              "id": "",
              "nodes": [],
              "style": null,
              "textData": {
                "text": "#vacation #dream #summer",
                "decorations": []
              }
            }
          ],
          "style": null,
          "paragraphData": {
            "textStyle": {
              "textAlignment": "AUTO",
              "lineHeight": null
            },
            "indentation": 0
          }
        }
      ],
      "metadata": {
        "version": 1,
        "createdTimestamp": "2022-01-20T09:53:04.526Z",
        "updatedTimestamp": "2022-01-20T09:53:04.526Z",
        "id": "37dcb4d8-ace3-4d13-96de-553583b9aab7"
      },
      "documentStyle": {
        "headerOne": null,
        "headerTwo": null,
        "headerThree": null,
        "headerFour": null,
        "headerFive": null,
        "headerSix": null,
        "paragraph": null
      }
    },
    "status": "UNPUBLISHED",
    "moderationDetails": null,
    "hasUnpublishedChanges": true,
    "editedDate": "2022-01-20T09:52:13.037Z",
    "scheduledPublishDate": null,
    "firstPublishedDate": null,
    "seoData": {
      "tags": [],
      "settings": null
    },
    "seoShowInSearch": true,
    "seoShowSnippetInSearch": true,
    "paidContentParagraph": 1,
    "slugs": [],
    "url": null,
    "createdDate": "2022-01-20T09:50:25.694Z"
  }
}
```

### Retrieving Multiple Draft Posts

To retrieve more than one draft post, use either the [List Draft Posts](https://dev.wix.com/api/rest/community/blog/draft-post/list-draft-posts) or [Query Draft Posts](https://dev.wix.com/api/rest/community/blog/draft-post/query-draft-posts) endpoints.

#### List Draft Posts

Using the [List Draft Posts](https://dev.wix.com/api/rest/community/blog/draft-post/list-draft-posts) endpoint, list the draft posts that are of the provided status and of English language for example:

```
curl 'http://www.wixapis.com/blog/v3/draft-posts?status=UNPUBLISHED&language=en' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

An example response to the call above will look something like this:

```json
{
  "draftPosts": [
    {
      "id": "2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5",
      "title": "When expecting, expect the unexpected",
      "excerpt": null,
      "featured": false,
      "categoryIds": [],
      "coverMedia": {
        "enabled": true,
        "image": {
          "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
          "url": "https://static.wixstatic.com/media/75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
          "height": 773,
          "width": 602,
          "altText": null,
          "urlExpirationDate": null,
          "filename": null,
          "sizeInBytes": null
        },
        "displayed": true,
        "custom": false
      },
      "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
      "hashtags": [
        "vacation",
        "dream",
        "summer"
      ],
      "commentingEnabled": true,
      "minutesToRead": 1,
      "heroImage": null,
      "tagIds": [],
      "relatedPostIds": [],
      "pricingPlanIds": [],
      "translationId": null,
      "language": "en",
      "changeOrigin": "NEW_EDIT_SESSION",
      "richContent": {
        "nodes": [
          {
            "type": "PARAGRAPH",
            "id": "foo",
            "nodes": [
              {
                "type": "TEXT",
                "id": "",
                "nodes": [],
                "style": null,
                "textData": {
                  "text": "Create a blog post subtitle that summarizes your post in a few short, punchy sentences and entices your audience to continue reading.",
                  "decorations": []
                }
              }
            ],
            "style": null,
            "paragraphData": {
              "textStyle": {
                "textAlignment": "AUTO",
                "lineHeight": null
              },
              "indentation": 0
            }
          },
          {
            "type": "IMAGE",
            "id": "f19jt",
            "nodes": [],
            "style": null,
            "imageData": {
              "containerData": {
                "width": {
                  "size": "CONTENT"
                },
                "alignment": "CENTER",
                "spoiler": null,
                "height": null,
                "textWrap": true
              },
              "image": {
                "src": {
                  "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
                  "private": null
                },
                "width": 602,
                "height": 773,
                "duration": null
              },
              "link": null,
              "disableExpand": null,
              "altText": "A cat looking at a window",
              "caption": "",
              "disableDownload": null
            }
          },
          {
            "type": "PARAGRAPH",
            "id": "9lomm",
            "nodes": [
              {
                "type": "TEXT",
                "id": "",
                "nodes": [],
                "style": null,
                "textData": {
                  "text": "#vacation #dream #summer",
                  "decorations": []
                }
              }
            ],
            "style": null,
            "paragraphData": {
              "textStyle": {
                "textAlignment": "AUTO",
                "lineHeight": null
              },
              "indentation": 0
            }
          }
        ],
        "metadata": {
          "version": 1,
          "createdTimestamp": "2022-01-20T13:31:13.637Z",
          "updatedTimestamp": "2022-01-20T13:31:13.637Z",
          "id": "37dcb4d8-ace3-4d13-96de-553583b9aab7"
        },
        "documentStyle": {
          "headerOne": null,
          "headerTwo": null,
          "headerThree": null,
          "headerFour": null,
          "headerFive": null,
          "headerSix": null,
          "paragraph": null
        }
      },
      "status": "UNPUBLISHED",
      "moderationDetails": null,
      "hasUnpublishedChanges": true,
      "editedDate": "2022-01-20T09:52:13.037Z",
      "scheduledPublishDate": null,
      "firstPublishedDate": null,
      "seoData": {
        "tags": [],
        "settings": null
      },
      "seoShowInSearch": true,
      "seoShowSnippetInSearch": true,
      "paidContentParagraph": 1,
      "slugs": [],
      "url": null,
      "createdDate": "2022-01-20T09:50:25.694Z"
    }
  ],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```

### Query Draft Posts
If a more detailed query is needed, use [Query Draft Posts](https://dev.wix.com/api/rest/community/blog/draft-post/query-draft-posts).
In the example below we're going to request only draft posts that have a title starting with "When expecting".
Note that we're also requesting to include the `"URL"` field in the response:

```
curl 'https://www.wixapis.com/blog/v3/draft-posts/query' --data-binary '{"fieldsToInclude": ["URL"], "filter":{"title":{"$startsWith": "When expecting"}}}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response we got looked like this:

```json
{
  "draftPosts": [
    {
      "id": "2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5",
      "title": "When expecting, expect the unexpected",
      "excerpt": null,
      "featured": false,
      "categoryIds": [],
      "coverMedia": {
        "enabled": true,
        "image": {
          "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
          "url": "https://static.wixstatic.com/media/75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
          "height": 773,
          "width": 602,
          "altText": null,
          "urlExpirationDate": null,
          "filename": null,
          "sizeInBytes": null
        },
        "displayed": true,
        "custom": false
      },
      "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
      "hashtags": [
        "vacation",
        "dream",
        "summer"
      ],
      "commentingEnabled": true,
      "minutesToRead": 1,
      "heroImage": null,
      "tagIds": [],
      "relatedPostIds": [],
      "pricingPlanIds": [],
      "translationId": null,
      "language": "en",
      "changeOrigin": "NEW_EDIT_SESSION",
      "richContent": {
        "nodes": [
          {
            "type": "PARAGRAPH",
            "id": "foo",
            "nodes": [
              {
                "type": "TEXT",
                "id": "",
                "nodes": [],
                "style": null,
                "textData": {
                  "text": "Create a blog post subtitle that summarizes your post in a few short, punchy sentences and entices your audience to continue reading.",
                  "decorations": []
                }
              }
            ],
            "style": null,
            "paragraphData": {
              "textStyle": {
                "textAlignment": "AUTO",
                "lineHeight": null
              },
              "indentation": 0
            }
          },
          {
            "type": "IMAGE",
            "id": "f19jt",
            "nodes": [],
            "style": null,
            "imageData": {
              "containerData": {
                "width": {
                  "size": "CONTENT"
                },
                "alignment": "CENTER",
                "spoiler": null,
                "height": null,
                "textWrap": true
              },
              "image": {
                "src": {
                  "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
                  "private": null
                },
                "width": 602,
                "height": 773,
                "duration": null
              },
              "link": null,
              "disableExpand": null,
              "altText": "A cat looking at a window",
              "caption": "",
              "disableDownload": null
            }
          },
          {
            "type": "PARAGRAPH",
            "id": "9lomm",
            "nodes": [
              {
                "type": "TEXT",
                "id": "",
                "nodes": [],
                "style": null,
                "textData": {
                  "text": "#vacation #dream #summer",
                  "decorations": []
                }
              }
            ],
            "style": null,
            "paragraphData": {
              "textStyle": {
                "textAlignment": "AUTO",
                "lineHeight": null
              },
              "indentation": 0
            }
          }
        ],
        "metadata": {
          "version": 1,
          "createdTimestamp": "2022-01-20T13:41:05.368Z",
          "updatedTimestamp": "2022-01-20T13:41:05.368Z",
          "id": "37dcb4d8-ace3-4d13-96de-553583b9aab7"
        },
        "documentStyle": {
          "headerOne": null,
          "headerTwo": null,
          "headerThree": null,
          "headerFour": null,
          "headerFive": null,
          "headerSix": null,
          "paragraph": null
        }
      },
      "status": "UNPUBLISHED",
      "moderationDetails": null,
      "hasUnpublishedChanges": true,
      "editedDate": "2022-01-20T09:52:13.037Z",
      "scheduledPublishDate": null,
      "firstPublishedDate": null,
      "seoData": {
        "tags": [],
        "settings": null
      },
      "seoShowInSearch": true,
      "seoShowSnippetInSearch": true,
      "paidContentParagraph": 1,
      "slugs": [],
      "url": {
        "base": "https://some.wixsite.com/my-site-1",
        "path": "/post/when-expecting-expect-the-unexpected"
      },
      "createdDate": "2022-01-20T09:50:25.694Z"
    }
  ],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```

### Publish a Draft Post
When you are done editing your draft post, and it is ready to be published for your users, use [Publish Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/publish-draft-post) with the id of a post you want to publish:
```
curl 'https://www.wixapis.com/blog/v3/draft-posts/894a58a2-dc75-422d-9ca6-00a489750dfd/publish' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>' -X POST
```
The response will be a published post id:
```json
{
    "postId": "894a58a2-dc75-422d-9ca6-00a489750dfd"
}
```
After the publishing post becomes available to the public and can be fetched from [Post API's](https://dev.wix.com/api/rest/community/blog/post) with the given id.
> If you publish a Draft Post that is already published it will be updated with the latest Draft Post entities values

### Un Publish a Draft Post
If after the publishing you noticed that you made some mistakes, and you want to hide the post from the public until you fix them, use [Un Publish Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/un-publish-draft-post):
```
curl 'https://www.wixapis.com/blog/v3/draft-posts/894a58a2-dc75-422d-9ca6-00a489750dfd/un-publish' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>' -X POST
```
This actions returns empty response and reverts Post back to Draft Post which is not available to your users.
> Be careful, reverting Post to Draft Post will remove its view, like counts

### Delete a Draft Post
When you are not satisfied with your draft post, and you have decided to delete it, use [Delete Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/delete-draft-post) with the id of a post you want to delete:
```
curl 'https://www.wixapis.com/blog/v3/draft-posts/0eed85df-8332-4d7b-9184-164a482f0b41' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>' -X DELETE
```
As a result, the draft post will be moved to trash, from which it can later be restored. See [Restore Deleted Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/restore-deleted-draft-post).
The response of a successful deletion will be an empty object.
> Please take note that it's not restricted to delete a **published** post also. However, it will be unpublished, so use this action with caution as likes, comments and views counts will be lost in case of post restore from the trash.

### Delete a Draft Post permanently
If you decide that post in your trash will be no longer needed in the future, use [Delete Draft Post permanently](https://dev.wix.com/api/rest/community/blog/draft-post/delete-draft-post-permanently) to remove it from your blog permanently.
```
curl 'https://www.wixapis.com/blog/v3/draft-posts/trash/0eed85df-8332-4d7b-9184-164a482f0b41' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>' -X DELETE
```
This action returns an empty response.
> **WARNING**: be careful as this operation is destructive and there will be no way of restoring the post after permanent deletion.

### Get a Deleted Draft Post by ID

To get a specific deleted draft post, use [Get Deleted Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/get-deleted-draft-post) to retrieve a deleted draft post by its ID:

```
curl 'http://www.wixapis.com/blog/v3/draft-posts/trash-bin/2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```


An example response to [Get Deleted Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/get-deleted-draft-post) will look something like this:

```json
{
  "draftPost": {
    "id": "2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5",
    "title": "When expecting, expect the unexpected",
    "excerpt": null,
    "featured": false,
    "categoryIds": [],
    "coverMedia": {
      "enabled": true,
      "image": {
        "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
        "url": "https://static.wixstatic.com/media/75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
        "height": 773,
        "width": 602,
        "altText": null,
        "urlExpirationDate": null,
        "filename": null,
        "sizeInBytes": null
      },
      "displayed": true,
      "custom": false
    },
    "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
    "hashtags": [
      "vacation",
      "dream",
      "summer"
    ],
    "commentingEnabled": true,
    "minutesToRead": 1,
    "heroImage": null,
    "tagIds": [],
    "relatedPostIds": [],
    "pricingPlanIds": [],
    "translationId": null,
    "language": "en",
    "changeOrigin": "MOVE_TO_TRASH",
    "richContent": {
      "nodes": [
        {
          "type": "PARAGRAPH",
          "id": "foo",
          "nodes": [
            {
              "type": "TEXT",
              "id": "",
              "nodes": [],
              "style": null,
              "textData": {
                "text": "Create a blog post subtitle that summarizes your post in a few short, punchy sentences and entices your audience to continue reading.",
                "decorations": []
              }
            }
          ],
          "style": null,
          "paragraphData": {
            "textStyle": {
              "textAlignment": "AUTO",
              "lineHeight": null
            },
            "indentation": 0
          }
        },
        {
          "type": "IMAGE",
          "id": "f19jt",
          "nodes": [],
          "style": null,
          "imageData": {
            "containerData": {
              "width": {
                "size": "CONTENT"
              },
              "alignment": "CENTER",
              "spoiler": null,
              "height": null,
              "textWrap": true
            },
            "image": {
              "src": {
                "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
                "private": null
              },
              "width": 602,
              "height": 773,
              "duration": null
            },
            "link": null,
            "disableExpand": null,
            "altText": "A cat looking at a window",
            "caption": "",
            "disableDownload": null
          }
        },
        {
          "type": "PARAGRAPH",
          "id": "9lomm",
          "nodes": [
            {
              "type": "TEXT",
              "id": "",
              "nodes": [],
              "style": null,
              "textData": {
                "text": "#vacation #dream #summer",
                "decorations": []
              }
            }
          ],
          "style": null,
          "paragraphData": {
            "textStyle": {
              "textAlignment": "AUTO",
              "lineHeight": null
            },
            "indentation": 0
          }
        }
      ],
      "metadata": {
        "version": 1,
        "createdTimestamp": "2022-01-20T15:35:52.685Z",
        "updatedTimestamp": "2022-01-20T15:35:52.685Z",
        "id": "37dcb4d8-ace3-4d13-96de-553583b9aab7"
      },
      "documentStyle": {
        "headerOne": null,
        "headerTwo": null,
        "headerThree": null,
        "headerFour": null,
        "headerFive": null,
        "headerSix": null,
        "paragraph": null
      }
    },
    "status": "DELETED",
    "moderationDetails": null,
    "hasUnpublishedChanges": true,
    "editedDate": "2022-01-20T09:52:13.037Z",
    "scheduledPublishDate": null,
    "firstPublishedDate": null,
    "seoData": {
      "tags": [],
      "settings": null
    },
    "seoShowInSearch": true,
    "seoShowSnippetInSearch": true,
    "paidContentParagraph": null,
    "slugs": [],
    "url": null,
    "createdDate": "2022-01-20T09:50:25.694Z"
  }
}
```

### List Deleted Draft Posts

Using the [List Deleted Draft Posts](https://dev.wix.com/api/rest/community/blog/draft-post/list-deleted-draft-posts) endpoint, list the deleted draft posts:

```
curl 'http://www.wixapis.com/blog/v3/draft-posts/trash-bin' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

An example response to the call above will look something like this:

```json
{
  "draftPosts": [
    {
      "id": "2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5",
      "title": "When expecting, expect the unexpected",
      "excerpt": null,
      "featured": false,
      "categoryIds": [],
      "coverMedia": {
        "enabled": true,
        "image": {
          "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
          "url": "https://static.wixstatic.com/media/75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
          "height": 773,
          "width": 602,
          "altText": null,
          "urlExpirationDate": null,
          "filename": null,
          "sizeInBytes": null
        },
        "displayed": true,
        "custom": false
      },
      "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
      "hashtags": [
        "vacation",
        "dream",
        "summer"
      ],
      "commentingEnabled": true,
      "minutesToRead": 1,
      "heroImage": null,
      "tagIds": [],
      "relatedPostIds": [],
      "pricingPlanIds": [],
      "translationId": null,
      "language": "en",
      "changeOrigin": "MOVE_TO_TRASH",
      "richContent": {
        "nodes": [
          {
            "type": "PARAGRAPH",
            "id": "foo",
            "nodes": [
              {
                "type": "TEXT",
                "id": "",
                "nodes": [],
                "style": null,
                "textData": {
                  "text": "Create a blog post subtitle that summarizes your post in a few short, punchy sentences and entices your audience to continue reading.",
                  "decorations": []
                }
              }
            ],
            "style": null,
            "paragraphData": {
              "textStyle": {
                "textAlignment": "AUTO",
                "lineHeight": null
              },
              "indentation": 0
            }
          },
          {
            "type": "IMAGE",
            "id": "f19jt",
            "nodes": [],
            "style": null,
            "imageData": {
              "containerData": {
                "width": {
                  "size": "CONTENT"
                },
                "alignment": "CENTER",
                "spoiler": null,
                "height": null,
                "textWrap": true
              },
              "image": {
                "src": {
                  "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
                  "private": null
                },
                "width": 602,
                "height": 773,
                "duration": null
              },
              "link": null,
              "disableExpand": null,
              "altText": "A cat looking at a window",
              "caption": "",
              "disableDownload": null
            }
          },
          {
            "type": "PARAGRAPH",
            "id": "9lomm",
            "nodes": [
              {
                "type": "TEXT",
                "id": "",
                "nodes": [],
                "style": null,
                "textData": {
                  "text": "#vacation #dream #summer",
                  "decorations": []
                }
              }
            ],
            "style": null,
            "paragraphData": {
              "textStyle": {
                "textAlignment": "AUTO",
                "lineHeight": null
              },
              "indentation": 0
            }
          }
        ],
        "metadata": {
          "version": 1,
          "createdTimestamp": "2022-01-20T15:34:39.999Z",
          "updatedTimestamp": "2022-01-20T15:34:39.999Z",
          "id": "37dcb4d8-ace3-4d13-96de-553583b9aab7"
        },
        "documentStyle": {
          "headerOne": null,
          "headerTwo": null,
          "headerThree": null,
          "headerFour": null,
          "headerFive": null,
          "headerSix": null,
          "paragraph": null
        }
      },
      "status": "DELETED",
      "moderationDetails": null,
      "hasUnpublishedChanges": true,
      "editedDate": "2022-01-20T09:52:13.037Z",
      "scheduledPublishDate": null,
      "firstPublishedDate": null,
      "seoData": {
        "tags": [],
        "settings": null
      },
      "seoShowInSearch": true,
      "seoShowSnippetInSearch": true,
      "paidContentParagraph": null,
      "slugs": [],
      "url": null,
      "createdDate": "2022-01-20T09:50:25.694Z"
    }
  ],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```

### Restore a Deleted Draft Post

To restore a specific deleted draft post from trash, use [Restore Deleted Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/restore-deleted-draft-post) to restore a deleted draft post by its ID:

```
curl 'http://www.wixapis.com/blog/v3/draft-posts/trash-bin/2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5/restore' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>' -X POST
```


An example response to [Restore Deleted Draft Post](https://dev.wix.com/api/rest/community/blog/draft-post/restore-deleted-draft-post) will look something like this:

```json
{
  "draftPost": {
    "id": "2c0f1022-2ab5-4e57-95b0-0b36b78f4ed5",
    "title": "When expecting, expect the unexpected",
    "excerpt": null,
    "featured": false,
    "categoryIds": [],
    "coverMedia": {
      "enabled": true,
      "image": {
        "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
        "url": "https://static.wixstatic.com/media/75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
        "height": 773,
        "width": 602,
        "altText": null,
        "urlExpirationDate": null,
        "filename": null,
        "sizeInBytes": null
      },
      "displayed": true,
      "custom": false
    },
    "memberId": "4b9f4b64-0792-481e-9289-b2550c1bb7ea",
    "hashtags": [],
    "commentingEnabled": true,
    "minutesToRead": 1,
    "heroImage": null,
    "tagIds": [],
    "relatedPostIds": [],
    "pricingPlanIds": [],
    "translationId": null,
    "language": "en",
    "changeOrigin": "NEW_EDIT_SESSION",
    "richContent": {
      "nodes": [
        {
          "type": "PARAGRAPH",
          "id": "foo",
          "nodes": [
            {
              "type": "TEXT",
              "id": "",
              "nodes": [],
              "style": null,
              "textData": {
                "text": "Create a blog post subtitle that summarizes your post in a few short, punchy sentences and entices your audience to continue reading.",
                "decorations": []
              }
            }
          ],
          "style": null,
          "paragraphData": {
            "textStyle": {
              "textAlignment": "AUTO",
              "lineHeight": null
            },
            "indentation": 0
          }
        },
        {
          "type": "IMAGE",
          "id": "f19jt",
          "nodes": [],
          "style": null,
          "imageData": {
            "containerData": {
              "width": {
                "size": "CONTENT"
              },
              "alignment": "CENTER",
              "spoiler": null,
              "height": null,
              "textWrap": true
            },
            "image": {
              "src": {
                "id": "75059a_9f8cd2f1282c4dc7ae9a4bea155e2661~mv2.jpg",
                "private": null
              },
              "width": 602,
              "height": 773,
              "duration": null
            },
            "link": null,
            "disableExpand": null,
            "altText": "A cat looking at a window",
            "caption": "",
            "disableDownload": null
          }
        },
        {
          "type": "PARAGRAPH",
          "id": "9lomm",
          "nodes": [
            {
              "type": "TEXT",
              "id": "",
              "nodes": [],
              "style": null,
              "textData": {
                "text": "#vacation #dream #summer",
                "decorations": []
              }
            }
          ],
          "style": null,
          "paragraphData": {
            "textStyle": {
              "textAlignment": "AUTO",
              "lineHeight": null
            },
            "indentation": 0
          }
        }
      ],
      "metadata": {
        "version": 1,
        "createdTimestamp": "2022-02-01T20:00:22.885Z",
        "updatedTimestamp": "2022-02-01T20:00:22.885Z",
        "id": "37dcb4d8-ace3-4d13-96de-553583b9aab7"
      },
      "documentStyle": {
        "headerOne": null,
        "headerTwo": null,
        "headerThree": null,
        "headerFour": null,
        "headerFive": null,
        "headerSix": null,
        "paragraph": null
      }
    },
    "status": "UNPUBLISHED",
    "moderationDetails": null,
    "hasUnpublishedChanges": true,
    "editedDate": "2022-01-20T23:06:17.182Z",
    "scheduledPublishDate": null,
    "firstPublishedDate": "2022-01-20T22:17:59.798Z",
    "seoData": {
      "tags": [],
      "settings": null
    },
    "seoShowInSearch": true,
    "seoShowSnippetInSearch": true,
    "paidContentParagraph": null,
    "slugs": [],
    "url": null,
    "createdDate": "2022-01-20T09:50:25.694Z"
  }
}
```


## Category API


### Get a Category

To get a specific category, use [Get Category](https://dev.wix.com/api/rest/wix-blog/blog/category/get-category) to retrieve a category by its ID:

```
curl 'http://www.wixapis.com/blog/v3/categories/894a58a2-dc75-422d-9ca6-10a489750dfd' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will contain a category object:

```json
{
  "category": {
    "id": "894a58a2-dc75-422d-9ca6-10a489750dfd",
    "label": "Summer",
    "postCount": 17,
    "description": "Posts about my summer",
    "title": "Summer",
    "rank": 1,
    "language": "en",
    "translationId": "111a58a2-dc75-422d-9ca6-00a489750dfd"
  }
}
```

### Retrieving Multiple Categories

To retrieve more than one category, use either the [List Categories](https://dev.wix.com/api/rest/wix-blog/blog/category/list-categories) or [Query Categories](https://dev.wix.com/api/rest/wix-blog/blog/category/query-categories) endpoints.

#### List Categories

Using the [List Categories](https://dev.wix.com/api/rest/wix-blog/blog/category/list-categories) endpoint, you can retrieve all existing categories:

```
curl 'http://www.wixapis.com/blog/v3/categories' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will be an array of the retrieved categories:

```json
{
  "categories": [
    {
      "id": "93f76102-d776-414f-b19f-854b0028035b",
      "label": "Vegetarian",
      "postCount": 0,
      "description": "Vegetarian recipes",
      "title": "Vegetarian",
      "coverMedia": {
        "enabled": true,
        "displayed": true
      },
      "rank": 0,
      "language": "en"
    },
    {
      "id": "05211adc-ae26-43fa-9f09-6cdbb53174ce",
      "label": "Fish",
      "postCount": 2,
      "description": "Fish recipes",
      "title": "Fish",
      "coverMedia": {
        "enabled": true,
        "displayed": true
      },
      "rank": 1,
      "language": "en"
    },
    {
      "id": "a68da372-6bfa-412c-ad29-a3f1000ea3f2",
      "label": "Spices",
      "postCount": 0,
      "description": "Ideas how to create your own spices",
      "title": "Spices",
      "coverMedia": {
        "enabled": true,
        "displayed": true
      },
      "rank": 2,
      "language": "en"
    }
  ],
  "metaData": {
    "count": 3,
    "offset": 0,
    "total": 3
  }
}
```

#### Query Categories

If a more detailed query is needed, use [Query Categories](https://dev.wix.com/api/rest/wix-blog/blog/category/query-categories).

In the example below we request only categories that have a title starting with "Summer":

```
curl 'https://www.wixapis.com/blog/v3/categories/query' --data-binary '{"fieldsToInclude": ["URL"], "filter":{"title":{"$startsWith": "Summer"}}}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will be an array of the categories that matched the query:

```json
{
  "categories": [
  {
    "id": "894a58a2-dc75-422d-9ca6-10a489750dfd",
    "label": "Summer",
    "postCount": 17,
    "url": {
      "base": "https://some.wixsite.com/something-to-prod/blog",
      "path": "/blog/categories/summer"
    },
    "description": "Posts about my summer",
    "title": "Summer",
    "rank": 1,
    "language": "en",
    "translationId": "111a58a2-dc75-422d-9ca6-00a489750dfd"
  }],
  "metaData": {
    "count": 1,
    "offset": 0,
    "total": 1
  }
}
```



## Tag API

Tags, like categories, provide a way to group your posts. Tags are more lightweight and granular than categories.

### Query Blog Posts by Tag

Imagine a cooking blog where a site owner writes recipes as posts, and groups them by recipe type using categories.

Additional information about the main ingredients is also found in tags like `chicken`, `mushrooms`, `fresh pasta`, `etc`.

This allows the site owner to layer multiple classifications onto their posts, which you can then retrieve in more flexible ways.

Step 1. **Retrieve List of Desired Tags**

To fetch all the tags representing ingredients from the blog, use the [Query Tags](https://dev.wix.com/api/rest/wix-blog/blog/tags/query-tags) endpoint.

In the specific example below, we request all tags with a label starting with word "coriander":

```
curl 'https://www.wixapis.com/blog/v2/tags/query' --data-binary '{"filter":{"label":{"$startsWith": "coriander"}}}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will be an array of the tags that matched the query:

```json
{
  "tags": [
    {
      "id": "f0ad2e22-2cfd-49ff-aa3a-eae68a9d5008",
      "label": "coriander leaves",
      "slug": "coriander-leaves",
      "createdDate": "2021-11-17T11:26:53.987Z",
      "updatedDate": "2021-11-17T11:26:53.987Z",
      "publicationCount": 1,
      "postCount": 1,
      "url": {
        "base": "https://fantastic-cooking.com",
        "path": "/recipes/tags/coriander-leaves"
      },
      "language": "en"
    },
    {
      "id": "fec0b26b-fdcd-4662-badb-fd23a123f0ec",
      "label": "coriander seeds",
      "slug": "coriander-seeds",
      "createdDate": "2021-11-17T11:31:45.892Z",
      "updatedDate": "2021-11-17T11:31:45.892Z",
      "publicationCount": 1,
      "postCount": 1,
      "url": {
        "base": "https://fantastic-cooking.com",
        "path": "/recipes/tags/coriander-seeds"
      },
      "language": "en"
    }
  ],
  "metaData": {
    "count": 2,
    "offset": 0,
    "total": 2
  }
}
```
Step 2. **Retrieve Posts Matching the Tags**
  
The returned tag IDs can be used in the [Query Posts](https://dev.wix.com/api/rest/wix-blog/blog/post/query-posts) endpoints, to get all the posts with the specified tag:

```
curl 'https://www.wixapis.com/blog/v3/posts/query' --data-binary '{"fieldsToInclude": ["URL"], "filter":{"tagIds":{"$hasSome": ["f0ad2e22-2cfd-49ff-aa3a-eae68a9d5008", "fec0b26b-fdcd-4662-badb-fd23a123f0ec"]}}}' -H 'Content-Type: application/json' -H 'Authorization: <AUTH>'
```

The response will look like this:

```json
{
  "posts": [
    {
      "id": "ccedcbe1-5588-4833-b2d7-7d33b9c24d15",
      "title": "Pepper and Coriander Crusted Tuna",
      "excerpt": "Pepper and Coriander Crusted Tuna",
      "firstPublishedDate": "2021-11-17T11:30:59.861Z",
      "lastPublishedDate": "2021-11-17T11:30:59.861Z",
      "slug": "pepper-and-coriander-crusted-tuna",
      "featured": false,
      "pinned": false,
      "categoryIds": [],
      "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
      "hashtags": [],
      "commentingEnabled": true,
      "minutesToRead": 1,
      "tagIds": [
        "f7a2fa4d-c3b3-48a6-91bf-9b6a422971fe",
        "d45f3110-00e0-4339-8619-7b6863002e37",
        "fec0b26b-fdcd-4662-badb-fd23a123f0ec",
        "215f3038-2a7a-460f-b876-fe1e17dea1cd"
      ],
      "relatedPostIds": [],
      "pricingPlanIds": [],
      "language": "en"
    },
    {
      "id": "20b6a0a9-8492-406a-898b-a793b09048a9",
      "title": "Pico de gallo salsa",
      "excerpt": "Pico de gallo salsa",
      "firstPublishedDate": "2021-11-17T11:27:34.603Z",
      "lastPublishedDate": "2021-11-17T11:27:34.603Z",
      "slug": "pico-de-gallo-salsa",
      "featured": false,
      "pinned": false,
      "categoryIds": [],
      "memberId": "2d24cb8a-adcc-466a-ab59-fa74e0889a37",
      "hashtags": [],
      "commentingEnabled": true,
      "minutesToRead": 1,
      "tagIds": [
        "0a57ac1a-1733-4fd3-8a17-123b1578399b",
        "f0ad2e22-2cfd-49ff-aa3a-eae68a9d5008",
        "c0dac587-0963-43dd-ae48-9afa432bab22",
        "4f801cd8-47d3-4434-81ff-5ff9178ae40e"
      ],
      "relatedPostIds": [],
      "pricingPlanIds": [],
      "language": "en"
    }
  ],
  "metaData": {
    "count": 2,
    "offset": 0,
    "total": 2
  }
}
```

#### Retrieve single tag

You can also retrieve a single tag either by ID, slug or label.

To fetch a tag by ID, use the [Get Tag](https://dev.wix.com/api/rest/wix-blog/blog/tags/get-tag) endpoint:

```
curl \
'http://www.wixapis.com/blog/v3/tags/6d72a3bb-053c-4de5-a897-5ef6be30b1b0' \
-H 'Content-Type: application/json' \
-H 'Authorization: <AUTH>'
```

The [Get Tag By Label](https://dev.wix.com/api/rest/wix-blog/blog/tags/get-tag-by-label) endpoint can be used to fetch tag when the label is known:

```
curl \
  'http://www.wixapis.com/blog/v3/tags/labels/eggplant' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <AUTH>'
```

To fetch a tag using its URL slug, use [Get Tag By Slug](https://dev.wix.com/api/rest/wix-blog/blog/tags/get-tag-by-slug):

```
curl \
  'http://www.wixapis.com/blog/v3/tags/slugs/eggplant' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <AUTH>'
```

The response structure is the same for all three requests; a single tag object.

```json
{
  "tag": {
    "id": "6d72a3bb-053c-4de5-a897-5ef6be30b1b0",
    "label": "eggplant",
    "slug": "eggplant",
    "createdDate": "2021-08-13T08:58:20.145Z",
    "updatedDate": "2021-08-13T08:58:20.145Z",
    "publicationCount": 2,
    "postCount": 1,
    "language": "en"
  }
}
```

## Post Stats API

#### Get Total Posts

Retrieves total post count by given language. For example to get total count for publications written in english language use request:

```
curl 'www.wixapis.com/blog/v2/stats/posts/total?language=en' \
    -H 'Content-Type: application/json' \
    -H 'Authorization: <AUTH>'
```

The response will be a json object with `total` field which represents total publication count for given language:

```json
{ "total": 9 }
```

`language` parameter is optional and when is not present post count for all languages will be present

#### Query Post Count

Retrieves the number of posts per month published from first day of a month, ignoring days value in period start field.  
For example, to retrieve statistics for posts in English language for last 3 months starting from `2018-11-01` ordered by oldest month first:

```
curl --request POST 'http://social-blog.wix.com/_api/communities-blog-node-api/v2/stats/posts/count' \
    --header 'Authorization: <AUTH>' \
    --header 'Content-Type: application/json' \
    --data-raw '{
                  "rangeStart": "2018-11-01",
                  "order": "OLDEST",
                  "months": 3,
                  "language": "en"
                }'
```

The response will be a json object with `stats` array field where each entry represents statistic of posts in english language count for a single month

```json
{ "stats": [
    {
    "periodStart": "2018-11-01T00:00:00.000Z",
    "postCount": 1
  },
    {
    "periodStart": "2018-12-01T00:00:00.000Z",
    "postCount": 2
  },
    {
    "periodStart": "2019-01-01T00:00:00.000Z",
    "postCount": 2
  }
]} 
```
