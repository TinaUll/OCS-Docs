---


uid: AssetRulesAPI
---

# Asset Rules API

## Get Rule

Gets the specified rule

### Request

```
GET api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Response

The response includes a status code and a response body.

### Response body

The requested asset rule.

| Status Code               | Body Type  | Description                                                 |
| ------------------------- | ---------- | ----------------------------------------------------------- |
| 200 OK                    | Asset Rule | The asset rule with the requested identifier                |
| 403 Forbidden             | Error      | You are not authorized to retrieve the asset rule.          |
| 404 Not Found             | Error      | The asset rule with the requested identifier was not found. |
| 500 Internal Server Error | Error      | Internal server error.                                      |

### Example response body

```
{
    "Id": "id",
    "Name": "name",
    "Description": "description",
    "AutomationId": "automationId",
    "Expressions": [
        {
            "Field": "Id",
            "Specifications": [ { "Type": "Group", "Name": "streamId" } ]
        },
    ],
    "Outputs": [
        {
            "Field": "Asset",
            "Value": {
                "Id": "assetId",
                "Name": "assetName",
                "Description": "this is an asset generated by an asset rule",
                "Metadata": [],
                "StreamReferences": [],
                "MeasurementMappings": []
            }
        }
    ],
    "ValueMappings": {},
    "CreationTime": "2020-11-02T04:42:14.2727061",
    "ModifiedTime": "2020-11-02T04:42:14.2727061"
}
```

***

## Create Rule

Gets or creates a rule with the specified ID.

```
POST api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Request body

A serialized request body

### Response

The response includes a status code and response body.

| Status Code               | Body Type  | Description                                            |
| ------------------------- | ---------- | ------------------------------------------------------ |
| 200 OK                    | Asset Rule | The existing asset rule with the specified identifier. |
| 201 Created               | Asset Rule | The created asset rule with the specified identifier.  |
| 400 Bad Request           | Error      | Request is not valid.                                  |
| 403 Forbidden             | Error      | You are not authorized to retrieve the asset rule.     |
| 409 Conflict              | Error      | Another asset rule with the specified ID.              |
| 500 Internal Server Error | Error      | Internal server error.                                 |

***

## Create or Update Rule

Creates the specified rule. If a rule with the specified rule ID already exists, the rule definition is updated. 

### Request

```
PUT api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Request body

The serialized version of the created or updated asset rule.

### Response

The response includes a status code and a response body.

| Status Code               | Body Type  | Description                                           |
| ------------------------- | ---------- | ----------------------------------------------------- |
| 200 OK                    | Asset Rule | The updated asset rule with the specified identifier. |
| 201 Created               | Asset Rule | The created asset rule with the specified identifier. |
| 400 Bad Request           | Error      | Request is not valid.                                 |
| 403 Forbidden             | Error      | You are not authorized to retrieve the asset rule.    |
| 500 Internal Server Error | Error      | Internal server error.                                |

***

## Delete Rule

Deletes the specified rule

### Request

```
DELETE api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Response

The response includes a status code. 

| Status Code               | Body Type  | Description                                           |
| ------------------------- | ---------- | ----------------------------------------------------- |
| 204 No Content          | null | The specified rule was deleted |
| 404 Not Found           | Error      | The specified rule was not found.                                |
| 403 Forbidden             | Error      | You are not authorized to delete the asset rule.    |
| 500 Internal Server Error | Error      | Internal server error.                                |

***

## Execute Rule

Executes the specified rule

### Request

```
POST api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}/execute
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Response

The response includes a status code. 

| Status Code               | Body Type  | Description                                           |
| ------------------------- | ---------- | ----------------------------------------------------- |
| 204 No Content          | null | The specified rule was executed |
| 404 Not Found           | Error      | The specified rule was not found.                                |
| 403 Forbidden             | Error      | You are not authorized to delete the asset rule.    |
| 409 Conflict             | Error      | The automation id associated with the rule was invalid.    |
| 500 Internal Server Error | Error      | Internal server error.                                |

***

## Search Rules

Gets all asset rules that the requesting identity has access to

### Request

```
GET api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

### Response

The response includes a status code and response body.

| Status Code               | Body Type | Description                                               |
| ------------------------- | --------- | --------------------------------------------------------- |
| 200 OK                    | Rule List | List of rules that the requesting identity has access to. |
| 400 Bad Request           | Error     | Invalid query parameters.                                 |
| 403 Forbidden             | Error     | You are not authorized to retrieve rules.                 |
| 500 Internal Server Error | Error     | Internal server error.                                    |

***

## Get Rule ACL

Gets the Access Control List (ACL) of the specified rule.

### Request

```
GET api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}/accesscontrol
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Response

The response includes a status code and a response body.

| Status Code               | Body Type         | Description                                    |
| ------------------------- | ----------------- | ---------------------------------------------- |
| 200 OK                    | AccessControlList | The Access Control List of the specified rule. |
| 403 Forbidden             | Error             | You are not authorized to retrieve the ACL.    |
| 404 Not Found             | Error             | The specified rule ID was not found.           |
| 500 Internal Server Error | Error             | Internal server error.                         |

***

## Set Rule ACL

Sets the Access Control List (ACL) of the specified rule

### Request

```
PUT api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}/accesscontrol
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Request Body

```
{   "RoleTrusteeAccessControlEntries": [
     {
         "Trustee": {
             "Type": 3,
             "ObjectId": "sampleObjectId"
         },
         "AccessType: 0,
         "AccessRights": 15
     }
]}

```

### Response 

The response includes a status code and a response body.

| Status Code               | Body Type         | Description                                    |
| ------------------------- | ----------------- | ---------------------------------------------- |
| 200 OK                    | AccessControlList | The Access Control List of the specified rule. |
| 400 Bad Request           | Error             | Specified ACL is invalid.                      |
| 403 Forbidden             | Error             | You are not authorized to set the ACL.         |
| 404 Not Found             | Error             | The specified rule ID was not found.           |
| 500 Internal Server Error | Error             | Internal server error.                         |

***

## Get Access Rights

Gets a list of the common access rights that the identity, who is making the request, has on the specified rule 

### Request

```
GET api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}/accessrights
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Response

The response includes a status code and a response body.

| Status Code               | Body Type   | Description                                                  |
| ------------------------- | ----------- | ------------------------------------------------------------ |
| 200 OK                    | String List | Access rights on the specified rule for the requesting identity. |
| 403 Forbidden             | Error       | You are not authorized to get the access rights.             |
| 404 Not Found             | Error       | The specified rule ID was not found.                         |
| 500 Internal Server Error | Error       | Internal server error.                                       |

***

## Get Rule Owner

Gets the owner of the specified rule

### Request

```
GET api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}/owner
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Response

The response includes a status code and a response body.

### Response body

| Status Code               | Body Type | Description                                   |
| ------------------------- | --------- | --------------------------------------------- |
| 200 OK                    | Trustee   | The owner of the specified rule.              |
| 403 Forbidden             | Error     | You are not authorized to get the rule owner. |
| 404 Not Found             | Error     | The specified rule ID was not found.          |
| 500 Internal Server Error | Error     | Internal server error.                        |

***

## Set Rule Owner 

Changes the owner of the specified rule

### Request

```
PUT api/tenants/{tenantId}/namespaces/{namespaceId}/assetrules/{ruleId}/owner
```

### Parameters

`tenantID`

The tenant identifier

`namespaceId`

The namespace identifier

`ruleId`

The rule identifier

### Request body

The serialized Access Control List.

```
{
   "Type": 2,
   "TenantId": "tenantIdGuid",
   "ObjectId": "objectIdGuid"
}
```

### Response

The response includes a status code and a response body. 

| Status Code               | Body Type | Description                                          |
| ------------------------- | --------- | ---------------------------------------------------- |
| 200 OK                    | Trustee   | The new owner of the specified rule.                 |
| 400 Bad Request           | Error     | Specified owner is invalid.                          |
| 403 Forbidden             | Error     | You are not authorized to set the owner of the rule. |
| 404 Not Found             | Error     | The specified rule ID was not found.                 |
| 500 Internal Server Error | Error     | Internal server error.                               |
