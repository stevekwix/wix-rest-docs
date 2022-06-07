SortOrder: 1
# Sample use cases & flows: Portfolio


This article shares some possible use cases for your app, as well as an example flow that could support each one. You're certainly not limited to these use cases, but they can be a helpful jumping off point as you plan your app's implementation.


## Third Party Use-Case: Show projects from multiple different sites/platforms on one site


Your app can help the site owners to show their projects, collecting it from different sites or platforms. 
For Example: "A large architecture firm that is looking to showcase all of their multiple architects, interior designers, or contractors all on one website."

1. Retrieve the external sites/platforms projects using their API (if its Wix Site with Portfolio, you can use [ListProjects]() or [QueryProjects]()).

1. Use [createCollection]() to create collection for each external source.

1. Use [createProject](), [createProjectItems]() to upload each project and assign to the right collection from previous step.

1. Use [createProjectItem]() or [BulkCreateProjectItems]() to upload media items to project.

### Keeping Portfolio synced to the external site/platform:

1. Your app needs to create a mapping between the Wix media items and the external media.

1. Listen to changes from external platform.

1. Use [updateProject]() or [deleteProject]() in case of changes in project.

1. Use [updateProjectItem]() or [deleteProjectItem]() in cases of changes in the project media.

## Velo Use-Case: Designers community for uploading and share their work

1. Create a custom page with form for members to upload their Projects.

1. When user first submitting his work, create a collection for the member using createCollection(), and store the mapping of the collectionId and memberId.

1. On submitting work use createProject(), createProjectItems() methods to upload the project and media items and assign to the relevant collection.

1. Now, all member's works can be shown together on the Portfolio page under different collections.
