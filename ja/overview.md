<!-- pre-align:aligned sig=2dc4a20dad20 -->

<a id="search-corporation-search-overview"></a>
## Search > Corporation Search > 概要 { #search-corporation-search-overview }

国税庁で管理する事業者番号に対して、課税タイプおよび新規登録、休廃業しているかどうかをスクレイピングモジュールで照会した後、財務/税務/ERPシステムと連携するサービスです。  
この照会サービスは正確な税務処理と、取引相手が税金計算書を交付できない休廃業した企業または簡易課税者と疑われる場合に、納税者がこれを確認して思わぬ被害を受けないようにするためのサービスです。

<a id="service-configuration"></a>
### サービス構成図 { #service-configuration }
![](http://static.toastoven.net/prod_corporation_search/Corporation Search_overview01_en.png)

<a id="available-services"></a>
### 提供サービス { #available-services }

|サービス|説明|
|---|---|
|課税情報|	事業者課税タイプ(一般/簡易/免除)|
|休廃業情報| 休廃業しているかかどうか、休廃業日時 |

<a id="features"></a>
### 主な機能 { #features }

- Excelファイルによる事業者登録番号の新規登録、休廃業しているかどうかの大量照会をサポートします。
- REST APIを提供しており、多様なプラットフォームで手軽に使用できます。
- REST APIによる、リアルタイム単件照会および複数取引先大量照会をサポートします。
