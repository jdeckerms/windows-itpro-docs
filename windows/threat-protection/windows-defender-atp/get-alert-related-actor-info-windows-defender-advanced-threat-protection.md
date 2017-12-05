---
title: Get alert related actor information API
description: Retrieves the actor information related to the specific alert.
keywords: apis, graph api, supported apis, get, alert, actor, information, related
search.product: eADQiWindows 10XVcnh
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: macapara
author: mjcaparas
ms.localizationpriority: high
ms.date: 10/17/2017
---

# Get alert related actor information 
Retrieves the actor information related to the specific alert.

## Permissions
User needs read permissions.

## HTTP request
```
GET /testwdatppreview/alerts/{id}/actor
```

## Request headers

Header | Value 
:---|:---
Authorization | Bearer {token}. **Required**.
Content type | application/json


## Request body
Empty

## Response
If successful and alert and actor exist - 200 OK.
If alert not found or actor not found - 404 Not Found.


## Example

Request

Here is an example of the request.

```
GET https://graph.microsoft.com/testwdatppreview/alerts/{id}/actor
Content-type: application/json

```

Response

Here is an example of the response.


```
HTTP/1.1 200 OK
Content-type: application/json
{
    "@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#Actors/$entity",
    "id": "zinc",
    "linkToReport": "link-to-pdf"
}

```
