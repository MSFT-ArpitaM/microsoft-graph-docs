---
title: "Syntax for using the $filter OData query parameter"
description: "Learn how to use the $filter OData query parameter and its operators against different types of properties in Microsoft Graph."
author: "FaithOmbongi"
ms.localizationpriority: high
ms.custom: graphiamtop20, scenarios:getting-started
---

# Syntax for using the $filter OData query parameter

The following article demonstrates the syntax for using the `$filter` OData query parameter and its associated operators. The examples are provided for guidance only and do not reflect a comprehensive list for the application of `$filter`.

These examples show how to use `$filter` to match against supported properties and relationships that are primitive types, complex types, enumeration types, or a collection of one of these types.

> [!IMPORTANT]
> Examples marked with `*` are only supported with [advanced query capabilities](/graph/aad-advanced-queries).

<!-- To discuss: We don't use advanced query capabilities in these statements because these syntaxes should apply across all of Graph, not just directory. Will the asterisk be enough? --> 

## Apply $filter on single primitive types like String, Int, and dates

| Operator (s)           | Syntax                                                              |
|------------------------|---------------------------------------------------------------------|
| `eq`                   | `/users?$filter=userType eq 'Member'`                               |
| `not`                  | `/users?$filter=not userType eq 'Member'`*                          |
| `ne`                   | `/users?$filter=companyName ne null`*                               |
| `startsWith`           | `/users?$filter=startsWith(userPrincipalName, 'admin')`             |
| `endsWith`             | `/users?$count=true&$filter=endsWith(mail,'@outlook.com')`          |
| `in`                   | `/users?$filter=userType in ('Guest')`                              |
| `le`                   | `/devices?$filter=registrationDateTime le 2021-01-02T12:00:00Z`     |
| `ge`                   | `/devices?$filter=registrationDateTime ge 2021-01-02T12:00:00Z`     |
| `not` and `endsWith`   | `/users?$filter=NOT endsWith(mail, 'OnMicrosoft.com')&$count=true`* |
| `not` and `startsWith` | `/users?$filter=NOT startsWith(mail, 'A')&$count=true`()            |
| `not` and `eq`         | `/users?$filter=not(companyName eq 'Contoso E.A.')&$count=true`*    |
| `not` and `in`         | `/users?$filter=not (userType in ('Member'))&$count=true`*          |
| <!--| `contains`       | - | -->

## Apply $filter on a collection of primitive types

| Operator (s)                             | Syntax                                                                     |
|------------------------------------------|----------------------------------------------------------------------------|
| `eq`                                     | `/groups?$filter=groupTypes/any(c:c eq 'Unified')`                         |
| `not`                                    | `/groups?$filter=not groupTypes/any(c:c eq 'Unified')`*                    |
| `ne`                                     | `/users?$filter=companyName ne null`*                                      |
| `startsWith`                             | `/users?$filter=businessPhones/any(p:startsWith(p, '44 121'))`*            |
| `endsWith`                               | `/users?$filter=endsWith(mail,'@outlook.com')`*                            |
| `in`                                     | otherMails - how?                                                          |
| `le`                                     | `groups?$filter=createdOnBehalfOf/deletedDateTime le 2021-01-02T12:00:00Z` |
| `ge`                                     | `groups?$filter=createdOnBehalfOf/deletedDateTime ge 2021-01-02T12:00:00Z` |
| `gt`                                     |                                                                            |
| `lt`                                     |                                                                            |
| `any` and `eq`                           | `/groups?$filter=groupTypes/any(c:c eq 'Unified')`                         |
| `not` and `endsWith`                     | `/groups?$filter=NOT(endsWith(mail,'OnMicrosoft.com'))`*                   |
| `not` and `startsWith`                   | `$filter=NOT(startsWith(mail,'Pineview'))&$count=true`*                    |
| `not` and `eq`                           | `/groups?$filter=NOT(mail eq 'PineviewSchoolStaff@Contoso.com')`*          |
| `not` and `in`                           |                                                                            |
| `eq` and `$count` for empty collections  | `/users?$filter=assignedLicenses/$count eq 0`*                             |
| `ne` and `$count` for empty collections  | `/users?$filter=assignedLicenses/$count ne 0`*                             |
| `not` and `$count` for empty collections | `/users?$filter=NOT(assignedLicenses/$count ne 0)`*                        |
| <!--| `contains`       | - | -->

## Apply $filter on a GUID types

**RULE:** GUID values are not enclosed in quotes in `$filter` queries.

| Operator (s) | Syntax                                                                                            |
|--------------|---------------------------------------------------------------------------------------------------|
| `eq`         | `/servicePrincipals?$filter=appOwnerOrganizationId eq 72f988bf-86f1-41af-91ab-2d7cd011db47`*      |
| `not`        | `/servicePrincipals?$filter=NOT(appOwnerOrganizationId eq 72f988bf-86f1-41af-91ab-2d7cd011db47)`* |

## Apply $filter on a single complex type

| Operator (s) | Syntax                                                           |
|--------------|------------------------------------------------------------------|
| `eq`         |                                                                  |
| `le`         |                                                                  |
| `ge`         | `/users?$filter=manager/deletedDateTime ge 2021-01-02T12:00:00Z` |

## Apply $filter on a collection of a complex type

**RULE:** GUID values are not enclosed in quotes in `$filter` queries.

| Operator (s) | Syntax                                                                                            |
|--------------|---------------------------------------------------------------------------------------------------|
| `eq`         |  `/devices?$filter=alternativeSecurityIds/any(a:a/type ge 12345)`     |


## Apply $filter on a collection in a complex type

| Operator (s) | Syntax                                                                             |
|--------------|------------------------------------------------------------------------------------|
| `eq`         | `/users?$filter=authorizationInfo/certificateUserIds/any(x:x eq '9876543210@mil')` |
| `startsWith` | `/users?$filter=authorizationInfo/certificateUserIds/any(x:startswith(x,'987654321'))` |
| `endsWith`   | `/users?$filter=proxyAddresses/any(p:endsWith(p,'OnMicrosoft.com'))`* |
| `le`         |  |
| `ge`         | `/servicePrincipals?$filter=keyCredentials/any(k:k/endDateTime ge 2021-01-02T12:00:00Z)` |


## See also

+ [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries)

<!--## Use AND and OR clauses with multiple query strings in a $filter statement
<!-- Understand why the first query

https://graph.microsoft.com/v1.0/groups?$filter=(groupTypes/any(c:c eq 'Unified') and startswith(displayName, 'marketing')) or (mailEnabled eq false and securityEnabled eq true and startswith(displayName, 'marketing'))

returns this error:

```http
{
    "error": {
        "code": "Request_UnsupportedQuery",
        "message": "Search filter expression has excessive height: 4. Max allowed: 3.",
        "innerError": {
            "date": "2022-07-29T16:26:47",
            "request-id": "cc9fbc61-3c41-4982-a2cf-447285a6a821",
            "client-request-id": "de60367f-327a-5d3d-6ff7-7e370de14ee8"
        }
    }
}
```

And why this next query requires advanced query capabilities.


The following request includes the following expressions:
1. Find Microsoft 365 groups
2. Find groups that are not mail enabled but are security enabled
3. Find groups whose displayName starts with 'marketing'

The expressions are matched as follows: Find groups that match (1) or (2) above AND their displayName starts with 'marketing'.

https://graph.microsoft.com/v1.0/groups?$filter=(groupTypes/any(c:c eq 'Unified') or (mailEnabled eq false and securityEnabled eq true)) and startswith(displayName, 'marketing')&$count=true
ConsistencyLevel: eventual

-->