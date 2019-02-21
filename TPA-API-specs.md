<< Back to [HOME](README.md)

## Login

#### To call server APIs a token is required. To get this token using the below mentioned login API

`tpaKey` will be provided by us, which you can store in a safe place in your server where no one can access it.

Login API retruns a `token` which you can use in rest of the APIs 

    /tpa/login [POST]
    
HEADER

    Content-Type:application/json
    
BODY
```javascript
{
  "tpaKey": "asdasd",  // required
  "customerId": "number" // required - example: 13 - we will provide this value and it will remain fixed
}
```

RESPONSE - code - 200
```javascript
{
  "result": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
  },
  "name": "SuccessfullySaved.",
  "code": 20,
  "message": "Notification Sent Successfully to Upgrade Devices"
}
```

## TPA app upgrade

#### Notify CMS server about app upgrade

Call this API to inform the server about a new build

    /tpa/app-upgrade/notify [POST]

HEADER

    Content-Type:application/json
    Authorization : Bearer <token>

QUERY

    NA

BODY
```javascript
{
  "deviceOs": "ANDROID|WINDOWS",  // required - possible values ANDROID or WINDOWS
  "buildDownloadUrl": "http://builddownloadurl", // required - this is the link to download the zip file of your application
  "tpappId": 123, // required - third party app id (CMS team will provide one ID which will be final and you can always use that one
  "tpappVersion": "x.y.z", // required - this is the version of the app that you are updating to
  "deviceIds": [    // required - specify on which device you want to send this build
    23,
    43,
    28
  ],
  "updateType": "DELETE_AND_UPDATE|ONLY_UPDATE"   // required - possible values DELETE_AND_UPDATE or ONLY_UPDATE
}
```

Parameters explained:

1. `deviceOs` : can be one of the following enums `ANDROID` or `WINDOWS`
2. `tpappVersion` : version of the app that is being updated
3. `updateType` : one of the following values: 
    1. `DELETE_AND_UPDATE` : this will trigger following action: delete all the files in the pre-defined folder and the move the new contents of the zip file to that folder
    2. `ONLY_UPDATE` : this will replace only those files on that folder which have same name. Copy the new files from the zip to that folder. Keep the files in the folder as it is if they are not present in the zip
    
    
RESPONSE - code - 200
```javascript
{
  "result": null,
  "name": "SuccessfullySaved.",
  "code": 20,
  "message": "Notification Sent Successfully to Upgrade Devices"
}
```

## IFrame APIs

These APIs can be used to add a new iframe based to CMS webapp. Each iframe will be shown by the CMS web app on a separate reports page. `iframeUrl` is the URL which be added in the `src` attribute of the `iframe` tag on the CMS web app

### Add a iframe url
--------------------

Use this API add an iframe url on the CMS app

    /iframe-url [POST]

HEADER

    Authorization: Bearer {userToken} 
    Content-Type:application/json

BODY
```javascript
{
  "iframeUrl": "string", // required
  "iframeTitle": "string",  // required - max 100 chars
  "iframeDescription": "string", // required - max 250 chars
  "order": 22  // required - defines in which order the iframe will appear on the CMS page
}
```

RESPONSE - code - 200
```javascript
{
  "result": {
    "iframeUrlId": 1, // long
    "iframeUrl": "string",
    "iframeTitle": "string",
    "iframeDescription": "string",
    "order": 22
  },
  "name": null,
  "code": null,
  "message": null
}
```

### Update a iframe url
-----------------------

Use this API update an existing iframe url on the CMS app

    /iframe-url/<iframeUrlId> [PUT]

HEADER

    Authorization: Bearer {userToken} 
    Content-Type:application/json

BODY
```javascript
{
  "iframeUrl": "string",
  "iframeTitle": "string",
  "iframeDescription": "string",
  "order": 22
}
```

RESPONSE - code - 200
```javascript
{
  "result": {
    "iframeUrlId": 1, // long
    "iframeUrl": "string",
    "iframeTitle": "string",
    "iframeDescription": "string",
    "order": 22
  },
  "name": null,
  "code": null,
  "message": null
}
```

### Get all iframe urls
-----------------------

Fetches all the iframe urls used on the CMS app

    /iframe-url [GET]

HEADER

    Authorization: Bearer {userToken} 
    Content-Type:application/json

BODY

    NA

RESPONSE - code - 200
```javascript
{
  "result": [
    {
      "iframeUrlId": 1, // long
      "iframeUrl": "string",
      "iframeTitle": "string",
      "iframeDescription": "string",
      "order": 22
    }
  ],
  "name": null,
  "code": null,
  "message": null
}
```

### Get a iframe url by id
--------------------------

Fetches an individual iframe url on the CMS app

    /iframe-url/<iframeUrlId> [GET]

HEADER

    Authorization: Bearer {userToken} 
    Content-Type:application/json

BODY

    NA

RESPONSE - code - 200
```javascript
{
  "result": {
    "iframeUrlId": 1, // long
    "iframeUrl": "string",
    "iframeTitle": "string",
    "iframeDescription": "string",
    "order": 22 // integer
  },
  "name": null,
  "code": null,
  "message": null
}
```

### Delete a iframe url
-----------------------

Use this API to delete an iframe url from the CMS app

    /iframe-url/<iframeUrlId> [DELETE]

HEADER

    Authorization: Bearer {userToken} 
    Content-Type:application/json

BODY

    NA

RESPONSE - code - 200
```javascript
{
  "result": null,
  "name": "SuccessfullyDeleted",
  "code": null,
  "message": "Succcessfully deleted"
}
```
