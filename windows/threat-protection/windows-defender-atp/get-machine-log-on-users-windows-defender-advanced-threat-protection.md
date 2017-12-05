---
title: Get machine log on users API
description: Retrieves a collection of logged on users.
keywords: apis, graph api, supported apis, get, machine, log on, users
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

# Get machine log on users 
Retrieves a collection of logged on users.

## Permissions
User needs read permissions.

## HTTP request
```
GET /testwdatppreview/machines/{id}/logonusers
```

## Request headers

Header | Value 
:---|:---
Authorization | Bearer {token}. **Required**.
Content type | application/json


## Request body
Empty

## Response
If successful and machine and user exist - 200 OK.
If no machine found or no users found - 404 Not Found.


## Example

Request

Here is an example of the request.

```
GET https://graph.microsoft.com/testwdatppreview/machines/{id}/logonusers
Content-type: application/json
```

Response

Here is an example of the response.


```
HTTP/1.1 200 OK
Content-type: application/json
 "@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#Users",
    "value": [
        {
            "id": "m",
            "accountSid": null,
            "accountName": "",
            "accountDomainName": "northamerica",
…
}
```
