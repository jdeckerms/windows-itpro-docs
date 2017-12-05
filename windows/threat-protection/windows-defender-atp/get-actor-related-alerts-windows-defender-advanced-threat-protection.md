---
title: Get actor related alerts API
description: Retrieves all alerts related to a given actor.
keywords: apis, graph api, supported apis, get, actor, related, alerts
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

# Get actor related alerts 
Retrieves all alerts related to a given actor.

## Permissions
User needs read permissions.

## HTTP request
```
GET /testwdatppreview/actor/{id}/alerts
```

## Request headers

Header | Value 
:---|:---
Authorization | Bearer {token}. **Required**.
Content type | application/json


## Request body
Empty

## Response
If successful and alert exists - 200 OK. 
If actor does not exist or no related alerts - 404 Not Found.


## Example

Request

Here is an example of the request.

```
GET https://graph.microsoft.com/testwdatppreview/actors/zinc/alerts
Content-type: application/json
```

Response

Here is an example of the response.


```
HTTP/1.1 200 OK
Content-type: application/json
{
    "@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#Alerts",
    "@odata.count": 3,
    "value": [
        {
            "id": "636390437845006321_-1646055784",
            "severity": "Medium",
            "status": "Resolved",
            "description": "Malware associated with ZINC has been detected.",
            "recommendedAction": "1.\tContact your incident response team.",
            "alertCreationTime": "2017-08-23T00:09:43.9057955Z",
            "category": "Malware",
            "title": "Malware associated with the activity group ZINC was discovered",
…
}
```
