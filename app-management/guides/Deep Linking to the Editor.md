# Deep Linking to the Editor

## Introduction

This API generates a link to the user’s Editor and then with an offer to install the app and add it’s components to the stage.

### Authorization

This endpoint requires an authorization header - pass the access token from the [OAuth installation flow](https://dev.wix.com/api/rest/getting-started/authentication).

### Permissions

This endpoint requires the WIX_DEVELOPERS.GET_EDITOR_DEEP_LINK [permission scope](https://devforum.wix.com/en/article/available-permissions).

## Using the API

Custom parameters in the form of key-value pairs can be sent in the body of the request. They will be added to the Settings Panel of the custom element if one has been added to the app.

### Request

```curl
Curl -X GET \
https://wixapis.com/apps/v1/editor-deep-link \
-H 'Authorization: <AUTH>'
```

### Response

```json
{
   "url": <url>
}
```

If successful, the response contains a that sends users to their editor with a request to install or add your app.
If unsuccessful, the returned url parameter will be set to'1'.

## Custom Element Settings Panel

The custom element is an app component that adds visual control objects  as well as a settings panel. When an app with a custom element  is installed, whether by deep link or not, the settings are passed into the settings panel on the user's stage. The user can change the settings but you maintain access to them.

A custom element can be added to your app by selecting **Components > Website Component > Web component**:

![Custom Element](./../choose-custom-element.png)

A deep link can be used to send an app with a custom element to a user's stage together with its settings panel.

![Settings Panel](./../custom-element-on-stage.png)

Learn more about the custom element and its settings here.