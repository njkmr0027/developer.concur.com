
## Budget v4 - Budget Item


### Menu

* [Getting Started](#budget-v4-getting-started)
* [Fiscal Year](#budget-v4-fiscal-year-2020)
* [Budget Category](#budget-v4-budget-category)
* [Budget Item](#budget-v4-budget-item)
* [Budget Tracking Field](#budget-v4-budget-tracking)
* [Budget Adjustments](#budget-v4-budget-adjustments)


### Budget Item

This resource is used to retrieve and update information about a budget that spans a single fiscal year. Each budget has multiple details that correspond to fiscal periods - months, quarters, or a single period for a yearly budget.

* [GET All Budget Items](#get-all-budget-items)
* [GET a Budget Item](#get-a-budget-item)
* [POST a Budget Item](#post-a-budget-item)
* [DELETE a Budget Item](#delete-a-budget-item-header)
* [Schema](#budget-item-schema)
  * [Budget Item Header List](#budgetItemHeaderList)
  * [Budget Item Header](#budgetItemHeader)
  * [Budget Item Detail](#budgetItemDetail)
  * [Budget Amounts](#budgetAmounts)
  * [Budget Person](#budgetPerson)
  * [Budget Category](#budgetCategory)
  * [Expense Type](#expenseType)
  * [Budget Tracking Value](#budgetTrackingValue)
  * [Budget Item Balance](#budgetItemBalance)
  * [Fiscal Year](#budget-item-fiscalyear)
  * [Fiscal Period](#budget-item-fiscalperiod)
  * [Date Range](#dateRange)
  * [Budget Item Response](#budgetitemresponse)
  * [Error Response](#budget-item-error-response)
  * [Error Message](#budget-item-error-message)
* [Response Headers](#budget-item-response-headers)

### <a name="getall"></a>GET All Budget Items

Retrieve all budget items in groups of up to 50 items.  Due to response size and performance considerations, this endpoint does not return `budgetItemDetails`.  Use the [GET a Budget Item](#get) to retrieve all the details for a single budget.

### Scopes

This API call requires one of the following scopes:

* `budgetitem.read` - Refer to [Scope Usage](#budget-v4-getting-started) for full details.
* `budgetitem.write` - Refer to [Scope Usage](#budget-v4-getting-started) for full details.

### Request

#### URI
```shell
GET /budget/v4/budgetItemHeader
```

#### Template



#### Parameters

Name|Type|Format|Description
---|---|---|---
`adminView`|`boolean`|`query`|If `true`, returns all budgets for this entity, if `false`, returns only the budgets owned by the current user. Default:  `false`
`offset`|`integer`|`query`|The start of the page offset.  Default: `0`

#### Headers

* [RFC 7235 Authorization](https://tools.ietf.org/html/rfc7235#section-4.2)
* [RFC 7231 Content-Type](https://tools.ietf.org/html/rfc7231#section-3.1.1.5)

### Response

#### Status Codes

* [200 OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) Successful call, response is in body.
* [400 Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) The request was determined to be invalid by the server.
* [403 Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) The user does not have the necessary permissions to perform the request.
* [500 Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1) Error message in response body.
* [504 Gateway Timeout](https://tools.ietf.org/html/rfc7231#section-6.6.5) Error message in response body.

#### Headers

[Response Headers](#responseHeaders)

#### Payload

[Budget Item Header List](#budgetItemHeaderList)

### Example
```http
GET https://us.api.concursolutions.com/budget/v4/budgetItemHeader
Authorization: Bearer {token}
Accept: application/json
```

#### Request
```http
HTTP/1.1 200 OK
Cache-Control: max-age=604800
Content-Type: application/json
Date: Wed, 06 Jul 2020 17:33:03 GMT
Etag: "359670651"
Expires: Wed, 13 Jul 2020 17:33:03 GMT
Last-Modified: Fri, 09 Aug 2020 23:54:35 GMT
Content-Length: 1270
concur-correlationid: dd6cee88-b725-4c06-9ee9-0ca4ae4f16b2
```


#### Response



```json
{
  "totalRows":122,"offset":0,"limit":50,
  "budgetItemHeaders":[
    {
        "name":"Marketing-US-Jean Normandy",
        "isTest":false,
        "budgetItemStatusType":"OPEN",
        "description":"Marketing-US",
        "id":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "costObjects":[
         {
          "code": "6",
          "fieldDefinitionId": "86eee673-3d81-49c2-966a-b63c7a9302e2",
          "value": "2",
          "listKey": "1334",
          "operator": "EQUAL",
          "displayName": "Country Code"
        }
        ],
        "periodType":"YEARLY",
        "active":true,
        "owned":false,
        "budgetAmounts":{
          "pendingAmount":1178.37697091,
          "unExpensedAmount":2310.73578092,
          "spendAmount":35.78378912,
          "adjustedBudgetAmount": 0,
          "availableAmount":8785.83923997,
          "unExpensedSettings":null,
          "threshold":"UNDER",
          "consumedPercent":12
        },
        "createdDate": "2019-06-26T17:49:53.102Z",
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"EUR",
        "annualBudget":10000.00000000,
        "budgetCategory":{
          "name":"airfare",
          "description":null,
          "statusType":"OPEN",
          "id":"27451c2d-9121-44bd-b4b0-f2119d2071c7"
        },
        "owner":{
          "externalUserCUUID":"8002250890004822936",
          "employeeUuid":"210fe25f-e326-495c-847a-de333173f616",
          "id":"f779261d-77ce-4123-b739-d842ef6f104d",
          "name":"Jean Normandy",
          "email":"jean.normandy@xyz.com",
          "employeeId":"jean.normandy"
         },
        "budgetApprovers":[
	      {
            "externalUserCUUID":"8002250890004822936",
            "employeeUuid":"210fe25f-e326-495c-847a-de333173f616",
            "id":"f779261d-77ce-4123-b739-d842ef6f104d",
            "name":"Jean Normandy",
            "email":"jean.normandy@xyz.com",
            "employeeId":"jean.normandy"
          }
        ],
        "budgetManagers":[
	      {
            "externalUserCUUID":"1563846384638464842",
            "employeeUuid":"13a13839-68d6-4ee8-90e9-58604278aa8f",
            "id":"e2bae688-e000-464a-8728-e1362c94f172",
            "name":"Walter Gupta",
            "email":"walter.gupta@xyz.com",
            "employeeId":"walter.gupta"
          }
        ],
        "budgetType": "PERSONAL_USE",
        "budgetViewers":[
          {
            "externalUserCUUID":"5005380230004873464",
            "employeeUuid":"eb6082b0-3a9a-4e79-a350-e6e067f34969",
            "id":"7ce7dfe0-6168-4b93-bb35-386bf023acc6",
            "name":"Dan Lee",
            "email":"dan.lee@xyz.com",
            "employeeId":"dan.lee"
          }
        ],
        "dateRange": null,
        "fiscalYear":{
          "name":"2017",
          "displayName":"2017",
          "startDate":"2017-01-01",
          "endDate":"2017-12-31",
          "status":"OPEN",
          "id":"a4f9d57f-14ac-4f03-b5aa-4256e5cff790",
          "lastModified":"2017-03-26 20:53:19",
          "currentYear":false
        }
      },
    {"Additional budget item headers removed for brevity":"Additional budget items headers removed for brevity"}
  ],
  "href":"https://us.api.concursolutions.com/budget/v1.1/budgetItemHeader/?offset=0",
  "next":{
    "href":"http://budget-service-rqa3-budget.us-west-2.nonprod.cnqr.delivery/budget/v1.1/budgetItemHeader/?adminView=true&offset=50"
  },
  "previous":null
}
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

### <a name="get"></a>GET a Budget Item

Retrieve the details of a single budget item.

### Scopes

This API call requires one of the following scopes:

* `budgetitem.read` - Refer to [Scope Usage](#budget-v4-getting-started) for full details.
* `budgetitem.write` - Refer to [Scope Usage](#budget-v4-getting-started) for full details.

### Request


#### URI

```shell
GET  /budget/v4/budgetItemHeader/{id}
```

#### Template


#### Parameters

Name|Type|Format|Description
---|---|---|---
`id`|`string`|`uuid`|The budget item header's key field.

#### Headers

* [RFC 7235 Authorization](https://tools.ietf.org/html/rfc7235#section-4.2)
* [RFC 7231 Content-Type](https://tools.ietf.org/html/rfc7231#section-3.1.1.5)

### Response

#### Status Codes

* [200 OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) Successful call, response is in body.
* [400 Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) The request was determined to be invalid by the server.
* [403 Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) The user does not have the necessary permissions to perform the request.
* [404 Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) The resource could not be found or does not exist.
* [500 Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1) Error message in response body.
* [504 Gateway Timeout](https://tools.ietf.org/html/rfc7231#section-6.6.5) Error message in response body.

#### Headers

[Response Headers](#responseHeaders)

#### Payload

[Budget Item Header](#budgetItemHeader)

### Example
```http
GET https://us.api.concursolutions.com/budget/v4/budgetItemHeader/72eee673-3d81-49c2-966a-b63c7a9302e6
Authorization: Bearer {token}
```
#### Request
```http
HTTP/1.1 200 OK
Cache-Control: max-age=604800
Content-Type: application/json
Date: Wed, 06 Jul 2020 17:33:03 GMT
Etag: "359670651"
Expires: Wed, 13 Jul 2020 17:33:03 GMT
Last-Modified: Fri, 09 Aug 2020 23:54:35 GMT
Content-Length: 1270
concur-correlationid: 918cfb55-06a1-47da-8ef1-774a45427af9
```


#### Response



```json
 {
    "name":"Marketing-US-Jean Normandy",
    "isTest":false,
    "budgetItemStatusType":"OPEN",
    "description":"Marketing-US",
    "id":"72eee673-3d81-49c2-966a-b63c7a9302e6",
    "costObjects":[
     {
          "code": "6",
          "fieldDefinitionId": "86eee673-3d81-49c2-966a-b63c7a9302e2",
          "value": "2",
          "listKey": "1334",
          "operator": "EQUAL",
          "displayName": "Country Code"
        }
    ],
    "periodType":"QUARTERLY",
    "active":true,
    "owned":false,
    "budgetAmounts":{
      "pendingAmount":6870.48165307,
      "unExpensedAmount":102126.89000000,
      "spendAmount":764.86966050,
      "adjustedBudgetAmount": 0,
      "availableAmount":2364.64868643,
      "unExpensedSettings":null,
      "threshold":"UNDER",
      "consumedPercent":76
    },
    "createdDate": "2019-06-26T17:49:53.102Z",
    "currencyCode":"EUR",
    "annualBudget":10000.00000000,
    "budgetCategory":null,
    "owner":{
      "externalUserCUUID":"8002250890004822936",
      "employeeUuid":"210fe25f-e326-495c-847a-de333173f616",
      "id":"f779261d-77ce-4123-b739-d842ef6f104d",
      "name":"Jean Normandy",
      "email":"jean.normandy@xyz.com",
      "employeeId":"jean.normandy"
     },
    "budgetApprovers":[
       {
        "externalUserCUUID":"8002250890004822936",
        "employeeUuid":"210fe25f-e326-495c-847a-de333173f616",
        "id":"f779261d-77ce-4123-b739-d842ef6f104d",
        "name":"Jean Normandy",
        "email":"jean.normandy@xyz.com",
        "employeeId":"jean.normandy"
       }
    ],
    "budgetManagers":[
      {
        "externalUserCUUID":"1563846384638464842",
        "employeeUuid":"13a13839-68d6-4ee8-90e9-58604278aa8f",
        "id":"e2bae688-e000-464a-8728-e1362c94f172",
        "name":"Walter Gupta",
        "email":"walter.gupta@xyz.com",
        "employeeId":"walter.gupta"
      }
    ],
    "budgetType": "PERSONAL_USE",
    "budgetViewers":[
      {
        "externalUserCUUID":"5005380230004873464",
        "employeeUuid":"eb6082b0-3a9a-4e79-a350-e6e067f34969",
        "id":"7ce7dfe0-6168-4b93-bb35-386bf023acc6",
        "name":"Dan Lee",
        "email":"dan.lee@xyz.com",
        "employeeId":"dan.lee"
      }
    ],
    "budgetItemDetails":[
      {
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"USD",
        "amount":2500.00000000,
        "id":"4c165d40-804f-4aaa-b900-a46538537f6a",
        "budgetItemDetailStatusType":"OPEN",
        "budgetAmounts":{
          "pendingAmount":6870.48165307,
          "unExpensedAmount":102126.89000000,
          "spendAmount":764.86966050,
          "adjustedBudgetAmount": 0,
          "availableAmount":-5135.35131357,
          "unExpensedSettings":null,
          "consumedPercent":305,
          "threshold":"OVER"
        },
        "detailDashboardBudgetItemAdjustmentDTOs": [
          {
            "adjustmentType": "BUDGET_BALANCE",
            "amount": 0,
            "amountType": "QUICK_EXPENSE",
            "description": "string",
            "transactionDate": "2019-06-26"
          }
        ],
        "fiscalPeriod":{
          "name":"2017 - Q1",
          "fiscalPeriodStatus":"OPEN",
          "id":"b9659f8a-4e74-4531-9e23-1222ab1507f2",
          "periodType":"QUARTERLY",
          "startDate":"2017-01-01",
          "endDate":"2017-03-31",
          "spendDate":null,
          "fiscalYearId":"bcb41c95-2d53-4a1a-830f-7c6b01fa79da",
          "currentPeriod":false
        },
        "budgetItemBalances":[
          {
            "featureTypeCode":"PURCHASE_REQUEST",
            "featureTypeSubCode":"NONE",
            "workflowState":"SUBMITTED",
            "amount":6870.48165307,
            "id":"11cb732e-cbc4-41cb-82be-162d632d5499"
          },
          {
            "featureTypeCode":"EXPENSE",
            "featureTypeSubCode":"NONE",
            "workflowState":"PAID",
            "amount":764.86966050,
            "id":"0f09cc65-b879-4969-a8a1-9dd52c96486d"
          },
          {
            "featureTypeCode":"EXPENSE",
            "featureTypeSubCode":"ERECEIPTS",
            "workflowState":"UNSUBMITTED",
            "amount":102126.89000000,
            "id":"27c49c8a-c24d-42eb-b089-84268350ae03"
          }
        ]
      },
      {
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"EUR",
        "amount":2500.00000000,
        "id":"0a2dc181-389e-4c85-bb57-e4f1a11ace4e",
        "budgetItemDetailStatusType":"OPEN",
        "budgetAmounts":{
          "pendingAmount":0,
          "unExpensedAmount":0,
          "spendAmount":0,
          "adjustedBudgetAmount": 0,
          "availableAmount":2500.00000000,
          "unExpensedSettings":null,
          "consumedPercent":0,
          "threshold":"UNDER"
        },
        "detailDashboardBudgetItemAdjustmentDTOs": [
          {
            "adjustmentType": "BUDGET_BALANCE",
            "amount": 0,
            "amountType": "QUICK_EXPENSE",
            "description": "string",
            "transactionDate": "2019-06-26"
          }
        ],
        "fiscalPeriod":{
          "name":"2017 - Q2",
          "fiscalPeriodStatus":"OPEN",
          "id":"590d4e22-40be-43cc-ac1b-01b0d0263e19",
          "periodType":"QUARTERLY",
          "startDate":"2017-04-01",
          "endDate":"2017-06-30",
          "spendDate":null,
          "fiscalYearId":"bcb41c95-2d53-4a1a-830f-7c6b01fa79da",
          "currentPeriod":true
        },
        "budgetItemBalances":[]
      },
      {
        "Additional budget item details removed for brevity": "Additional budget item details removed for brevity"
      }
    ],
    "dateRange": null,
    "fiscalYear":{
      "name":"2017",
      "displayName":"2017",
      "startDate":"2017-01-01",
      "endDate":"2017-12-31",
      "status":"OPEN",
      "id":"a4f9d57f-14ac-4f03-b5aa-4256e5cff790",
      "lastModified":"2017-03-26 20:53:19",
      "currentYear":false,
      "monthlyFiscalPeriods":[
        {
          "name":"2017-Special - Jan",
          "fiscalPeriodStatus":"OPEN",
          "periodType":"MONTHLY",
          "startDate":"2017-01-01",
          "endDate":"2017-01-31",
          "id":"1929d1d9-6c99-4635-9272-508364193f8f",
          "spendDate":null,
          "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
          "currentPeriod":false
        },
        {
          "name":"2017-Special - Feb",
          "fiscalPeriodStatus":"OPEN",
          "periodType":"MONTHLY",
          "startDate":"2017-02-01",
          "endDate":"2017-02-28",
          "id":"41aa7452-e52a-4fd6-9c8a-5b199edeadaf",
          "spendDate":null,
          "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
          "currentPeriod":false
        },
        {
          "name":"2017-Special - Mar",
          "fiscalPeriodStatus":"OPEN",
          "periodType":"MONTHLY",
          "startDate":"2017-03-01",
          "endDate":"2017-03-31",
          "id":"6c7d0b13-96b9-4d76-a083-4d38c96144e2",
          "spendDate":null,
          "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
          "currentPeriod":false
        }
      ],
      "quarterlyFiscalPeriods":[
        {
          "name":"2017-Special - Q1",
          "fiscalPeriodStatus":"OPEN",
          "id":"5ce25dfd-8b2b-4fea-91eb-f8f9ad0bb896 ",
          "periodType":"QUARTERLY",
          "startDate":"2017-01-01",
          "endDate":"2017-03-31",
          "spendDate":null,
          "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
          "currentPeriod":false
        },
        {
        "name":"2017-Special - Q2",
        "fiscalPeriodStatus":"OPEN",
        "id":"5ce25dfd-8b2b-4fea-91eb-f8f9ad0bb896 ",
        "periodType":"QUARTERLY",
        "startDate":"2017-04-01",
        "endDate":"2017-06-30",
        "spendDate":null,
        "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
        "currentPeriod":false
      },
      {
        "name":"2017-Special - Q3",
        "fiscalPeriodStatus":"OPEN",
        "id":"5ce25dfd-8b2b-4fea-91eb-f8f9ad0bb896 ",
        "periodType":"QUARTERLY",
        "startDate":"2017-07-01",
        "endDate":"2017-09-30",
        "spendDate":null,
        "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
        "currentPeriod":false
      },
      {
        "name":"2017-Special - Q4",
        "fiscalPeriodStatus":"OPEN",
        "id":"5ce25dfd-8b2b-4fea-91eb-f8f9ad0bb896 ",
        "periodType":"QUARTERLY",
        "startDate":"2017-10-01",
        "endDate":"2017-12-31",
        "spendDate":null,
        "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
        "currentPeriod":false
      }
      ],
      "yearlyFiscalPeriods":[
        {
          "name":"2017-Special",
          "fiscalPeriodStatus":"OPEN",
          "id":"a6bede66-4f3d-412f-a620-2a073013cb2a",
          "periodType":"YEARLY",
          "startDate":"2017-01-01",
          "endDate":"2017-12-31",
          "spendDate":null,
          "fiscalYearId":"2edd7bd4-8f10-46e5-bf52-d553f6c7df80",
          "currentPeriod":false
        }
      ],
      "customFiscalPeriods":[],
    }
  }
```
<br>
<br>
<br>
<br>

### <a name="post"></a>POST a Budget Item

Save a new budget or update an existing budget.

### Scopes

`budgetitem.write` - Refer to [Scope Usage](#budget-v4-getting-started) for full details.

### Request

#### URI

#### Template

```http
POST  /budget/v4/budgetItemHeader
```

#### Parameters

N/A

#### Headers

* [RFC 7235 Authorization](https://tools.ietf.org/html/rfc7235#section-4.2)
* [RFC 7231 Content-Type](https://tools.ietf.org/html/rfc7231#section-3.1.1.5)

#### Payload

[Budget Item Header](#budgetItemHeader)

### Response

#### Status Codes

* [200 OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) Successful call, response is in body.
* [400 Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) The request was determined to be invalid by the server. Possibly a validation failed on the data that was sent in the payload. The response will have a list of validation errors in the body. See below for an example 400 response.
* [403 Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) The user does not have the necessary permissions to perform the request.
* [404 Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) The resource could not be found or does not exist.
* [500 Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1) Error message in response body.
* [504 Gateway Timeout](https://tools.ietf.org/html/rfc7231#section-6.6.5) Error message in response body.

#### Headers

[Response Headers](#responseHeaders)

#### Payload

[Budget Item Response](#budgetItemResponse) or [Error Response](#errorResponse)

### Example
```http
POST https://us.api.concursolutions.com/budget/v4/budgetItemHeader
Authorization: Bearer {token}
```
#### Request



#### Quarterly Budget Example
```json
  {
    "name":"Marketing-US-Jean Normandy",
    "isTest":false,
    "budgetItemStatusType":"OPEN",
    "description":"Marketing-US",
    "id":"72eee673-3d81-49c2-966a-b63c7a9302e6",
    "costObjects":[
      {
      "fieldDefinitionId":"86eee673-3d81-49c2-966a-b63c7a9302e2",
      "code": "6",
      "value": "2",
      "listKey": "1334",
      "operator": "EQUAL",
      "displayName":"Country Code"
    }
    ],
    "periodType":"QUARTERLY",
    "currencyCode":"EUR",
    "budgetCategory":{
      "id":"27451c2d-9121-44bd-b4b0-f2119d2071c7"
    },
    "owner":{
      "externalUserCUUID":"8002250890004822936",
      "employeeUuid":"210fe25f-e326-495c-847a-de333173f616",
      "email":"jean.normandy@xyz.com",
      "employeeId":"jean.normandy"
     },
    "budgetApprovers":[
      {
        "externalUserCUUID":"5005380230004873464",
        "employeeUuid":"eb6082b0-3a9a-4e79-a350-e6e067f34969",
        "email":"dan.lee@xyz.com",
        "employeeId":"dan.lee"
      }
    ],
    "budgetManagers":[
      {
        "externalUserCUUID":"1563846384638464842",
        "employeeUuid":"13a13839-68d6-4ee8-90e9-58604278aa8f",
        "email":"walter.gupta@xyz.com",
        "employeeId":"walter.gupta"
      }
    ],
    "budgetType": "PERSONAL_USE",
    "budgetViewers":[
      {
        "externalUserCUUID":"5005380230004873464",
        "employeeUuid":"eb6082b0-3a9a-4e79-a350-e6e067f34969",
        "email":"dan.lee@xyz.com",
        "employeeId":"dan.lee"
      }
    ],
    "budgetItemDetails":[
      {
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"EUR",
        "amount":2500.00000000,
        "id":"4c165d40-804f-4aaa-b900-a46538537f6a",
        "budgetItemDetailStatusType":"OPEN",
        "fiscalPeriod":{
          "id":"b9659f8a-4e74-4531-9e23-1222ab1507f2"
        }
      },
      {
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"EUR",
        "amount":2500.00000000,
        "id":"0a2dc181-389e-4c85-bb57-e4f1a11ace4e",
        "budgetItemDetailStatusType":"OPEN",
        "fiscalPeriod":{
          "id":"590d4e22-40be-43cc-ac1b-01b0d0263e19"
        }
      },
      {
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"EUR",
        "amount":2500.00000000,
        "id":"35d7dc8a-5ec8-4d5f-ba7c-d9304f7afee3",
        "budgetItemDetailStatusType":"OPEN",
        "fiscalPeriod":{
          "id":"09cd5be1-a21d-47f2-b6b5-8d9019709327"
        }
      },
      {
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"EUR",
        "amount":2500.00000000,
        "id":"4ec30f7c-e7fa-4832-9134-85bed9a85b9c",
        "budgetItemDetailStatusType":"OPEN",
        "fiscalPeriod":{
          "id":"c3beec03-a096-4a33-b7af-b49127742702"
        }
      }
    ],
    "fiscalYear":{
      "id":"a4f9d57f-14ac-4f03-b5aa-4256e5cff790"
    }
  }
```

#### Date Range Budget Example
```json
  {
    "name":"Marketing-US-Jean Normandy Date Range",
    "isTest":false,
    "budgetItemStatusType":"OPEN",
    "description":"Marketing-US",
    "id":"72eee673-3d81-49c2-966a-b63c7a9302e6",
    "costObjects":[
     {
      "code": "6",
      "fieldDefinitionId": "86eee673-3d81-49c2-966a-b63c7a9302e2",
      "value": "2",
      "listKey": "1334",
      "operator": "EQUAL",
      "displayName": "Country Code"
    }
    ],
    "periodType":"DATE_RANGE",
    "currencyCode":"EUR",
    "budgetCategory":{
      "id":"27451c2d-9121-44bd-b4b0-f2119d2071c7"
    },
    "owner":{
      "externalUserCUUID":"8002250890004822936",
      "employeeUuid":"210fe25f-e326-495c-847a-de333173f616",
      "email":"jean.normandy@xyz.com",
      "employeeId":"jean.normandy"
     },
    "budgetApprovers":[
      {
        "externalUserCUUID":"5005380230004873464",
        "employeeUuid":"eb6082b0-3a9a-4e79-a350-e6e067f34969",
        "email":"dan.lee@xyz.com",
        "employeeId":"dan.lee"
      }
    ],
    "budgetManagers":[
      {
        "externalUserCUUID":"1563846384638464842",
        "employeeUuid":"13a13839-68d6-4ee8-90e9-58604278aa8f",
        "email":"walter.gupta@xyz.com",
        "employeeId":"walter.gupta"
      }
    ],
    "budgetType": "PERSONAL_USE",
    "budgetViewers":[
      {
        "externalUserCUUID":"5005380230004873464",
        "employeeUuid":"eb6082b0-3a9a-4e79-a350-e6e067f34969",
        "email":"dan.lee@xyz.com",
        "employeeId":"dan.lee"
      }
    ],
    "budgetItemDetails":[
      {
        "budgetItemHeaderId":"72eee673-3d81-49c2-966a-b63c7a9302e6",
        "budgetName":"Marketing-US-Jean Normandy",
        "currencyCode":"EUR",
        "amount":2500.00000000,
        "id":"4c165d40-804f-4aaa-b900-a46538537f6a",
        "budgetItemDetailStatusType":"OPEN",
        "fiscalPeriod":{
          "id":"b9659f8a-4e74-4531-9e23-1222ab1507f7"
        }
      }
    ],
    "fiscalYear":{
      "id":null
    }
  }
```

#### Response

#### Success Response

```http
HTTP/1.1 200 OK
Cache-Control: max-age=604800
Content-Type: application/json
Date: Wed, 06 Jul 2020 17:33:03 GMT
Etag: "359670651"
Expires: Wed, 13 Jul 2020 17:33:03 GMT
Last-Modified: Fri, 09 Aug 2020 23:54:35 GMT
Content-Length: 97
concur-correlationid: 809a0898-e523-4114-950d-bd22705a3b25
```

```json
  {
    "success": true,
    "budgetItemHeaderId": "72eee673-3d81-49c2-966a-b63c7a9302e6"
  }
```

#### Failure Response

```shell
HTTP/1.1 400 Bad Request
Cache-Control: no-store
Connection: close
Content-Length: 459
Content-Type: application/json;charset=utf-8
Date: Fri, 21 Sep 2018 15:27:05 GMT
Expires: Thu, 20 Sep 2018 15:27:05 GMT
Pragma: no-cache
concur-correlationid: cea62849-02e5-4a7f-a576-68280c84bd02
```

```json
{
  "status" : false,
  "errorMessageList" : [
    {
      "errorType" : "ERROR",
      "errorCode" : "BUDGET.BUDGET_ITEM_NAME_REQUIRED",
      "errorMessage" : "Budget item name is required"
    },
    {
      "errorType" : "ERROR",
      "errorCode" : "BUDGET.BUDGET_ITEM_NAME_ERROR",
      "errorMessage" : "Budget item name should be more than 1 characters"
    },
    {
      "errorType" : "ERROR",
      "errorCode" : "BUDGET.BUDGET_ITEM_OWNER_REQUIRED",
      "errorMessage" : "Budget item owner is required"
    }
  ]
}
```

#### <a name="delete"></a>DELETE a Budget Item Header

Delete a budget item.

### Scopes

`budgetitem.write` - Refer to [Scope Usage](#budget-v4-getting-started) for full details.

### Request

#### URI

#### Template

```http
DELETE  /budget/v4/budgetItemHeader/{id}
```

#### <a name="parameters"></a>Parameters

Name|Type|Format|Description
---|---|---|---
`id`|`string`|`path`|The budget item header's key field.

#### Headers

* [RFC 7235 Authorization](https://tools.ietf.org/html/rfc7235#section-4.2)
* [RFC 7231 Content-Type](https://tools.ietf.org/html/rfc7231#section-3.1.1.5)

### Response

#### Status Codes

* [200 OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) Successful call, response is in body.
* [400 Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) The request was determined to be invalid by the server.
* [403 Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) The user does not have the necessary permissions to perform the request.
* [404 Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) The resource could not be found or does not exist.
* [500 Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1) Error message in response body.
* [504 Gateway Timeout](https://tools.ietf.org/html/rfc7231#section-6.6.5) Error message in response body.

#### Headers

[Response Headers](#responseHeaders)

#### Payload

[Budget Item Response](#budgetItemResponse) or [Error Response](#errorResponse)

### Example

#### Request

```http
DELETE https://us.api.concursolutions.com/budget/v4/budgetItemHeader/72eee673-3d81-49c2-966a-b63c7a9302e6
Authorization: Bearer {token}
```

### Response

```shell
HTTP/1.1 200 OK
Cache-Control: no-store
Connection: keep-alive
Content-Length: 97
Content-Type: application/json;charset=utf-8
Date: Fri, 21 Sep 2018 15:24:27 GMT
Expires: Thu, 20 Sep 2018 15:24:27 GMT
Pragma: no-cache
Vary: Origin
concur-correlationid: 86a0d9fe-9e98-43c3-89d8-a2917dd844cb
```

```json
  {
    "success": true,
    "budgetItemHeaderId": "72eee673-3d81-49c2-966a-b63c7a9302e6"
  }

```

### <a name="schema"></a>Budget Item - Schema

#### <a name="budgetItemHeaderList"></a>PagedBudgetItemHeaderList

Name|Type|Format|Description
---|---|---|---
`totalRows`|`integer`|-|The total number of rows available.
`offset`|`integer`|-|The starting row for this page of results (zero-based).
`limit`|`integer`|-|The number of results returned per page. Maximum: `50`
`budgetItemHeaders`|`array`|[`budgetItemHeader`](#budgetItemHeader)|List of budget item headers. Each budget item header represents a single budget for a fiscal year.
`href`|`string`|-|The link to this page of results.
`previous`|`string`|`href`|The `href` for the previous page of results (`null` if this is the first page of results).
`next`|`string`|`href`|The `href` for the next page of results (`null` if no results remaining).


#### <a name="budgetItemHeader"></a>BudgetItemHeader

Name|Type|Format|Description
---|---|---|---
`active`|`boolean`|-|**READ ONLY** Indicates if this budget should be displayed on user screens.
`annualBudget`|`decimal`|-|**READ ONLY** The total budget amount and accumulated balances for this budget header.
`budgetAmounts`|`array`|[`budgetAmounts`](#budgetAmounts)|**READ ONLY** The accumulated budget amounts for this budget.
`budgetManagers`|`array`|[`budgetPerson`](#budgetPerson)|If managers exist, spend items only matches this budget if one of the managers is in the manager hierarchy of the submitter or approver for the given spend item.
`budgetApprovers`|`array`|[`budgetPerson`](#budgetPerson)|The workflow approvers for this budget.
`budgetCategory`|`array`|[`budgetCategory`](#budgetCategory)|The budget category for this budget item.  If a budget category is present, spending items must match one of the expense types in the budget category in order to match this budget.
`budgetItemDetails`|`array`|[`budgetItemDetail`](#budgetItemDetail)|**Required** Specify the budget information for each fiscal period in the fiscal year.
`budgetItemStatusType`|`string`|-|The status of this budget item. Supported values: `OPEN`, `CLOSED`(no spending can be attached to this budget), `REMOVED`
`budgetType`|`string`|-| The budget type indicates if the budget item is personal or not. Supported values: `PERSONAL_USE`, `BUDGET`, `RESTRICTED`
`budgetViewers`|`array`|[`budgetPerson`](#budgetPerson)|The users who can view this budget.
`costObjects`|`array`|[`budgetTrackingValue`](#budgetTrackingValue)|The cost object list for matching spending items.
`createdDate`|`date`|`YYYY-MM-DD`|**READ ONLY** The time the budget item header was created. Date in UTC.
`currencyCode`|`string`|-|The 3-letter ISO 4217 currency code for the budget currency. This is the currency code of the budget amount. Spending Items are converted using yesterday's closing value. Examples: `USD` - US dollars; `BRL` - Brazilian real; `CAD` - Canadian dollar; `CHF` - Swiss franc; `EUR` - Euro; `GBO` - Pound sterling; `HKD` - Hong Kong dollar; `INR` - Indian rupee; `MXN` - Mexican peso; `NOK` - Norwegian krone; `SEK` - Swedish krona.
`description`|`string`|-|**Required** The user-friendly name for this budget. This description is displayed to end users on desktop and mobile.
`dateRange`|`dateRange`|-|**READ ONLY** Specify custom date range for budget.
`fiscalYear`|`array`|[`fiscalYear`](#fiscalYear)|**Required** The fiscal year for this budget.  Only the ID of the fiscal year, which can be retrieved from the [Fiscal Year service](#/api-reference/budget/v4.fiscal-year.html), is required for creating/updating a budget.
`fiscalYearId`|`string`|-|The unique identifier of the fiscal year for this budget.
`id`|`string`|-|The key for this object.
`isTest`|`boolean`|-|The test flag for the budget item.  If `true`, this budget will only match spending submitted by test users.
`lastModifiedDate`|`dateRange`|-|**READ ONLY** The last time the budget item header was updated. Date in UTC.
`name`|`string`|-|**Required** The admin-facing name for this budget.
`owned`|`string`|-|**READ ONLY** A flag indicating if the current user is the owner of this budget.
`owner`|`array`|[`budgetPerson`](#budgetPerson)|**Required** The user who is ultimately responsible for this budget.
`periodType`|`string`|-|**READ ONLY** The type of period within the fiscal year that this budget's details use.


#### <a name="budgetItemDetail"></a>BudgetItemDetail

Name|Type|Format|Description
---|---|---|---
`amount`|`decimal`|-|**Required** The budget currency amount allocated to this fiscal period. May be zero.
`budgetAmounts`|`array`|[`budgetAmounts`](#budgetAmounts)|**READ ONLY** The accumulated budget numbers for this budget.
`budgetItemBalances`|`array`|[`budgetItemBalance`](#budgetItemBalance)|**READ ONLY** Shows the break-out of budget spending by product and workflow state.
`budgetItemDetailStatusType`|`string`|-|The status of this budget item. Supported values: `OPEN`, `CLOSED`(no spending can be attached to this budget), `REMOVED`
`currencyCode`|`string`|-|The 3-letter ISO 4217 currency code for the budget currency. Examples: `USD` - US dollars; `BRL` - Brazilian real; `CAD` - Canadian dollar; `CHF` - Swiss franc; `EUR` - Euro; `GBO` - Pound sterling; `HKD` - Hong Kong dollar; `INR` - Indian rupee; `MXN` - Mexican peso; `NOK` - Norwegian krone; `SEK` - Swedish krona.
`budgetName`|`string`|-|**READ ONLY** The admin-facing name of this budget.
`budgetItemHeaderId`|`string`|-|**READ ONLY** The unique ID of the header that contains this budget item detail.
`fiscalPeriod`|[`fiscalPeriod`](#fiscalPeriod) | - |**Required** The fiscal period for this budget amount. Only the ID of the fiscal period, which can be retrieved from the [Fiscal Year service](#/api-reference/budget/v4.fiscal-year.html), is required for creating/updating a budget.
`detailDashboardBudgetItemAdjustmentDTOs`|`array`|[`detailDashboardBudgetItemAdjustment`](#detailDashboardBudgetItemAdjustment) |**READ ONLY** List of budget adjustments.
`fiscalPeriod`|`array`|[`fiscalPeriod`](#fiscalPeriod)|**Required** The specific fiscal period when this budget amount will be used. Only the ID of the fiscal period, which can be retrieved from the [Fiscal Year service](#/api-reference/budget/v4.fiscal-year.html), is required for creating/updating a budget.


#### <a name="budgetAmounts"></a>BudgetAmounts

Name|Type|Format|Description
---|---|---|---
`adjustedBudgetAmount`|`decimal`|-|**READ ONLY** The amount adjusted against this budget.
`availableAmount`|`decimal`|-|**READ ONLY** The available amount accumulated against this budget. Uses budget setting to determine which amounts are included to calculate available amount.
`consumedPercent`|`decimal`|-|**READ ONLY** The percentage of the budget that is considered used. Uses budget setting to determine which amounts to include.
`pendingAmount`|`decimal`|-|**READ ONLY** The pending amount accumulated against this budget.
`spendAmount`|`decimal`|-|**READ ONLY** The spent amount accumulated against this budget.
`threshold`|`string`|-|**READ ONLY** The indicator of whether this budget is under the alert limit, equal to or over the alert limit but under the control limit, or equal to or over the control limit. Supported values: `UNDER`, `ALERT`, `OVER`
`unExpensedAmount`|`decimal`|-|**READ ONLY** The amount of unexpensed items like travel bookings, quick expenses, or e-receipts.
`unExpensedSettings`|`string`|-|**READ ONLY** The company's budget setting for unexpensed items. Applies to all budgets for the company. Supported values: `SHOW_UNSUBMITTED_EXPENSES_AS_PENDING`, `SHOW_UNSUBMITTED_EXPENSES_BALANCE`, `DO_NOT_SHOW_UNSUBMITTED_EXPENSES`

#### <a name="budgetPerson"></a>BudgetPerson

Provide externalUserCUUID or email or employee ID of the user for looking up the person.

Name|Type|Format|Description
---|---|---|---
`externalUserCUUID`|`string`|-|The unique identifier for this user. This must match the CUUID from SAP Concur's profile service.
`name`|`string`|-|**READ ONLY** The user's name. Provided for convenience.
`id`|`string`|-|The budget service's unique identifier for this user.
`email`|`string`|-|The email address of the person to lookup.
`employeeId`|`string`|-|**READ ONLY** The employee ID of the person to lookup.
`employeeUuid`|`string`|-|The unique identifier for this user.  This must match the UUID from SAP Concur's profile service.

#### <a name="budgetCategory"></a>BudgetCategory

Name|Type|Format|Description
---|---|---|---
`description`|`string`|-|The list of expense types that this budget category matches.
`name`|`string`|-|The admin-facing name for this category.
`statusType`|`string`|-|The status of this budget category. Supported values: `OPEN`, `REMOVED`
`id`|`string`|-|The unique identifier for the budget category.


#### <a name="expenseType"></a>ExpenseType

Name|Type|Format|Description
---|---|---|---
`featureTypeCode`|`string`|-|**Required** The product that this expense type applies to: Purchase Request, Invoice (Payment Request), Expense, or Request. Supported values: `PURCHASE_REQUEST`, `PAYMENT_REQUEST`, `EXPENSE`, `REQUEST`
`expenseTypeCode`|`string`|-|**Required** The alphanumeric code that describes an expense type. (Example: `MEALS`, `AC_CATER`) Valid expense type codes are returned by the GET /budgetCategory/expenseType method described in the [Budget Category service](#budget-v4-budget-category).
`name`|`string`|-|**READ ONLY** The name for this expense type if it maps to an expense type set up in your SAP Concur product(s).
`id`|`string`|-|The budget service's key for this object.


#### <a name="budgetTrackingValue"></a>BudgetTrackingValue

Name|Type|Format|Description
---|---|---|---
`code`|`string`|-|The code for the cost object field. This can be used instead of fieldDefinitionId and will take priority if populated. This value can be found for your budget tracking fields you have configured by using the GET All Budget Tracking Fields resource.
`value`|`string`|-|The value for the cost object field.  The value of this field will be ignored unless the operator field is `EQUAL`, `NOTEQUAL`, `INLIST`, or `NOTINLIST`. The value of this field can be one or more comma-separated values if the `INLIST` or `NOTINLIST` operator is chosen.
`listKey`|`string`|-|When setting up the budget, specify the `listKey` that maps to the value of this list in the SAP Concur list service.
`operator`|`string`|-| **Required** The comparison to use when matching values for this tracking field. Supported values: `EQUAL`, `INLIST`, `ISBLANK`, `NOTEQUAL`, `NOTINLIST`, `ISNOTBLANK`, `ISTRUE`, `ISFALSE`, `ISNOTTRUE`, `ISNOTFALSE`
`fieldDefinitionID`|`string`|-| **Required** The budget service’s key for this object’s field definition ID. This value can be found for your budget tracking fields you have configured by using the GET All Budget TrackingFields resource.
`displayName`|`string`|-| The budget field tracking name.


#### <a name="budgetItemBalance"></a>BudgetItemBalance

Name|Type|Format|Description
---|---|---|---
`amount`|`decimal`|-|**READ ONLY** The balance amount.
`featureTypeCode`|`string`|-|**READ ONLY** The product type for this balance. Supported values: `REQUEST`, `TRAVEL`, `EXPENSE`, `PAYMENT_REQUEST`
`featureTypeSubCode`|`string`|-|**READ ONLY** The feature type sub code for this balance. Supported values: `QUICK_EXPENSE`, `ERECEIPT`, `CREDIT_CARD`, `PERSONAL_CARD`, `TRIP`, `RECEIPT_CAPTURE`, `BILLING_STATEMENT`, `MANUAL`, `NONE`, `BUDGET_AMOUNT`, `SPENT_AMOUNT`, `PENDING_AMOUNT`, `PRE_AUTHORIZED`, `PURGE_ADJUSTMENT`
`workflowState`|`string`|-|**READ ONLY** Supported values: `UNSUBMITTED`, `UNSUBMITTED_HELD`, `SUBMITTED`, `APPROVED`, `PROCESSED`, `PAID`.
`id`|`string`|-|The unique identifier for this particular budget balance bucket..

#### <a name="fiscalYear"></a>Budget Item - FiscalYear

Name|Type|Format|Description
---|---|---|---
`currentYear`|`boolean`|-|**READ ONLY** If `true`, this is the current fiscal year based on the current date and time. `false`, if otherwise.
`startDate`|`date`|`YYYY-MM-DD`|**Required** The start date for this fiscal year. The distance between start date and end date may not be more than two years.
`endDate`|`date`|`YYYY-MM-DD`|**Required** The end date for this fiscal year. The distance between start date and end date may not be more than two years.
`name`|`datetime`|-|**Required** The name of this fiscal year. Must be unique for this entity.
`status`|`string`|-|**Required** The status of this fiscal year. Supported values: `OPEN`, `CLOSED`, `REMOVED`
`id`|`string`|-|The budget service's key for this object.
`lastModified`|`datetime`|-|**READ ONLY** The UTC date and time when this object was last changed.
`displayName`|`string`|-|**READ ONLY** Display name for fiscal year. For date range budget item we use this field to display.
`monthlyFiscalPeriods`|`array`|[`fiscalPeriod`](#fiscalPeriod)|**READ ONLY** The list of monthly Fiscal Periods in this Fiscal Year. Fiscal periods must complete fill the parent Fiscal Year with no overlaps.
`quarterlyFiscalPeriods`|`array`|[`fiscalPeriod`](#fiscalPeriod)|**READ ONLY** The list of quarterly Fiscal Periods in this Fiscal Year.  If this parameter is not specified, quarterly Fiscal Periods are automatically generated based on the monthly Fiscal Periods supplied.
`yearlyFiscalPeriods`|`array`|[`fiscalPeriod`](#fiscalPeriod)	|**READ ONLY** The list of yearly Fiscal Periods in this Fiscal Year.  If this parameter is not specified, one period is created that fills the Fiscal Year.
`customFiscalPeriods`|`array`|[`fiscalPeriod`](#fiscalPeriod)	|**READ ONLY** The list of custom Fiscal Periods in this Fiscal Year.  Custom Fiscal Periods are API-only and will not display on user budget dashboards.
`openAndClosedFiscalPeriods`|`array`|[`fiscalPeriod`](#fiscalPeriod)	|**READ ONLY** The list of all Fiscal Periods in this Fiscal Year, sorted by status.
`fiscalPeriods`|`array`|[`fiscalPeriod`](#fiscalPeriod)	|**READ ONLY** The list of all Fiscal Periods in this Fiscal Year.
`displayName`|`string`|-|**READ ONLY** Display name for fiscal year. For date range budget item we use this field to display.

#### <a name="fiscalPeriod"></a>Budget Item - FiscalPeriod

Name|Type|Format|Description
---|---|---|---
`currentPeriod`|`boolean`|-|**READ ONLY** If `true`, this is the current fiscal period based on the current time. `false`, if otherwise.
`startDate`|`date`|`YYYY-MM-DD`|**Required** The start date for this fiscal period. Must be within the parent fiscal year.
`endDate`|`date`|`YYYY-MM-DD`|**Required** The end date for this fiscal year. Must be within the parent fiscal year.
`name`|`string`|-|**Required** The name of this fiscal period. Must be unique for this entity.
`fiscalPeriodStatus`|`string`|-|**Required** The status of this fiscal period. Supported values: `OPEN`, `CLOSED`, `REMOVED`
`periodType`|`string`|-|**Required** The type of fiscal period. Supported values: `MONTHLY`, `QUARTERLY`, `YEARLY`, `CUSTOM`, `DATE_RANGE`
`fiscalYearId`|`string`|-|The key of the parent fiscal year for this fiscal period.
`id`|`string`|-|The budget service's key for this object.
`spendDate`|`date`|-|**READ ONLY** If the current date is after this fiscal period's start date, this field shows the current date.

#### <a name="dateRange"></a>DateRange

Name|Type|Format|Description
---|---|---|---
`startDate`|`date`|`YYYY-MM-DD`|The start date for the budget.
`endDate`|`date`|`YYYY-MM-DD`|The end date for the budget.

#### <a name="detailDashboardBudgetItemAdjustment"></a>DetailDashboardBudgetItemAdjustment

Name|Type|Format|Description
---|---|---|---
`adjustmentType`|`string`|-|The type of adjustment being made. Only a user reference field. Supported values: `BUDGET_BALANCE`, `FUND_TRANSFER`, `EXPENSE`, `PAYMENT_REQUEST`, `PURCHASE_REQUEST`, `REQUEST`, `PURGE_ADJUSTMENT`
`amount`|`decimal`|-|The value of the amount adjusted (+/-).
`amountType`|`string`|-|The amount type of the field. Supported values: `QUICK_EXPENSE`, `ERECEIPT`, `CREDIT_CARD`, `PERSONAL_CARD`, `TRIP`, `RECEIPT_CAPTURE`, `BILLING_STATEMENT`, `MANUAL`, `NONE`, `BUDGET_AMOUNT`, `SPENT_AMOUNT`, `PENDING_AMOUNT`, `PRE_AUTHORIZED`, `PURGE_ADJUSTMENT`
`description`|`string`|-|The short description of the adjustment.
`transactionDate`|`date`|`YYYY-MM-DD`|The transaction date of adjusted spend. Required when the adjustment is made for amount type. Supported values: `SPENT_AMOUNT`, `PENDING_AMOUNT`

#### <a name="budgetItemResponse"></a>BudgetItemResponse

Name|Type|Format|Description
---|---|---|---
`success`|`boolean`|-|`True` or `False` for success or failure.
`budgetItemHeaderId`|`guid`|-|The key of the created/updated/removed budget item header.

#### <a name="errorResponse"></a>Budget Item - Error Response

Name|Type|Format|Description
---|---|---|---
`status`|`boolean`|-|`False` if there was an error.
`errorMessageList`|`array`|[`errorMessage`](#errorMessage)|List of all errors detected.

#### <a name="errorMessage"></a>Budget Item - Error Message

Name|Type|Format|Description
---|---|---|---
`errorType`|`String`|-|WARNING or ERROR.
`errorCode`|`String`|-|Text code for this error.
`errorMessage`|`String`|-|Plain language error message.

#### <a name="responseHeaders"></a>Budget Item - Response Headers

* `concur-correlationid` is a SAP Concur specific custom header used for technical support in the form of a [RFC 4122 A Universally Unique IDentifier (UUID) URN Namespace](https://tools.ietf.org/html/rfc4122)
* [RFC 7231 Allow](https://tools.ietf.org/html/rfc7231#section-7.4.1)
* [RFC 7234 Cache-Control](https://tools.ietf.org/html/rfc7234#section-5.2)
* [RFC 7230 Content-Length](https://tools.ietf.org/html/rfc7230#section-3.3.2)
* [RFC 7231 Content-Type](https://tools.ietf.org/html/rfc7231#section-3.1.1.5)
* [RFC 7231 Date](https://tools.ietf.org/html/rfc7231#section-7.1.1.2)
* [RFC 7234 Expires](https://tools.ietf.org/html/rfc7234#section-5.3)
* [RFC 7232 ETag](https://tools.ietf.org/html/rfc7232#section-2.3)
* [RFC 7234 Pragma](https://tools.ietf.org/html/rfc7234#section-5.4)
* [RFC 7231 Server](https://tools.ietf.org/html/rfc7231#section-7.4.2)
* [RFC 7231 Vary](https://tools.ietf.org/html/rfc7231#section-7.1.4)
