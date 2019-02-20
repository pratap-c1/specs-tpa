## Login

#### To call server APIs a token is required. To get this token using the below mentioned login API

    /tpa/login [POST]
HEADER

    Content-Type:application/json
    
BODY
```javascript
{
  "tpaKey": "asdasd",  // required
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

    /app-upgrade/notify [POST]

HEADER

    Content-Type:application/json
    Authorization : Bearer <token>

QUERY

    NA

BODY
```javascript
{
  "deviceOs": "WINDOWS",  // required
  "buildDownloadUrl": "http://builddownloadurl", // required
  "tpappId": 123, // required - third party app id (CMS team will provide one ID which will be final and you can always use that one
  "tpappVersion": "x.y.z" // required - this is the version of the app that you are updating to
}
```

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

### Add a iframe url
--------------------

    /iframe-url [POST]

HEADER

    Authorization: Bearer {userToken} 
    Content-Type:application/json

BODY
```javascript
{
  "iframeUrl": "string"
}
```

RESPONSE - code - 200
```javascript
{
  "result": {
    "iframeUrlId": 1, // long
    "iframeUrl": "string"
  },
  "name": null,
  "code": null,
  "message": null
}
```

### Update a iframe url
-----------------------

    /iframe-url/<iframeUrlId> [PUT]

HEADER

    Authorization: Bearer {userToken} 
    Content-Type:application/json

BODY
```javascript
{
  "iframeUrl": "string"
}
```

RESPONSE - code - 200
```javascript
{
  "result": {
    "iframeUrlId": 1, // long
    "iframeUrl": "string"
  },
  "name": null,
  "code": null,
  "message": null
}
```

### Get all iframe urls
-----------------------

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
      "iframeUrl": "string"
    }
  ],
  "name": null,
  "code": null,
  "message": null
}
```

### Get a iframe url by id
--------------------------

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
    "iframeUrl": "string"
  },
  "name": null,
  "code": null,
  "message": null
}
```

### Delete a iframe url
-----------------------

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
