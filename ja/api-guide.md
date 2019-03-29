## Search > Corporation Search > APIガイド

次のようなAPIを呼び出して、取引先の休廃業照会サービスを利用できます。

<br/>

### 取引先の休廃業要請
------------------------------------
[HTTP request]

```
POST   [Content-Type : application/x-www-form-urlencoded]
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/requests?p={param}
```

[Path Parameters]

|名前|	データ型|	説明|
|---|---|---|
|appkey|	String| アプリケーションキー(AppKey) |
|p|	String| 暗号化されたリクエスト本文パラメータ(request body parameter) |

[Request body Parameters]

|名前|	データ型|	説明|
|---|---|---|
|custNo|	long| 顧客番号(TOAST Consoleページ内にある) |
|crtKey|	String| 顧客認証キー(TOAST Consoleページ内にある) |
|bnoList|	String| 事業者登録番号(複数可能) |

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"
,"bnoList":["1234567890","0123456789","9012345678"]}

JSONデータをAES256暗号化処理後、 URLEncoder(UTF-8)処理されたデータ
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
        "resultMessage": "要請に成功しました。",
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

|名前|	データ型|	説明|
|---|---|---|
|reqNo|	long| 要請番号 |
|resultCnt|	int| 要請した事業者登録番号の個数 |
|reqDate|	String|	要請した日時|

<br/>

### 取引先の休廃業要請状態の確認
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/verification?p={param}
```

[Path Parameters]

|名前|	データ型|	説明|
|---|---|---|
|appkey|	String| アプリケーションキー(AppKey) |
|p|	String|	暗号化されたリクエスト本文パラメータ(request body parameter)|

[Request body Parameters]

|名前|	データ型|	説明|
|---|---|---|
|custNo|	long|	顧客番号(TOAST Consoleページ内にある)|
|crtKey|	String|	顧客認証キー(TOAST Consoleページ内にある)|
|reqNo|	long|	要請番号|

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"
,"reqNo":58}

JSONデータをAES256暗号化処理後、 URLEncoder(UTF-8)処理されたデータ
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
        "resultMessage": "要請に成功しました。",
        "successful": true
    },
    "data": {
        "reqNo": 68,
        "resultDate": “2015-11-11 10:10:10”,
}
}
```

[Response]

|名前|	データ型|	説明|
|---|---|---|
|reqNo|	long|	要請番号|
|resultDate|	String|	完了日時|

<br/>

### 取引先の休廃業要請結果データを受け取る
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/results?p={param}
```

[Path Parameters]

|名前|	データ型|	説明|
|---|---|---|
|appkey|	String|	アプリケーションキー(AppKey)|
|p|	String| 暗号化されたリクエスト本文パラメータ(request body parameter) |

[Request body Parameters]

|名前|	データ型|	説明|
|---|---|---|
|custNo|	long|	顧客番号(TOAST Consoleページ内にある)|
|crtKey|	String|	顧客認証キー(TOAST Consoleページ内にある)|
|reqNo|	long|	要請番号|
|scn| String [Y,N] | 取引先名の照会フラグ[必須値ではない] |

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"
,"reqNo":58}

JSONデータをAES256暗号化処理後、 URLEncoder(UTF-8)処理されたデータ
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
        "resultMessage": "照会要請が完了しました。",
        "successful": true
    },
    "data": {
        "reqNo": 58,
        "resultCnt": 8,
        "resultDate": "2015-11-11 10:10:10",
        "resultEncrytData": "8LAT2G8kMp1rFby+n0gWIDYhpnO/sDSU2zMyp0tLnb9Y901/+sw5agirJsWgpJm6s81R1uwOyC+zzBOG98H+WrC1zAMHX1U5tcpbgF+RSeQdx//8r6Af1NXQ3FZ/IsVJnhvttKEqnpFVzGt11zhNz1Tunjㅍ4d+N+MWYEr7BW2izaQXxRlZ0HX8X8lEiJp7JutKO9BKpZbAtR471SsDAtT6gS845CayO2ojA6ujpqtF/v/ZQei+0KEF10eBwutGTmn1i891E7K/NzdsQbu8qeau7Ksx+QrLSm0SaPHrK71XFjincB/xxXp12xc1zsZK3drQQ/U2xbiAY3CPqTXdNjWpj/iBRZaagQcC6VVvlIrMJ4t4O+cr7xsW5iMgmcpg75dPpsa4pkG8V0S9YKGg24TH+qfM7RZ9Xh7m+OSZMQRtbFT4fLLawB4E7mMKRPCBjmR3elQ0vVrNhWZ8kFt+a8C4D+EdWTIplvkS13tKkFFCF4=",
}
}
```

[Response]

|名前|	データ型|	説明|
|---|---|---|
|reqNo|	long|	要請番号|
|resultCnt|	int| 完了データ個数 |
|resultDate|	String| 完了日時 |
|resultEncrytData|	String| 暗号化された休廃業情報データ |

resultEncrytData該当データのURLDecoder処理後、 AES256復号化処理

```
[{"bno":"1234567890","bnoCd":"01","bnoCont":"付加価値税一般課税者です。","bnoDate":"2015-11-11 10:10:10"}
,{"bno":"1234567890","bnoCd":"01","bnoCont":"付加価値税一般課税者です。","bnoDate":"2015-11-11 10:10:10"}
,{"bno":"1234567890","bnoCd":"01","bnoCont":"付加価値税一般課税者です。","bnoDate":"2015-11-10 10:10:10"}]
```

|名前|	データ型|	説明|
|---|---|---|
|bno|	String|	事業者登録番号|
|bnoCd|	String| 結果コード |
|bnoCont|	String| 照会結果 |
|bnoDate|	String| 照会日 |
|custNm|	String| 取引先名(scnがYの場合のみ含まれる) |

<br/>

### 取引先の休廃業直近で要請中の要請番号を確認
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/recent?p={param}
```

[Path Parameters]

|名前|	データ型|	説明|
|---|---|---|
|appkey|	String| アプリケーションキー(AppKey) |
|p|	String| 暗号化されたリクエスト本文パラメータ(request body parameter) |

[Request body Parameters]

|名前|	データ型|	説明|
|---|---|---|
|custNo|	long|	顧客番号(TOAST Consoleページ内にある)|
|crtKey|	String|	顧客認証キー(TOAST Consoleページ内にある)|

[Example Request]

```
{"custNo":1
,"crtKey":"qaz!@wsx"}

JSONデータをAES256暗号化処理後、 URLEncoder(UTF-8)処理されたデータ
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
        "resultMessage": "要請に成功しました。",
        "successful": true
    },
    "data": {
        "recentReqNo": 68,
        "recentReqDate": “2015-11-11 10:10:10”,
}
}
```

[Response]

|名前|	データ型|	説明|
|---|---|---|
|recentReqNo|	long|	最終要請番号|
|recentReqDate|	String|	最終要請日時|

<br/>

### 取引先の休廃業の一週間以内の要請内容を確認
------------------------------------

[HTTP request]

```
GET
https://api-toastbill.cloud.toast.com/scraping/v1.0/appkeys/{appkey}/reqlists?p={param}
```

[Path Parameters]

|名前|	データ型|	説明|
|---|---|---|
|appkey|	String| アプリケーションキー(AppKey) |
|p|	String| 暗号化されたリクエスト本文パラメータ(request body parameter) |

[Request body Parameters]

|名前|	データ型|	説明|
|---|---|---|
|custNo|	long|	顧客番号(TOAST Consoleページ内にある)|
|crtKey|	String|	顧客認証キー(TOAST Consoleページ内にある)|

[Example Request]

<pre><code>{"custNo":1
,"crtKey":"qaz!@wsx"}
JSONデータをAES256暗号化した後、 URLEncoder(UTF-8)処理されたデータ
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
        "resultMessage": "要請に成功しました。",
        "successful": true
    },
    "data": {
        "reqList ": “[{“reqNo”:68,”reqStatCd”:”REQUEST”,”reqYmdt”:”2015-10-10 10:10:10”,”trtYmdt”:””,”reqCnt”:20}
, [{“reqNo”:69,”reqStatCd”:”COMPLETE”,”reqYmdt”:”2015-10-10 10:10:10”,”trtYmdt”:” 2015-10-12 10:10:10”,”reqCnt”:20}]”
}
}
```

[Response]

|名前|	データ型|	説明|
|---|---|---|
|reqNo|	long|	要請番号|
|reqStatCd|	String|	要請状態|
|reqYmdt|	String|	要請日時|
|trtYmdt|	String|	結果日時|
|reqCnt|	int|	要請個数|

<br/>

## 参考事項
### 結果照会コード表
|コード値|	結果値|
|---|---|
|00|	事業を行っていない事業者|
|01|	付加価値税一般課税者|
|02|	付加価値税簡易課税者|
|03|	付加価値税免除事業者|
|04| 収益事業を営まない非営利法人または固有番号が付与された団体。国家機関 |
|05|	休業者|
|06|	廃業者|
|09|	その他|

<br/>

### AES 256暗号化

> 暗号化モジュール開発時、CBC、パディングはPKCS5Paddingを使用
> [Example] 
Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding")

> 文字コード(character set)エンコードはUTF-8を使用
