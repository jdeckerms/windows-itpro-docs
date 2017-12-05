---
title: Get domain related machines API
description: Retrieves a collection of machines related to a given domain address.
keywords: apis, graph api, supported apis, get, domain, related, machines
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

# Get domain related machines
Retrieves a collection of machines related to a given domain address.

## Permissions
User needs read permissions.

## HTTP request
```
GET /testwdatppreview/domains/{id}/machines
```

## Request headers

Header | Value 
:---|:---
Authorization | Bearer {token}. **Required**.
Content type | application/json


## Request body
Empty

## Response
If successful and domain and machine exists - 200 OK.
If domain or machines do not exist - 404 Not Found.


## Example

Request

Here is an example of the request.

```
GET https://graph.microsoft.com/testwdatppreview/domains/{id}/machines
Content-type: application/json
```

Response

Here is an example of the response.


```
HTTP/1.1 200 OK
Content-type: application/json
{    
"@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#Machines",
    "value": [
        {
            "id": "0a3250e0693a109f1affc9217be9459028aa8426",
            "computerDnsName": "ComputerPII_4aa5f8f4509b90675a13183742f1b1ad67cf62b0.DomainPII_23208d0fe863968308c0c8e67dc0004bd1257631",
            "firstSeen": "2017-07-05T08:21:00.0572159Z",
            "osPlatform": "Windows10",
…
}
```
