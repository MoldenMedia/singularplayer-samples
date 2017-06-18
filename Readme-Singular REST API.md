# Singular REST API

## Introduction

Welcome to the Singular.live REST API documentation. The Singular.live REST API provides functions to GET information on Web Channels, private and public Data Nodes, to CREATE Data Nodes, to UPDATE their content and to CONTROL Web Channels.
This document describes the REST API calls and the JSON data formats used. You can use any HTTP based library to access the Singular.live REST API. The examples in this document show requests and responses used in curl. 
The base URL of the REST API is [`https://app.singular.live/apiv1`](https://app.singular.live/apiv1).

**NOTE:**
> At the current time (May, 2017), the base URL of the REST API is [`https://app.singular.live/apiv1`](https://app.singular.live/apiv1)

This documentation is open source. If you’ve found any errors, typos or would like to improve this document, 
feel free to send us requests and comments to [`sdk@singular.live`](mailto:sdk@singular.live).

**INFO:**
> Request/Response in Singular APIs is in JSON format. Request content-type must be application/json

## Table of Contents

1. **[Introduction](#introduction)**

1. **[Authentication](#authentication)**

1. **[Data Nodes](#data-nodes)**
   * [Resource Data Node](#resource-data-node)
   * [Get All Data Nodes](#get-all-data-nodes)
   * [Get one Data Node](#get-one-data-node)
   * [Get model and payload from Data Node](#get-model-and-payload-from-data-node)
   * [Create a Data Node](#create-a-data-node)
   * [Update metadata of a Data Node](#update-metadata-of-a-data-node)
   * [Delete a Data Node](#delete-a-data-node)

1. **[Web Channels](#web-channels)**
   * [Resource Web Channel](#resource-web-channel)
   * [Get All Web Channels](#get-all-web-channels)
   * [Get One Web Channel](#get-one-web-channel)
   * [Set a Composition to a Web Channel](#set-a-composition-to-a-web-channel)
   * [Get Control Parameters in from Web Channel](#get-control-parameters-in-from-web-channel)
   * [Control a Web Channel](#control-a-web-channel)
   * [Set a Composition to a Web Channel](#set-a-composition-to-a-web-channel)
   * [Set a Composition to a Web Channel](#set-a-composition-to-a-web-channel)

1. **[Errors](#errors)**

1. **[Getting Help](#getting-help)**

1. **[Questions & More Information Needed?](#questions-more-information-needed)**

## Authentication
Singular.Live uses [basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) over HTTPS but we will soon move to OAUTH2 for the authentication.
Singular.Live expects for the basic authentication to be included in all API requests to the server in a header.

To authorize, use this code:

```html
# With shell, you can just pass the correct header with each request
curl "https://app.singular.live/apiv1" -H "Authorization: TheAuthorisationComesHere"
```

## Data Nodes

### Resource Data Node
| Resources | Method | Represents |
| --------- | ------ |:---------- |
| /datanodes | GET |	Retrieve data nodes and data node data that belong to the authenticated user. |
| | POST | Create a new data node. |
| | PUT | Write data to a data node |
| | DELETE | Delete a data node |

### Get All Data Nodes

This endpoint retrieves all data nodes which belong to this authenticated user.

#### HTTP Request

| ``` GET https://app.singular.live/apiv1/datanodes/ ``` |
|:--------------------------------------------------:|

```html
curl https://app.singular.live/apiv1/datanodes 
```

The above command returns JSON structured like this:

```javascript
[
  {
    "id": 4,
    "account_id": 1,
    "user_id": 139,
    "is_deleted": 0,
    "fid": "root",
    "name": "Header",
    "firebaseUrl": "https://fiery-torch-2122.firebaseio.com/users/139/dataNodes/-KPZq2lIM1yVZLKr2SGM",
    "thumbnail": "images/defaultimage.png",
    "category": null,
    "created_at": "2016-08-19T22:07:30.000Z",
    "updated_at": "2016-08-19T22:07:30.000Z"
  },
  {
    "id": 3,
    "account_id": 1,
    "user_id": 139,
    "is_deleted": 0,
    "fid": "root",
    "name": "Hello",
    "firebaseUrl": "https://fiery-torch-2122.firebaseio.com/users/139/dataNodes/-KPZk4oOYnQqwrdSNiPf",
    "thumbnail": "images/defaultimage.png",
    "category": null,
    "created_at": "2016-08-19T21:41:25.000Z",
    "updated_at": "2016-08-19T21:54:07.000Z"
  }
]
```

### Get one Data Node

This endpoint retrieves a specific data node which belongs to this authenticated user.

#### HTTP Request

| ``` GET https://app.singular.live/apiv1/datanodes/<ID> ``` |
|:--------------------------------------------------:|

```html
curl https://app.singular.live/apiv1/datanodes/4
```

The above command returns JSON structured like this:

```javascript
{
  "id": 4,
  "account_id": 1,
  "user_id": 139,
  "is_deleted": 0,
  "fid": "root",
  "name": "Header",
  "firebaseUrl": "https://fiery-torch-2122.firebaseio.com/users/139/dataNodes/-KPZq2lIM1yVZLKr2SGM",
  "thumbnail": "images/defaultimage.png",
  "category": null,
  "created_at": "2016-08-19T22:07:30.000Z",
  "updated_at": "2016-08-19T22:07:30.000Z"
}
```

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the data node to retrieve|

### Get model and payload from Data Node

This endpoint retrieves a model and payload data of data node from specific data node which belong to this authenticated user.
HTTP Request

| ``` GET https://app.singular.live/apiv1/datanodes/<ID>/data ``` |
|:--------------------------------------------------:|

```html
curl https://app.singular.live/apiv1/datanodes/4/data
```

The above command returns JSON structured like this:

```javascript
{
  "model": {
    "fields": [
      {
        "defaultValue": "Title",
        "id": "title",
        "title": "title",
        "type": "text"
      },
      {
        "defaultValue": "Description",
        "id": "description",
        "title": "description",
        "type": "text"
      }
    ]
  },
  "payload": {
    "description": "Decription",
    "title": "Default title"
  }
}
```

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the data node to retrieve|

### Create a Data Node

This endpoint creates a new data node.

#### HTTP Request

| ``` POST https://app.singular.live/apiv1/datanodes ``` |
|:--------------------------------------------------:|

#### HTTP Request Body

The request body is key/value pairs of fields to create new data node.

#### HTTP Response

If success, the ID of created data node will be provided

```html
curl https://app.singular.live/apiv1/datanodes/4/data curl -H "Content-Type: application/json" -X POST -d
{
  "name": "Header",
  "folder": "root",
  "data": {
      "model": {
        "fields": [{
          "defaultValue": "Title",
          "id": "title",
          "title": "title",
          "type": "text"
        }, {
          "defaultValue": "Description",
          "id": "description",
          "title": "description",
          "type": "text"
        }]
      },
      "payload": {
        "title": "Default title",
        "description": "Decription"
      }
  },
  "thumbnail": "images/defaultimage.png"
}
https://app.singular.live/apiv1/datanodes
```

The above command returns JSON structured like this:

```javascript
{
  "id": 4,
  "account_id": 1,
  "user_id": 139,
  "is_deleted": 0,
  "fid": "root",
  "name": "Header",
  "firebaseUrl": "https://fiery-torch-2122.firebaseio.com/users/139/dataNodes/-KPZq2lIM1yVZLKr2SGM",
  "thumbnail": "images/defaultimage.png",
  "category": null,
  "created_at": "2016-08-19T22:07:30.000Z",
  "updated_at": "2016-08-19T22:07:30.000Z"
}
```

### Update metadata of a Data Node

This endpoint updates the metadata in a specific data node.

#### HTTP Request

| ``` PUT https://app.singular.live/apiv1/datanodes/<ID>/metadata ``` |
|:--------------------------------------------------:|

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the data node to update |

#### HTTP Request Body

The request body is key/value pairs of fields you would like to update in this data node.

#### HTTP Response

If success, ‘ok’ string will be returned

```html
curl -H "Content-Type: application/json" -X PUT -d
{
  "name": "New header",
  "thumbnail": "http://test.com/update.jpg"
}
https://app.singular.live/apiv1/datanodes/4/metadata
```

The above command returns JSON structured like this:

```javascript
"ok"
```

### Update model and payload in a Data Node

This endpoint updates a model or the payload of a specific data node.

#### HTTP Request

| ``` PUT https://app.singular.live/apiv1/datanodes/<ID>/data ``` |
|:--------------------------------------------------:|

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the data node to update |

#### HTTP Request Body

The request body is key/value pairs of fields you would like to update in this data node.

#### HTTP Response

If success, the updated data node including the model and payload.

```html
curl -H "Content-Type: application/json" -X PUT -d
{
  "model": {
    "fields": [{
      "defaultValue": "Title",
      "id": "title",
      "title": "title",
      "type": "text"
    }, {
      "defaultValue": "Description",
      "id": "description",
      "title": "description",
      "type": "text"
    }]
  },
  "payload": {
    "title": "Default title2",
    "description": "Decription2"
  }
}
https://app.singular.live/apiv1/datanodes/4/data
```

The above command returns JSON structured like this:

```javascript
{
  "model": {
    "fields": [
      {
        "defaultValue": "Title",
        "id": "title",
        "title": "title",
        "type": "text"
      },
      {
        "defaultValue": "Description",
        "id": "description",
        "title": "description",
        "type": "text"
      }
    ]
  },
  "payload": {
    "title": "Default title2",
    "description": "Decription2"
  },
  "id": "-KPZuIfHpWSydPAQxEzH"
}
```

### Delete a Data Node

This endpoint deletes a specific date node.

#### HTTP Request

| ``` DELETE https://app.singular.live/apiv1/datanodes/<ID> ``` |
|:--------------------------------------------------:|

```html
curl -H "Content-Type: application/json" -X DELETE -d https://app.singular.live/apiv1/datanodes/4
```

The above command returns JSON structured like this:

```javascript
{
    "status": "success"
}
```

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the data node to delete |

## Web Channels

### Resource Web Channel

| Resources | Method | Represents |
|:----------|:-------|:-----------|
| /webchannels | GET | Retrieve web channels and web channel details that belong to the authenticated user. |
| | PUT | Assign a composition and send control commands to a web channel |

### Get All Web Channels

This endpoint retrieves all web channels which belong to this authenticated user.

#### HTTP Request

```html
GET https://app.singular.live/apiv1/webchannels
```

```html
curl "https://app.singular.live/apiv1/webchannels"
```

The above command returns JSON structured like this:

```javascript
[{
  "id": 144,
  "user_id": 22,
  "name": "Channel B",
  "category": "",
  "created_at": "2016-03-28T14:24:17.000Z",
  "updated_at": "2016-03-28T14:24:17.000Z"
}, {
  "id": 143,
  "user_id": 22,
  "name": "Channel A",
  "category": "",
  "created_at": "2016-03-28T14:23:52.000Z",
  "updated_at": "2016-03-28T14:23:52.000Z"
}]
```

### Get one Web Channel

This endpoint retrieves a specific web channels which belong to this authenticated user.

#### HTTP Request

```html
GET https://app.singular.live/apiv1/webchannels(<ID>
```

```html
curl "https://app.singular.live/apiv1/webchannels/144"
```

The above command returns JSON structured like this:

```javascript
{
  "id": 144,
  "user_id": 22,
  "name": "Channel B",
  "category": "",
  "created_at": "2016-03-28T14:24:17.000Z",
  "updated_at": "2016-03-28T14:24:17.000Z"
}
```

#### URL Parameters:

|Parameter | Description |
|:---------|:------------|
| ID | The ID of the web channel to retrieve |

### Set a Composition to a Web Channel

This endpoint assigns a specific composition to a specific web channels which belong to this authenticated user.

#### HTTP Request

```html
PUT https://app.singular.live/apiv1/webchannels/<ID>/composition
```

```html
curl -H "Content-Type: application/json" -X POST -d
{
  "compositionId": "30"
}
https://app.singular.live/apiv1/webchannels/144/composition
```

The above command returns JSON structured like this:

```javascript
{
    "status": "success"
}
```

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the web channel to assign the composition to |

### Get Control Parameters in from Web Channel

This endpoint return available control nodes and animation state in a web channel.

#### HTTP Request

```html
GET https://app.singular.live/apiv1/webchannels/<ID>/control
```

```html
curl "https://app.singular.live/apiv1/webchannels/255/control"
```

The above command returns JSON structured like this:

```javascript
[
  {
    "compositionId": "-KLOVPujVBeo74oDJRQT",
    "animation": {
      "current": "Out1"
    }
  },
  {
    "compositionId": "-KM00xbzuqYqqhR2Ppkq",
    "animation": {
      "current": "In"
    },
    "controlNodes": {
      "model": [
        {
          "defaultValue": "Default Text",
          "id": "txLine1",
          "title": "txLine1",
          "type": "text"
        },
        {
          "defaultValue": "Default Text",
          "id": "txTitle",
          "title": "txTitle",
          "type": "text"
        }
      ],
      "payload": {
        "txLine1": "Line 1",
        "txTitle": "Title"
      }
    }
  },
  {
    "compositionId": "e53e506d-82e5-92d0-a9e5-bba7cfe0b4d9",
    "animation": {
      "current": "Out1"
    },
    "controlNodes": {
      "model": [
        {
          "defaultValue": "Default Text",
          "id": "txTitle",
          "title": "txTitle",
          "type": "text"
        }
      ],
      "payload": {
        "txTitle": "This is title"
      }
    }
  }
]
```

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the web channel |

### Control a Web Channel

Update animation state and control nodes in multiple compositions in a web channel.
Available actions in animation control are “play” and “jump”.

#### HTTP Request

```html
PUT https://app.singular.live/apiv1/webchannels/<ID>/control
```

```html
curl -H "Content-Type: application/json" -X PUT -d
[
  {
    "compositionId": "-KLOVPujVBeo74oDJRQT",
    "animation": {
      "action": "jump",
      "from": "In",
      "to": "Out1"
    }
  },
  {
    "compositionId": "-KM00xbzuqYqqhR2Ppkq",
    "animation": {
      "current": "In"
    },
    "controlNodes": {
      "payload": {
        "txLine1": "Line 1-1",
        "txTitle": "New title"
      }
    }
  },
  {
    "compositionId": "e53e506d-82e5-92d0-a9e5-bba7cfe0b4d9",
    "animation": {
      "action": "play",
      "from": "In",
      "to": "Out1"
    }
    "controlNodes": {
      "payload": {
        "txTitle": "This is new title"
      }
    }
  }
]
https://app.singular.live/apiv1/webchannels/255/control
```

The above command returns JSON structured like this:

```javascript

```

#### URL Parameters:

| Parameter | Description |
|:----------|:------------|
| ID | The ID of the web channel to update |
	
## Errors

The Singular.live REST API uses the folloeing error codes:

| Error Code | Return Message | Description |
|:----------:|:---------------|:------------|
| 200 | OK | Success
| 304 | Not Modified | There was no new data to return |
| 400 | Bad Request | The request was invalid. The accompanying error message provides detailed information |
| 401 | Unauthorized | Authentication credentials are missing or invalid |
| 404 | Not Found | The specified resource could not be found. Also returned when the requested format is not supported by the requested method. |
| 405 | Method Not Allowed | You tried to access a kitten with an invalid method |
| 500 | Internal Server Error | We had a problem with our server. Please try again later |
| 502 | Bad Gateway | Singular.Live is down or being upgraded |
| 503 | Service Unavailable | Singular.Live is up, but overloaded with requests. Please try again later |
		
Example of error response:

```javascript
{
    "error": {
        "message": "Message describing the error",
        "type": "Bad Request",
        "code": 400
    }
}
```

## Getting Help

- **Need help**? Ask a question to the [Singular Helpdesk](https://singularlive.zendesk.com/hc/en-us/requests/new).
- **Found a bug?** You can open a [GitHub issue](https://github.com/singularlive/singularplayer-samples/issues).

## Questions & More Information Needed?

Please contact our helpdesk, customers’ success or support team:

- Visit us at: [www.singular.live](http://www.singular.live)
- for helpdesk please contact: [helpdesk@singular.live](mailto:helpdesk@singular.live)
- for support please contact: [support@singular.live](mailto:support@singular.live)
- for sales please contact: [sales@singular.live](mailto:sales@singular.live)
- for general information: [info@singular.live](mailto:info@singular.live)
