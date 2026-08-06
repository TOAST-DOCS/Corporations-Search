<!-- pre-align:aligned sig=3d0b8c13d888 -->

# Corporation Search API Guide

**Search > Corporation Search > Corporation Search API Guide**

<a id="corporation-search-api-common-information"></a>
## Corporation Search API Common Information { #corporation-search-api-common-information }

<a id="authentication-and-authorization"></a>
### Authentication and Authorization { #authentication-and-authorization }

AppKey and SecretKey are required to use the Corporation Search API.

An Appkey is a unique authentication key issued for each NHN Cloud service, used to identify the service and validate API requests. A SecretKey is a private key used to control access to the API. For more information on checking and using Appkeys, please refer to the [Appkey](/nhncloud/en/public-api/appkey).

<a id="error-codes"></a>
## Error Codes { #error-codes }

| Response Code | Description |
| --- | --- |
| 0 | Successful |
| -1002 | Error in JSON specifications |
| -1003 | Error in decryption and others |
| -1006 | There is no user registered in the appkey. |
| -1008 | Invalid format of specified date. |
| -1201 | No business is requested. |
| -1202 | Not an authenticated user. |
| -1203 | Querying business owner. |
| -1204 | There is no history of request. |
| -1205 | Invalid request number. |
| -1206 | Invalid business registration number. |
| -1207 | The request number does not exist. |
| -1208 | There is no history of request for the recent 7 days. |
| -1209 | The date/time is already scrapped. |

---

<a id="request-for-query-of-business-closurecessation"></a>
## Request for Query of Business Closure/Cessation { #request-for-query-of-business-closurecessation }

Requests a query of business closure/cessation information for a list of business registration numbers.

<a id="request"></a>
### Request { #request }

```
POST /scraping/v1.0/appkeys/{appkey}/requests?p={param}
Content-Type: application/x-www-form-urlencoded
```

<a id="request-parameters"></a>
### Request Parameters { #request-parameters }

<details>
  <summary><strong>Example URL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/requests?p=rteo7fjjhGlVznybl239YSngEb2Y3VHOSJaM12AGasdyI1Y0pclSFnPo8uD8eHLFJ41AigDRpsXW36aBQoJXkTFhVeTQ4CMJFg8qKUXj%2Bl%2BwxjdkDJxVdCkJlh4Nnvxm
```

</details>

| Name | Category | Data Type | Required | Description |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | AppKey |
| p | URL | String | Y | Encrypted request body parameter |

<a id="request-body"></a>
### Request Body { #request-body }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx",
    "bnoList": ["1234567890", "0123456789", "9012345678"]
}

Encrypt JSON data in AES256 and process as URLEncoder(UTF-8)
rteo7fjjhGlVznybl239YSngEb2Y3VHOSJaM12AGasdyI1Y0pclSFnPo8uD8eHLFJ41AigDRpsXW36aBQoJXkTFhVeTQ4CMJFg8qKUXj%2Bl%2BwxjdkDJxVdCkJlh4Nnvxm
```

</details>

| Name | Data Type | Required | Description |
| --- | --- | --- | --- |
| custNo | Long | Y | Client number (available on NHN Cloud Console) |
| crtKey | String | Y | Client authentication key (available on NHN Cloud Console) |
| bnoList | String | Y | Business registration number (one or many) |

<a id="response"></a>
### Response { #response }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "Properly requested.",
        "successful": true
    },
    "data": {
        "reqNo": 68,
        "reqCnt": 8,
        "reqDate": "2015-12-10 10:10:10"
    }
}
```

</details>

| Name | Data Type | Description |
| --- | --- | --- |
| reqNo | Long | Request number |
| resultCnt | Int | Requested number of business registration numbers |
| reqDate | String | Date and time of request |

---

<a id="check-status-of-request-for-query-of-business-closurecessation"></a>
## Check Status of Request for Query of Business Closure/Cessation { #check-status-of-request-for-query-of-business-closurecessation }

Checks the processing status of the requested business closure/cessation query.

<a id="check-status-of-request-for-query-of-business-closurecessation-request"></a>
### Request { #check-status-of-request-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/verification?p={param}
```

<a id="check-status-of-request-for-query-of-business-closurecessation-request-parameters"></a>
### Request Parameters { #check-status-of-request-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>Example URL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/verification?p=TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| Name | Category | Data Type | Required | Description |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | AppKey |
| p | URL | String | Y | Encrypted request body parameter |

<a id="check-status-of-request-for-query-of-business-closurecessation-request-body"></a>
### Request Body { #check-status-of-request-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx",
    "reqNo": 58
}

Encrypt JSON data in AES256 and process as URLEncoder(UTF-8)
TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| Name | Data Type | Required | Description |
| --- | --- | --- | --- |
| custNo | Long | Y | Client number (available on NHN Cloud Console) |
| crtKey | String | Y | Client authentication key (available on NHN Cloud Console) |
| reqNo | Long | Y | Request number |

<a id="check-status-of-request-for-query-of-business-closurecessation-response"></a>
### Response { #check-status-of-request-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "Properly requested.",
        "successful": true
    },
    "data": {
        "reqNo": 68,
        "resultDate": "2015-11-11 10:10:10"
    }
}
```

</details>

| Name | Data Type | Description |
| --- | --- | --- |
| reqNo | Long | Request number |
| resultDate | String | Date and time of completion |

---

<a id="receive-result-of-request-for-query-of-business-closurecessation"></a>
## Receive Result of Request for Query of Business Closure/Cessation { #receive-result-of-request-for-query-of-business-closurecessation }

Receives the result data of the requested business closure/cessation query.

<a id="receive-result-of-request-for-query-of-business-closurecessation-request"></a>
### Request { #receive-result-of-request-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/results?p={param}
```

<a id="receive-result-of-request-for-query-of-business-closurecessation-request-parameters"></a>
### Request Parameters { #receive-result-of-request-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>Example URL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/results?p=TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| Name | Category | Data Type | Required | Description |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | AppKey |
| p | URL | String | Y | Encrypted request body parameter |

<a id="receive-result-of-request-for-query-of-business-closurecessation-request-body"></a>
### Request Body { #receive-result-of-request-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx",
    "reqNo": 58
}

Encrypt JSON data in AES256 and process as URLEncoder(UTF-8)
TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| Name | Data Type | Required | Description |
| --- | --- | --- | --- |
| custNo | Long | Y | Client number (available on NHN Cloud Console) |
| crtKey | String | Y | Client authentication key (available on NHN Cloud Console) |
| reqNo | Long | Y | Request number |
| scn | String [Y,N] | N | Query flag of business name |

<a id="receive-result-of-request-for-query-of-business-closurecessation-response"></a>
### Response { #receive-result-of-request-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "Completely requested for query.",
        "successful": true
    },
    "data": {
        "reqNo": 58,
        "resultCnt": 8,
        "resultDate": "2015-11-11 10:10:10",
        "resultEncrytData": "8LAT2G8kMp1rFby+n0gWIDYhpnO/sDSU2zMyp0tLnb9Y901/+sw5agirJsWgpJm6s81R1uwOyC+zzBOG98H+WrC1zAMHX1U5tcpbgF+RSeQdx//8r6Af1NXQ3FZ/IsVJnhvttKEqnpFVzGt11zhNz1Tunj4d+N+MWYEr7BW2izaQXxRlZ0HX8X8lEiJp7JutKO9BKpZbAtR471SsDAtT6gS845CayO2ojA6ujpqtF/v/ZQei+0KEF10eBwutGTmn1i891E7K/NzdsQbu8qeau7Ksx+QrLSm0SaPHrK71XFjincB/xxXp12xc1zsZK3drQQ/U2xbiAY3CPqTXdNjWpj/iBRZaagQcC6VVvlIrMJ4t4O+cr7xsW5iMgmcpg75dPpsa4pkG8V0S9YKGg24TH+qfM7RZ9Xh7m+OSZMQRtbFT4fLLawB4E7mMKRPCBjmR3elQ0vVrNhWZ8kFt+a8C4D+EdWTIplvkS13tKkFFCF4="
    }
}
```

</details>

| Name | Data Type | Description |
| --- | --- | --- |
| reqNo | Long | Request number |
| resultCnt | Int | Number of completed data |
| resultDate | String | Date and time of completion |
| resultEncrytData | String | Encrypted data of business closure/cessation |

Process URLDecoder of corresponding resultEncrytData, and decrypt AES256.

```
[
    {
        "bno": "1234567890",
        "bnoCd": "01",
        "bnoCont": "General taxpayer for value-added tax.",
        "bnoDate": "2015-11-11 10:10:10"
    },
    {
        "bno": "1234567890",
        "bnoCd": "01",
        "bnoCont": "General taxpayer for value-added tax.",
        "bnoDate": "2015-11-11 10:10:10"
    },
    {
        "bno": "1234567890",
        "bnoCd": "01",
        "bnoCont": "General taxpayer for value-added tax.",
        "bnoDate": "2015-11-10 10:10:10"
    }
]
```

| Name | Data Type | Description |
| --- | --- | --- |
| bno | String | Business registration number |
| bnoCd | String | Result code |
| bnoCont | String | Query result |
| bnoDate | String | Date of query |
| custNm | String | Business name (included only when scn is Y) |

---

<a id="check-recent-request-number-for-query-of-business-closurecessation"></a>
## Check Recent Request Number for Query of Business Closure/Cessation { #check-recent-request-number-for-query-of-business-closurecessation }

Checks the most recent request number for business closure/cessation query.

<a id="check-recent-request-number-for-query-of-business-closurecessation-request"></a>
### Request { #check-recent-request-number-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/recent?p={param}
```

<a id="check-recent-request-number-for-query-of-business-closurecessation-request-parameters"></a>
### Request Parameters { #check-recent-request-number-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>Example URL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/recent?p=3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| Name | Category | Data Type | Required | Description |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | AppKey |
| p | URL | String | Y | Encrypted request body parameter |

<a id="check-recent-request-number-for-query-of-business-closurecessation-request-body"></a>
### Request Body { #check-recent-request-number-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx"
}

Encrypt JSON data in AES256 and process as URLEncoder(UTF-8)
3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| Name | Data Type | Required | Description |
| --- | --- | --- | --- |
| custNo | Long | Y | Client number (available on NHN Cloud Console) |
| crtKey | String | Y | Client authentication key (available on NHN Cloud Console) |

<a id="check-recent-request-number-for-query-of-business-closurecessation-response"></a>
### Response { #check-recent-request-number-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "Properly requested.",
        "successful": true
    },
    "data": {
        "recentReqNo": 68,
        "recentReqDate": "2015-11-11 10:10:10"
    }
}
```

</details>

| Name | Data Type | Description |
| --- | --- | --- |
| recentReqNo | Long | Recent request number |
| recentReqDate | String | Recent date/time of request |

---

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation"></a>
## Check Requests of Recent 1 Week for Query of Business Closure/Cessation { #check-requests-of-recent-1-week-for-query-of-business-closurecessation }

Retrieves the list of business closure/cessation query requests in the recent week.

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-request"></a>
### Request { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/reqlists?p={param}
```

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-parameters"></a>
### Request Parameters { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>Example URL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/reqlists?p=3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| Name | Category | Data Type | Required | Description |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | AppKey |
| p | URL | String | Y | Encrypted request body parameter |

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-body"></a>
### Request Body { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx"
}

Encrypt JSON data in AES256 and process as URLEncoder(UTF-8)
3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| Name | Data Type | Required | Description |
| --- | --- | --- | --- |
| custNo | Long | Y | Client number (available on NHN Cloud Console) |
| crtKey | String | Y | Client authentication key (available on NHN Cloud Console) |

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-response"></a>
### Response { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>Example Code</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "Properly requested.",
        "successful": true
    },
    "data": {
        "reqList": [
            {
                "reqNo": 68,
                "reqStatCd": "REQUEST",
                "reqYmdt": "2015-10-10 10:10:10",
                "trtYmdt": "",
                "reqCnt": 20
            },
            {
                "reqNo": 69,
                "reqStatCd": "COMPLETE",
                "reqYmdt": "2015-10-10 10:10:10",
                "trtYmdt": "2015-10-12 10:10:10",
                "reqCnt": 20
            }
        ]
    }
}
```

</details>

| Name | Data Type | Description |
| --- | --- | --- |
| reqNo | Long | Request number |
| reqStatCd | String | Status of request |
| reqYmdt | String | Date/time of request |
| trtYmdt | String | Date/time of receiving result |
| reqCnt | Int | Number of requests |

---

<a id="references"></a>
## References { #references }

<a id="table-of-query-result-codes"></a>
### Table of Query Result Codes { #table-of-query-result-codes }

| Code | Result |
| --- | --- |
| 00 | Business owner who is not operating business |
| 01 | General taxpayer for value-added tax |
| 02 | Simplified taxpayer for value-added tax |
| 03 | Business owner who is exempted from value-added tax |
| 04 | Non-profit corporations or organization who own original numbers: national institutions |
| 05 | Ceased business owner |
| 06 | Closed business owner |
| 09 | Others |

<a id="aes-256-encryption"></a>
### AES 256 Encryption { #aes-256-encryption }

> Use CBC for the development of encryption module, or PKCS5Padding for padding.
> [Example]
> Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding")

> Apply UTF-8 to encode character sets.
