---
title: "Update wellKnownTaskList"
description: "Update the properties of a wellKnownTaskList object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
ms.localizationpriority: medium
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Update wellKnownTaskList
Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Update the properties of a [wellKnownTaskList](../resources/wellknowntasklist.md) object.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from least to most privileged)|
|:---|:---|
|Delegated (work or school account)|**TODO: Provide applicable permissions.**|
|Delegated (personal Microsoft account)|**TODO: Provide applicable permissions.**|
|Application|**TODO: Provide applicable permissions.**|

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
PATCH /user/tasks/lists/{wellKnownTaskListId}
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [wellKnownTaskList](../resources/wellknowntasklist.md) object.

The following table shows the properties that are required when you update the [wellKnownTaskList](../resources/wellknowntasklist.md).

|Property|Type|Description|
|:---|:---|:---|
|displayName|String|**TODO: Add Description** Inherited from [baseTaskList](../resources/basetasklist.md)|
|id|String|**TODO: Add Description** Inherited from [baseTaskList](../resources/basetasklist.md)|
|wellKnownListName|wellKnownListName_v2|**TODO: Add Description**. The possible values are: `none`, `defaultList`, `flaggedEmails`, `unknownFutureValue`.|



## Response

If successful, this method returns a `200 OK` response code and an updated [wellKnownTaskList](../resources/wellknowntasklist.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "update_wellknowntasklist"
}
-->
``` http
PATCH https://graph.microsoft.com/beta/user/tasks/lists/{wellKnownTaskListId}
Content-Type: application/json
Content-length: 121

{
  "@odata.type": "#microsoft.graph.wellKnownTaskList",
  "displayName": "String",
  "wellKnownListName": "String"
}
```


### Response
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true
}
-->
``` http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "@odata.type": "#microsoft.graph.wellKnownTaskList",
  "displayName": "String",
  "id": "748857e3-57e3-7488-e357-8874e3578874",
  "wellKnownListName": "String"
}
```
