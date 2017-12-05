---
title: Get file statistics API
description: Retrieves the prevalence for the given file.
keywords: apis, graph api, supported apis, get, file, statistics
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

# Get file statistics 
Retrieves the prevalence for the given file.

## Permissions
User needs read permissions.

## HTTP request
```
GET /testwdatppreview/files/{id}/stats
```

## Request headers

Header | Value 
:---|:---
Authorization | Bearer {token}. **Required**.
Content type | application/json


## Request body
Empty

## Response
If successful and file exists - 200 OK.
If file do not exist - 404 Not Found.


## Example

Request

Here is an example of the request.

```
GET https://graph.microsoft.com/testwdatppreview/files/{id}/machines
Content-type: application/json
```

Response

Here is an example of the response.


```
HTTP/1.1 200 OK
Content-type: application/json
{
    "@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#microsoft.windowsDefenderATP.api.InOrgFileStats",
    "sha1": "adae3732709d2178c8895c9be39c445b5e76d587",
    "orgPrevalence": "106398",
    "orgFirstSeen": "2017-07-30T13:29:50Z",
    "orgLastSeen": "2017-08-29T13:29:31Z",
    "topFileNames": [
        "chrome.exe",
        "old_chrome.exe"
    ]
}
```
