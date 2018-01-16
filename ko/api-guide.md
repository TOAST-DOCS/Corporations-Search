## Search > Corporation Search > API 가이드

다음과 같은 API 호출을 통해 거래처 휴/폐업조회 서비스를 이용할 수 있습니다.

<br/>

### 거래처 휴/페업 요청
------------------------------------
[HTTP request]

```
POST   [Content-Type : application/x-www-form-urlencoded]
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/requests?p={param}
```

[Path Parameters]

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	AppKey|
|p|	String|	암호화된 Request body Parameter|

[Request body Parameters]

|이름|	자료형|	설명|
|---|---|---|
|custNo|	long|	고객번호 (Console 페이지 내 있음)|
|cryKey|	String|	고객인증키 (Console 페이지 내 있음)|
|bnoList|	String|	사업자등록번호 (복수개가능)|

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"
,"bnoList":["1234567890","0123456789","9012345678"]}

Json데이터를 AES256 함호화 처리후, URLEncoder(UTF-8) 처리된 데이터
rteo7fjjhGlVznybl239YSngEb2Y3VHOSJaM12AGasdyI1Y0pclSFnPo8uD8eHLFJ41AigDRpsXW36aBQoJXkTFhVeTQ4CMJFg8qKUXj%2Bl%2BwxjdkDJxVdCkJlh4Nnvxm
```

[Example request URL]

```
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/1sdaf3rs34d2/requests?p=rteo7fjjhGlVznybl239YSngEb2Y3VHOSJaM12AGasdyI1Y0pclSFnPo8uD8eHLFJ41AigDRpsXW36aBQoJXkTFhVeTQ4CMJFg8qKUXj%2Bl%2BwxjdkDJxVdCkJlh4Nnvxm
```

[Example Response]

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "정상적으로 요청되었습니다.",
        "successful": true
    },
    "data": {
        "reqNo": 68,
        "reqCnt": 8,
    “reqDate” : “2015-12-10 10:10:10”
}
}
```

[Response]

|이름|	자료형|	설명|
|---|---|---|
|reqNo|	long|	요청번호|
|resultCnt|	int|	요청된 사업자등록번호 갯수|
|reqDate|	String|	요청된 일시|

<br/>

### 거래처 휴/페업 요청 상태확인
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/verification?p={param}
```

[Path Parameters]

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	AppKey|
|p|	String|	암호화된 Request body Parameter|

[Request body Parameters]

|이름|	자료형|	설명|
|---|---|---|
|custNo|	long|	고객번호 (Console 페이지 내 있음)|
|cryKey|	String|	고객인증키 (Console 페이지 내 있음)|
|reqNo|	long|	요청번호|

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"
,"reqNo":58}

Json데이터를 AES256 함호화 처리후, URLEncoder(UTF-8) 처리된 데이터
TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

[Example Request URL]

```
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/1sdaf3rs34d2/verification?p=TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

[Example Response]

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "정상적으로 요청되었습니다.",
        "successful": true
    },
    "data": {
        "reqNo": 68,
        "resultDate": “2015-11-11 10:10:10”,
}
}
```

[Response]

|이름|	자료형|	설명|
|---|---|---|
|reqNo|	long|	요청번호|
|resultDate|	String|	완료일시|

<br/>

### 거래처 휴/페업 요청 결과데이터 받기
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/results?p={param}
```

[Path Parameters]

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	AppKey|
|p|	String|	암호화된 Request body Parameter|

[Request body Parameters]

|이름|	자료형|	설명|
|---|---|---|
|custNo|	long|	고객번호 (Console 페이지 내 있음)|
|cryKey|	String|	고객인증키 (Console 페이지 내 있음)|
|reqNo|	long|	요청번호|
|scn|	String [Y,N]|	거래처명 조회Flag [필수값 아님]|

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"
,"reqNo":58}

Json데이터를 AES256 함호화 처리후, URLEncoder(UTF-8) 처리된 데이터
TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

[Example Request URL]

```
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/1sdaf3rs34d2/results?p=TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

[Example Response]

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "조회요청이 완료되었습니다.",
        "successful": true
    },
    "data": {
        "reqNo": 58,
        "resultCnt": 8,
        "resultDate": "2015-11-11 10:10:10",
        "resultEncrytData": "8LAT2G8kMp1rFby+n0gWIDYhpnO/sDSU2zMyp0tLnb9Y901/+sw5agirJsWgpJm6s81R1uwOyC+zzBOG98H+WrC1zAMHX1U5tcpbgF+RSeQdx//8r6Af1NXQ3FZ/IsVJnhvttKEqnpFVzGt11zhNz1Tunj4d+N+MWYEr7BW2izaQXxRlZ0HX8X8lEiJp7JutKO9BKpZbAtR471SsDAtT6gS845CayO2ojA6ujpqtF/v/ZQei+0KEF10eBwutGTmn1i891E7K/NzdsQbu8qeau7Ksx+QrLSm0SaPHrK71XFjincB/xxXp12xc1zsZK3drQQ/U2xbiAY3CPqTXdNjWpj/iBRZaagQcC6VVvlIrMJ4t4O+cr7xsW5iMgmcpg75dPpsa4pkG8V0S9YKGg24TH+qfM7RZ9Xh7m+OSZMQRtbFT4fLLawB4E7mMKRPCBjmR3elQ0vVrNhWZ8kFt+a8C4D+EdWTIplvkS13tKkFFCF4=",
}
}
```

[Response]

|이름|	자료형|	설명|
|---|---|---|
|reqNo|	long|	요청번호|
|resultCnt|	int|	완료데이터 갯수|
|resultDate|	String|	완료일자|
|resultEncrytData|	String|	암호화된 휴페업정보데이터|

resultEncrytData 해당데이터의 URLDecoder 처리 후, AES256 복호화 처리

```
[{"bno":"1234567890","bnoCd":"01","bnoCont":"부가가치세 일반과세자 입니다.","bnoDate":"2015-11-11 10:10:10"}
,{"bno":"1234567890","bnoCd":"01","bnoCont":"부가가치세 일반과세자 입니다.","bnoDate":"2015-11-11 10:10:10"}
,{"bno":"1234567890","bnoCd":"01","bnoCont":"부가가치세 일반과세자 입니다.","bnoDate":"2015-11-10 10:10:10"}]
```

|이름|	자료형|	설명|
|---|---|---|
|bno|	String|	사업자등록번호|
|bnoCd|	String|	결과결과코드|
|bnoCont|	String|	조회결과|
|bnoDate|	String|	조회날자|
|custNm|	String|	거래처명 (scn이 Y인경우만 포함됨)|

<br/>

### 거래처 휴/페업 최근 요청중인 요청번호 확인
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/recent?p={param}
```

[Path Parameters]

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	AppKey|
|p|	String|	암호화된 Request body Parameter|

[Request body Parameters]

|이름|	자료형|	설명|
|---|---|---|
|custNo|	long|	고객번호 (Console 페이지 내 있음)|
|cryKey|	String|	고객인증키 (Console 페이지 내 있음)|

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"}

Json데이터를 AES256 함호화 처리후, URLEncoder(UTF-8) 처리된 데이터
3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

[Example Request URL]

```
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/1sdaf3rs34d2/verification?p=3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

[Example Response]

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "정상적으로 요청되었습니다.",
        "successful": true
    },
    "data": {
        "recentReqNo": 68,
        "recentReqDate": “2015-11-11 10:10:10”,
}
}
```

[Response]

|이름|	자료형|	설명|
|---|---|---|
|recentReqNo|	long|	최근요청번호|
|recentReqDate|	String|	최근요청일시|

<br/>

### 거래처 휴/페업 최근 일주일내 요청내역 확인
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/reqlists?p={param}
```

[Path Parameters]

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	AppKey|
|p|	String|	암호화된 Request body Parameter|

[Request body Parameters]

|이름|	자료형|	설명|
|---|---|---|
|custNo|	long|	고객번호 (Console 페이지 내 있음)|
|cryKey|	String|	고객인증키 (Console 페이지 내 있음)|

[Example Request]

<pre><code>{"custNo":1
,"crtKey":"qaz!@wsx"}

Json데이터를 AES256 함호화 처리후, URLEncoder(UTF-8) 처리된 데이터
3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn</code></pre>


[Example Request URL]

```
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/1sdaf3rs34d2/reqlists?p=3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

[Example Response]

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "정상적으로 요청되었습니다.",
        "successful": true
    },
    "data": {
        "reqList ": “[{“reqNo”:68,”reqStatCd”:”REQUEST”,”reqYmdt”:”2015-10-10 10:10:10”,”trtYmdt”:””,”reqCnt”:20}
, [{“reqNo”:69,”reqStatCd”:”COMPLETE”,”reqYmdt”:”2015-10-10 10:10:10”,”trtYmdt”:” 2015-10-12 10:10:10”,”reqCnt”:20}]”
}
}
```

[Response]

|이름|	자료형|	설명|
|---|---|---|
|reqNo|	long|	요청번호|
|reqStatCd|	String|	요청상태|
|reqYmdt|	String|	요청일시|
|trtYmdt|	String|	결과일시|
|reqCnt|	int|	요청갯수|

<br/>

## 참고사항
### 결과조회코드표
|코드값|	결과값|
|---|---|
|00|	사업을 하고 있지 않는 사업자|
|01|	부가가치세 일반과세자|
|02|	부가가치세 간이과세자|
|03|	부가가치세 면세사업자|
|04|	수익사업을 영위하지 않는 비영리법인이거나 고유번호가 부여된 단체.국가기관|
|05|	휴업자|
|06|	폐업자|
|09|	기타|

<br/>

### AES 256 암호화

> 암호화모듈 개발시 CBC, 패딩은 PKCS5Padding 사용
> [Example] 
Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding")

> 문자셋 Encoding은 UTF8을 사용
