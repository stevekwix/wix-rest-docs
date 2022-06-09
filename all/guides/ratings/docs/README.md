SortOrder: 0
# Introduction

The Wix Ratings app allows site visitors and members to add ratings (scores) when:

* leaving a review for product/service
* commenting on a blog post with an added rating.

Each rating has a unique name and a points value. There can be multiple ratings for different aspects of the rated entity, plus an overall rating of the same entity.

An example could be leaving a review on an online shoe store. Together with their review, a site member or visitor could evaluate the whole product, giving an overall star rating for shoes.

They could also rate specific features (attributes) related to the product. These could be, for example,

* quality,
* shipping,
* color,
* value for money.

The site owner can configure the ratings, add attributes and let site visitors/members evaluate some specific parts of the product/service/other. The ratings API provides overall rating and rating per attribute (category, feature).

The default points value for the Wix Reviews app is from 1 to 5. However, the Ratings API allows third party developers to change the min and max rating values if needed.

TODO: anonymous ratings

TODO: inactive ratings

## Terminology
* **Namespace** name of application which manages ratings.
* **Group** logical container which scopes entities and gives the ability to differentiate between them.
* **Entity** a target for which rating is created.
* **Attribute:** various characteristics of an item that can be rated separate by the site visitors or members. It could be e.g., “main rating”, “color rating”, “quality rating”, “price rating” or other.
* **Rating:** an integer rating (points value) that site visitors or members give to an item.

**Example**:  User creates a product review for the **t-shirt** he just bought in **Stores** via **Wix Review** solution where he rated **quality** - **5/5** and **fit** - **4/5**, when the review is published rating is stored in Ratings service where it can be used to compute overall score of the product
* Namespace - Wix Review
* Group - Stores
* Entity - T-shirt product
* Attributes and values:
  * quality - 5
  * fit - 4


## Integrations

* Ratings is used in Wix Reviews for attributes of a product or service. One user can leave one rating per product attribute. A user can update their rating, overriding the previous rating.
* Wix Blog uses Ratings in comments to enable users to leave comment together with a rating.

## Limitations

* Only one rating per member/visitor/contact per entity and attribute.
* Only possible to group by entityId or group.
