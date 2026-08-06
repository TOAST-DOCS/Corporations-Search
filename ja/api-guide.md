<!-- pre-align:aligned sig=3d0b8c13d888 -->

# Corporation Search APIガイド

**Search > Corporation Search > Corporation Search APIガイド**

<a id="corporation-search-api-common-information"></a>
## Corporation Search API共通情報 { #corporation-search-api-common-information }

<a id="authentication-and-authorization"></a>
### 認証および権限 { #authentication-and-authorization }

Corporation Search APIを使用するには、AppkeyとSecretKeyが必要です。

Appkeyは、NHN Cloudの各サービスごとに発行される固有の認証キーであり、APIリクエスト時のサービス識別と有効性検証に使用されます。SecretKeyは、APIへのアクセスを制御するシークレットキーです。

Appkey及びSecretKeyの確認及び使用に関する詳細は、[Appkey](/nhncloud/ja/public-api/appkey)を参照してください。

<a id="error-codes"></a>
## エラーコード { #error-codes }

| 応答コード | 説明 |
| --- | --- |
| 0 | 成功 |
| -1002 | JSON規格エラー |
| -1003 | 復号化およびその他エラー |
| -1006 | 該当アプリケーションキー(Appkey)で登録されたユーザーがいません。 |
| -1008 | 指定した日付形式が無効です。 |
| -1201 | 要請した取引先がありません。 |
| -1202 | 認証されたユーザーではありません。 |
| -1203 | 事業者照会中です。 |
| -1204 | 要請された履歴がありません。 |
| -1205 | 無効な要請番号です。 |
| -1206 | 無効な事業者番号です。 |
| -1207 | 存在しない要請番号です。 |
| -1208 | 過去7日間の要請履歴がありません。 |
| -1209 | 該当日時はすでにスクレイピングが完了しました。 |

---

<a id="request-for-query-of-business-closurecessation"></a>
## 取引先の休廃業要請 { #request-for-query-of-business-closurecessation }

事業者登録番号リストに対する休廃業情報の照会を要請します。

<a id="request"></a>
### リクエスト { #request }

```
POST /scraping/v1.0/appkeys/{appkey}/requests?p={param}
Content-Type: application/x-www-form-urlencoded
```

<a id="request-parameters"></a>
### リクエストパラメータ { #request-parameters }

<details>
  <summary><strong>サンプルURL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/requests?p=rteo7fjjhGlVznybl239YSngEb2Y3VHOSJaM12AGasdyI1Y0pclSFnPo8uD8eHLFJ41AigDRpsXW36aBQoJXkTFhVeTQ4CMJFg8qKUXj%2Bl%2BwxjdkDJxVdCkJlh4Nnvxm
```

</details>

| 名前 | 区分 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | アプリケーションキー(AppKey) |
| p | URL | String | Y | 暗号化されたリクエスト本文パラメータ(request body parameter) |

<a id="request-body"></a>
### リクエスト本文 { #request-body }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx",
    "bnoList": ["1234567890", "0123456789", "9012345678"]
}

JSONデータをAES256暗号化処理後、URLEncoder(UTF-8)処理されたデータ
rteo7fjjhGlVznybl239YSngEb2Y3VHOSJaM12AGasdyI1Y0pclSFnPo8uD8eHLFJ41AigDRpsXW36aBQoJXkTFhVeTQ4CMJFg8qKUXj%2Bl%2BwxjdkDJxVdCkJlh4Nnvxm
```

</details>

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| custNo | Long | Y | 顧客番号(NHN Cloud Consoleページ内にある) |
| crtKey | String | Y | 顧客認証キー(NHN Cloud Consoleページ内にある) |
| bnoList | String | Y | 事業者登録番号(複数可能) |

<a id="response"></a>
### レスポンス { #response }

<details>
  <summary><strong>サンプルコード</strong></summary>

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
        "reqDate": "2015-12-10 10:10:10"
    }
}
```

</details>

| 名前 | データ型 | 説明 |
| --- | --- | --- |
| reqNo | Long | 要請番号 |
| resultCnt | Int | 要請した事業者登録番号の個数 |
| reqDate | String | 要請した日時 |

---

<a id="check-status-of-request-for-query-of-business-closurecessation"></a>
## 取引先の休廃業要請状態の確認 { #check-status-of-request-for-query-of-business-closurecessation }

要請した休廃業情報照会作業の処理状態を確認します。

<a id="check-status-of-request-for-query-of-business-closurecessation-request"></a>
### リクエスト { #check-status-of-request-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/verification?p={param}
```

<a id="check-status-of-request-for-query-of-business-closurecessation-request-parameters"></a>
### リクエストパラメータ { #check-status-of-request-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>サンプルURL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/verification?p=TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| 名前 | 区分 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | アプリケーションキー(AppKey) |
| p | URL | String | Y | 暗号化されたリクエスト本文パラメータ(request body parameter) |

<a id="check-status-of-request-for-query-of-business-closurecessation-request-body"></a>
### リクエスト本文 { #check-status-of-request-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx",
    "reqNo": 58
}

JSONデータをAES256暗号化処理後、URLEncoder(UTF-8)処理されたデータ
TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| custNo | Long | Y | 顧客番号(NHN Cloud Consoleページ内にある) |
| crtKey | String | Y | 顧客認証キー(NHN Cloud Consoleページ内にある) |
| reqNo | Long | Y | 要請番号 |

<a id="check-status-of-request-for-query-of-business-closurecessation-response"></a>
### レスポンス { #check-status-of-request-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "要請に成功しました。",
        "successful": true
    },
    "data": {
        "reqNo": 68,
        "resultDate": "2015-11-11 10:10:10"
    }
}
```

</details>

| 名前 | データ型 | 説明 |
| --- | --- | --- |
| reqNo | Long | 要請番号 |
| resultDate | String | 完了日時 |

---

<a id="receive-result-of-request-for-query-of-business-closurecessation"></a>
## 取引先の休廃業要請結果データを受け取る { #receive-result-of-request-for-query-of-business-closurecessation }

要請した休廃業情報照会の結果データを照会します。

<a id="receive-result-of-request-for-query-of-business-closurecessation-request"></a>
### リクエスト { #receive-result-of-request-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/results?p={param}
```

<a id="receive-result-of-request-for-query-of-business-closurecessation-request-parameters"></a>
### リクエストパラメータ { #receive-result-of-request-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>サンプルURL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/results?p=TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| 名前 | 区分 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | アプリケーションキー(AppKey) |
| p | URL | String | Y | 暗号化されたリクエスト本文パラメータ(request body parameter) |

<a id="receive-result-of-request-for-query-of-business-closurecessation-request-body"></a>
### リクエスト本文 { #receive-result-of-request-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx",
    "reqNo": 58
}

JSONデータをAES256暗号化処理後、URLEncoder(UTF-8)処理されたデータ
TSNRsStai0hQUM5m40dyDxIJsW5TON7QqVYjjhCIjBUKbMFqmiM1xZ8ND5%2Buo5xd
```

</details>

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| custNo | Long | Y | 顧客番号(NHN Cloud Consoleページ内にある) |
| crtKey | String | Y | 顧客認証キー(NHN Cloud Consoleページ内にある) |
| reqNo | Long | Y | 要請番号 |
| scn | String [Y,N] | N | 取引先名の照会フラグ |

<a id="receive-result-of-request-for-query-of-business-closurecessation-response"></a>
### レスポンス { #receive-result-of-request-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>サンプルコード</strong></summary>

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
        "resultEncrytData": "8LAT2G8kMp1rFby+n0gWIDYhpnO/sDSU2zMyp0tLnb9Y901/+sw5agirJsWgpJm6s81R1uwOyC+zzBOG98H+WrC1zAMHX1U5tcpbgF+RSeQdx//8r6Af1NXQ3FZ/IsVJnhvttKEqnpFVzGt11zhNz1Tunj4d+N+MWYEr7BW2izaQXxRlZ0HX8X8lEiJp7JutKO9BKpZbAtR471SsDAtT6gS845CayO2ojA6ujpqtF/v/ZQei+0KEF10eBwutGTmn1i891E7K/NzdsQbu8qeau7Ksx+QrLSm0SaPHrK71XFjincB/xxXp12xc1zsZK3drQQ/U2xbiAY3CPqTXdNjWpj/iBRZaagQcC6VVvlIrMJ4t4O+cr7xsW5iMgmcpg75dPpsa4pkG8V0S9YKGg24TH+qfM7RZ9Xh7m+OSZMQRtbFT4fLLawB4E7mMKRPCBjmR3elQ0vVrNhWZ8kFt+a8C4D+EdWTIplvkS13tKkFFCF4="
    }
}
```

</details>

| 名前 | データ型 | 説明 |
| --- | --- | --- |
| reqNo | Long | 要請番号 |
| resultCnt | Int | 完了データ個数 |
| resultDate | String | 完了日時 |
| resultEncrytData | String | 暗号化された休廃業情報データ |

resultEncrytData該当データのURLDecoder処理後、AES256復号化処理

```
[
    {
        "bno": "1234567890",
        "bnoCd": "01",
        "bnoCont": "付加価値税一般課税者です。",
        "bnoDate": "2015-11-11 10:10:10"
    },
    {
        "bno": "1234567890",
        "bnoCd": "01",
        "bnoCont": "付加価値税一般課税者です。",
        "bnoDate": "2015-11-11 10:10:10"
    },
    {
        "bno": "1234567890",
        "bnoCd": "01",
        "bnoCont": "付加価値税一般課税者です。",
        "bnoDate": "2015-11-10 10:10:10"
    }
]
```

| 名前 | データ型 | 説明 |
| --- | --- | --- |
| bno | String | 事業者登録番号 |
| bnoCd | String | 結果コード |
| bnoCont | String | 照会結果 |
| bnoDate | String | 照会日 |
| custNm | String | 取引先名(scnがYの場合のみ含まれる) |

---

<a id="check-recent-request-number-for-query-of-business-closurecessation"></a>
## 取引先の休廃業直近で要請中の要請番号を確認 { #check-recent-request-number-for-query-of-business-closurecessation }

直近で要請した休廃業情報照会の要請番号を確認します。

<a id="check-recent-request-number-for-query-of-business-closurecessation-request"></a>
### リクエスト { #check-recent-request-number-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/recent?p={param}
```

<a id="check-recent-request-number-for-query-of-business-closurecessation-request-parameters"></a>
### リクエストパラメータ { #check-recent-request-number-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>サンプルURL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/recent?p=3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| 名前 | 区分 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | アプリケーションキー(AppKey) |
| p | URL | String | Y | 暗号化されたリクエスト本文パラメータ(request body parameter) |

<a id="check-recent-request-number-for-query-of-business-closurecessation-request-body"></a>
### リクエスト本文 { #check-recent-request-number-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx"
}

JSONデータをAES256暗号化処理後、URLEncoder(UTF-8)処理されたデータ
3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| custNo | Long | Y | 顧客番号(NHN Cloud Consoleページ内にある) |
| crtKey | String | Y | 顧客認証キー(NHN Cloud Consoleページ内にある) |

<a id="check-recent-request-number-for-query-of-business-closurecessation-response"></a>
### レスポンス { #check-recent-request-number-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "要請に成功しました。",
        "successful": true
    },
    "data": {
        "recentReqNo": 68,
        "recentReqDate": "2015-11-11 10:10:10"
    }
}
```

</details>

| 名前 | データ型 | 説明 |
| --- | --- | --- |
| recentReqNo | Long | 最終要請番号 |
| recentReqDate | String | 最終要請日時 |

---

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation"></a>
## 取引先の休廃業の一週間以内の要請内容を確認 { #check-requests-of-recent-1-week-for-query-of-business-closurecessation }

直近一週間以内の休廃業情報照会要請内容のリストを照会します。

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-request"></a>
### リクエスト { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-request }

```
GET /scraping/v1.0/appkeys/{appkey}/reqlists?p={param}
```

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-parameters"></a>
### リクエストパラメータ { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-parameters }

<details>
  <summary><strong>サンプルURL</strong></summary>

```
https://api-corpsearch.nhncloudservice.com/scraping/v1.0/appkeys/1sdaf3rs34d2/reqlists?p=3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| 名前 | 区分 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appkey | URL | String | Y | アプリケーションキー(AppKey) |
| p | URL | String | Y | 暗号化されたリクエスト本文パラメータ(request body parameter) |

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-body"></a>
### リクエスト本文 { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-request-body }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "custNo": 1,
    "crtKey": "qaz!@wsx"
}

JSONデータをAES256暗号化処理後、URLEncoder(UTF-8)処理されたデータ
3Tm2TS3ynvXw3jcgh1SzQcMIBA2EIRp%2FheQSAsWSXHTP0TODL%2FYEL1Iml3Qn1CWn
```

</details>

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| custNo | Long | Y | 顧客番号(NHN Cloud Consoleページ内にある) |
| crtKey | String | Y | 顧客認証キー(NHN Cloud Consoleページ内にある) |

<a id="check-requests-of-recent-1-week-for-query-of-business-closurecessation-response"></a>
### レスポンス { #check-requests-of-recent-1-week-for-query-of-business-closurecessation-response }

<details>
  <summary><strong>サンプルコード</strong></summary>

```
{
    "header": {
        "resultCode": 0,
        "resultMessage": "要請に成功しました。",
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

| 名前 | データ型 | 説明 |
| --- | --- | --- |
| reqNo | Long | 要請番号 |
| reqStatCd | String | 要請状態 |
| reqYmdt | String | 要請日時 |
| trtYmdt | String | 結果日時 |
| reqCnt | Int | 要請個数 |

---

<a id="references"></a>
## 参考事項 { #references }

<a id="table-of-query-result-codes"></a>
### 結果照会コード表 { #table-of-query-result-codes }

| コード値 | 結果値 |
| --- | --- |
| 00 | 事業を行っていない事業者 |
| 01 | 付加価値税一般課税者 |
| 02 | 付加価値税簡易課税者 |
| 03 | 付加価値税免除事業者 |
| 04 | 収益事業を営まない非営利法人または固有番号が付与された団体・国家機関 |
| 05 | 休業者 |
| 06 | 廃業者 |
| 09 | その他 |

<a id="aes-256-encryption"></a>
### AES 256暗号化 { #aes-256-encryption }

> 暗号化モジュール開発時、CBC、パディングはPKCS5Paddingを使用
> [Example]
> Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding")

> 文字コード(character set)エンコードはUTF-8を使用
