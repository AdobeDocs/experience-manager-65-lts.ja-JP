---
title: AEM Analyzerによるアップグレードの複雑さの評価
description: AEM Analyzerを使用して、アップグレードの複雑さを評価する方法について説明します。
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 87c30912-c89a-42f1-b37b-ec439e7318c7
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 23%
---
# AEM Analyzerによるアップグレードの複雑さの評価 {#assessing-the-upgrade-complexity-with-the-aem-analyzer}

## 概要 {#overview}

AEM 6.5 LTS アナライザーは、6.5 LTSへのシームレスなアップグレードエクスペリエンスを提供するために更新が必要な領域を示すことで、現在のAEMの実装を評価します。

このツールは、リファクタリングの可能性がある領域を特定するレポートを生成します。

## AEM 6.5 LTS アナライザーレポート {#aem-65lts-analyzer-report}

AEM 6.5 LTS アナライザーレポートは、一般的なアップグレードの準備状況の概要を把握するために使用されます。 このレポートは、AEM 6.5 LTSへのアップグレードを成功させるために対処する必要がある問題のカテゴリ内の調査結果で構成されています。

AEM 6.5 LTS アナライザーレポートには、次のカテゴリが含まれます。

* リファクタリングが必要なアプリケーション機能
* サポートされている場所に移動する必要があるリポジトリ項目
* 設定の問題
* 新機能によって削除されたAEM 6.5機能、または現在AEM 6.5 LTSでサポートされていない機能
* JavaとGuava APIの使用状況の削除

これらのカテゴリに関連するカテゴリと考えられる影響と解決策に関する追加情報は、AEM 6.5 LTS アナライザーレポート内のリンクを介して提供されます。

## 入手方法 {#analyzer-availability}

AEM Analyzerは、[ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html)からzip ファイルとしてダウンロードできます。 パッケージは、[Package Manager](/help/sites-administering/package-manager.md)を介してソース AEM インスタンスにインストールできます。

## AEM Analyzerを使用する際の重要な考慮事項 {#important-considerations-for-using-aem-analyzer}

AEM Analyzerを実行する際の重要な考慮事項については、次の節を参照してください。

* Analyzer レポートは、AEM パターン検出の出力を使用して作成されます。 Analyzerで使用されるパターン検出のバージョンは、AEM Analyzer インストールパッケージに含まれています
* AEM Analyzerは、**管理者** ユーザーまたは&#x200B;**管理者** グループのユーザーのみが実行できます
* Analyzerは、バージョン 6.5以降のAEM インスタンスでサポートされています。

>[!NOTE]
>
>ビジネスクリティカルなインスタンスへの影響を避けるために、カスタマイズ、設定、コンテンツおよびユーザーアプリケーションの分野で、実稼動環境にできるだけ近いステージ環境でAEM Analyzerを実行することをお勧めします。 または、実稼動版のオーサー環境のクローンで実行することもできます。

* AEM Analyzerのレポートの内容の生成には、数分から数時間まで、かなりの時間がかかることがあります。 必要な時間は、AEM リポジトリのコンテンツのサイズと性質、AEMのバージョン、その他の要因に大きく依存します
* レポートのコンテンツの生成には膨大な時間が必要になる可能性があるため、バックグラウンド・プロセスによって生成され、キャッシュに保持されます。 レポートの表示とダウンロードは、期限が切れるか、レポートが明示的に更新されるまでコンテンツキャッシュを利用するので、比較的高速で行われます。 レポートのコンテンツの生成中に、ブラウザータブを閉じて後で戻り、そのコンテンツがキャッシュで使用可能になると、レポートを表示できます。

## AEM Analyzer レポートの表示 {#viewing-the-aem-analyzer-report}

AEM Analyzer レポートを表示するには、次の手順に従います。

1. Adobe Experience Managerを選択し、**ツール – オペレーション - 6.5 LTS Modernizer**&#x200B;に移動します

   ![ アナライザーレポートを表示1](/help/sites-deploying/assets/view-analyzer-report-1.png)

1. **AEM 6.5 LTS Analyzer**&#x200B;をクリックして開きます

   ![ アナライザーレポートを表示2](/help/sites-deploying/assets/view-analyzer-report-2.png)

1. 「**レポートを生成**」をクリックして、AEM Analyzerを実行します

   ![ アナライザーレポートを表示3](/help/sites-deploying/assets/view-analyzer-report-3.png)

1. AEM Analyzerがレポートを生成している間、画面に表示されたツールによる進行状況を確認できます。 完了した割合で進捗状況が表示されます。 また、分析項目の数と調査結果の数も表示されます

   ![ アナライザーレポートを表示4](/help/sites-deploying/assets/view-analyzer-report-4.png)

1. 6.5 LTS アナライザーレポートを生成すると、結果の概要と数が、結果のタイプと重要度レベルで整理された表形式で表示されます。 特定の検索の詳細を取得するには、テーブル内の検索のタイプに対応する番号をクリックします

   ![ アナライザーレポートを表示5](/help/sites-deploying/assets/view-analyzer-report-5.png)

1. 「**CSV に書き出し**」をクリックすると、レポートをコンマ区切り値（CSV）形式でダウンロードできます。 アナライザーがキャッシュをクリアし、**レポートの更新**&#x200B;をクリックしてレポートを再生成するように強制できます。 キャッシュが期限切れになった場合は、レポートを再生成する必要があります。

## AEM Analyzer レポートの解釈 {#interpreting-the-aem-analyzer-report}

6.5 LTS アナライザーツールをAEM インスタンスで実行すると、レポートがツールウィンドウに結果として表示されます。

レポートの形式は次のとおりです。

* **レポートの概要**：次の情報を含む、レポート自体に関する情報。

  * **レポート時間**: レポートの内容が生成され、最初に使用可能になった日時
  * **有効期限**: レポート コンテンツ キャッシュの有効期限
  * **生成期間**: レポートが生成された時間
  * **検索回数**: レポートに含まれる調査結果の合計数

* **System Overview**: Analyzerが実行されたAEM システムに関する情報
* **発見カテゴリ**：各セクションが同じカテゴリの 1 つ以上の発見に対応する複数セクション。 各セクションには次の内容が含まれます。カテゴリ名、サブタイプ、発見数と重要度、概要、カテゴリドキュメントへのリンク、個々の発見情報。

  ![ アナライザーレポートの概要](/help/sites-deploying/assets/analyzer-report-summary.png)

  アクションの大まかな優先度を示すために、各発見に重要度レベルが割り当てられます。

>[!NOTE]
>
>各カテゴリの検索について詳しくは、[パターン検出のカテゴリ](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/aso)を参照してください。

重要度レベルを把握するには、次の表に従います。

| 重要度 | 説明 |
|---|---|
| INFO | 情報提供の目的で提供されます。 |
| ADVISORY | アップグレードに関する問題の可能性があります。 さらに調査を行うことをお勧めします。 |
| CRITICAL | アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |

## AEM 6.5 LTS Analyzer CSV レポートの解釈 {#interpreting-the-aem-65lts-analyzer-report}

AEM インスタンスから&#x200B;**CSV** オプションをクリックすると、Analyzer レポートのCSV フォーマットがコンテンツキャッシュから構築され、ブラウザーに返されます。 ブラウザーの設定に応じて、このレポートは、デフォルト名が `report.csv` のファイルとして自動的にダウンロードされます。

キャッシュの有効期限が切れている場合、CSV ファイルが作成されダウンロードされる前にレポートが再生成されます。

レポートの CSV 形式には、パターン検出の出力から生成され、カテゴリタイプ、サブタイプ、重要度レベルで並べ替え、整理された情報が含まれます。 この形式は、Microsoft Excel などのアプリケーションでの表示や編集に適しています。 このツールは、繰り返し可能な形式であらゆる検索情報を提供することを目的としています。この形式は、レポートを長期的に比較し、進捗状況を測定するのに役立ちます。

CSV 形式レポートの列は次のとおりです。

* **コード**：カテゴリコード
* **タイプ**：カテゴリ名
* **サブタイプ**：カテゴリのサブタイプ
* **重要度**：重要レベル
* **識別子**：発見の主な識別子
* **メッセージ**：発見のために提供されたメッセージ
* **コンテキスト**：発見データの JSON 文字列

個々の検索条件の列の値「`\N`」は、データが提供されなかったことを示します。

## HTTP インターフェイス {#http-interface}

6.5 LTS Analyzerは、AEM内のユーザーインターフェイスの代わりに使用できるHTTP インターフェイスを提供します。 このインターフェイスは、`HEAD`と`GET`の両方のコマンドをサポートしています。 Analyzer レポートを生成し、JSON、CSV、タブ区切り値（TSV）の3つの形式のいずれかで返すために使用できます。

次のURLをHTTP アクセスで使用できます。ここで、`<host>`はAnalyzerがインストールされているサーバーのホスト名で、必要に応じてポートと共に使用します。

* `http://<host>/apps/aem66-analyzer/analysis/report.json` JSON 形式の場合
* `http://<host>/apps/aem66-analyzer/analysis/report.csv` CSV 形式の場合
* `http://<host>/apps/aem66-analyzer/analysis/report.tsv` TSV 形式の場合

### HTTP リクエストの実行 {#executing-an-http-request}

HTTP リクエストを実行する簡単な方法の1つは、管理者としてAEMに既にサインインしているブラウザーと同じブラウザーでタブを開くことです。 「ブラウザー」タブに URL を入力して、結果をブラウザーで表示またはダウンロードすることができます。

また、`curl` または `wget` などのコマンドラインツールおよび HTTP クライアントアプリケーションも使用できます。 認証済みのセッションで「ブラウザー」タブを使用しない場合は、コメントの一部として管理ユーザー名とパスワードを指定する必要があります。

次に、その方法の例を示します。

```shell
curl -u admin:admin 'http://localhost:4502/apps/aem66-analyzer/analysis/report.csv' > report.csv.
```

## キャッシュの有効期間の調整 {#adjusting-the-cache-lifetime}

AEM 6.5 LTS Analyzerのデフォルトのキャッシュ有効期間は24時間です。 レポートを更新し、キャッシュを再生成するオプションを使用すると、AEM インスタンスとHTTP インターフェイスの両方で、このデフォルト値がAEM 6.5 LTS アナライザーのほとんどの用途に適している可能性があります。 AEM インスタンスに対してレポート生成時間が特に長い場合は、レポートの再生成を最小限に抑えるためにキャッシュの有効期間を調整することをお勧めします。

キャッシュのライフタイム値は、次のリポジトリノードの`maxCacheAge` プロパティとして保存されます。

```
/apps/aem66-analyzer/content/modernizer/analyzer/jcr:content
```

このプロパティの値は、キャッシュの有効期間（秒）です。 管理者は、CRX／DE Lite を使用してキャッシュの有効期間を調整できます。

## コンテンツ変換サービスの使用 {#using-content-transformer}

### 入手方法 {#content-transformer-availability}

Content Transformerは、Software Distribution Portalからzip ファイルとしてダウンロードできるAEM 6.5 LTS Analyzerにバンドルされています。

### コンテンツ変換サービスを使用する際の重要な考慮事項 {#important-considerations-for-using-content-transformer}

コンテンツ トランスフォーマ（CT）を使用する際の重要な考慮事項については、次の節を参照してください。

* Content Transformerを使用するには、まずAEM環境でAEM Analyzerを実行する必要があります
* 本番環境でコンテンツ変換サービスを実行できますが、本番環境のクローンでコンテンツ変換サービスを実行することをお勧めします。 さらに重要なのは、AEM AnalyzerとCTが同じ環境で実行されていることを確認する必要があります
* コンテンツ トランスフォーマを実行する環境の管理者である必要があります
* ソースの内容を変更できる削除操作では、変換前にデフォルトで`/etc/packages/modernizer-content-transformation`の下のソースパスのバックアップパッケージが作成されます。 「操作を削除」ダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、「パッケージ作成を有効にする」を常に選択することを強くお勧めします
* Content Transformerの各ページには、最大50個の結果が一覧表示されるように設定されています。 したがって、一度に最大50個の調査結果を変換できます。 これは、UIでタイムリーな応答を提供するために行われます。

### コンテンツ変換サービスを開く {#opening-the-content-transformer}

1. ソース AEM インスタンスに管理者としてログインし、*https://host:port/aem/start.htm*&#x200B;のスタートページに移動します
1. **ツール – オペレーション - 6.5 LTS Modernizer**&#x200B;に移動します

   ![ コンテンツ トランスフォーマ 1](/help/sites-deploying/assets/opening-content-transformer-1.png)を開いています

1. 6.5 LTS アナライザーレポート **の** Content Transformer カードをクリックします

   ![ コンテンツ トランスフォーマ 2](/help/sites-deploying/assets/opening-content-transformer-2.png)を開いています

1. アナライザーレポートが生成されない場合、**コンテンツの変換** ページには&#x200B;**レポートなし**&#x200B;と表示されます。 コンテンツに関連するすべての調査結果が削除された場合、同じ&#x200B;**レポートなし** メッセージも表示されます

   ![ コンテンツ トランスフォーマ 3](/help/sites-deploying/assets/opening-content-transformer-3.png)を開いています

1. 以下に、AEM Analyzer レポートの作成が成功した場合と、コンテンツに関連する問題が見つかった場合に、Content Transformerの概要ページがどのように表示されるかを示す例を示します。

AEM Analyzer レポートの有効期限がサイドパネルに表示されます。 コンテンツ関連の結果を見落とさないようにするには、最新のAEM Analyzer レポートでContent Transformerを実行することをお勧めします

![ コンテンツ トランスフォーマ 4](/help/sites-deploying/assets/opening-content-transformer-4.png)を開いています

1. パターンコード、サブタイプ、重要度、Sourceに基づいて問題をフィルタリングできます

   ![ コンテンツ トランスフォーマ 5](/help/sites-deploying/assets/opening-content-transformer-5.png)を開いています

### パスの削除 {#removing-paths}

1. すべての問題または特定の問題を選択し、**削除**&#x200B;を選択して解決できます

   ![ パス 1](/help/sites-deploying/assets/removing-paths-1.png)を削除しています

   >[!NOTE]
   >削除操作では、変換の前に、デフォルトで`/etc/packages/modernizer-content-transformation`の下にあるソースパスのバックアップパッケージが作成されます。 「操作を削除」ダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、「パッケージ作成を有効にする」を常に選択することを強くお勧めします。

   ![ パス 2](/help/sites-deploying/assets/removing-paths-2.png)を削除しています

1. パスの削除操作のために作成されたバックアップパッケージの例を以下に示します。 「**インストール**」をクリックして、ソースパスを復元できます

   ![ パス 3](/help/sites-deploying/assets/removing-paths-3.png)を削除しています

   >[!CAUTION]
   >
   >バックアップ パッケージが格納されている場所なので、`/etc/packages/modernizer-content-transformation`を削除しないでください。 この場所を削除してリポジトリのサイズを減らすことができるのは、これらのパッケージが不要になった場合のみです。

1. 必要に応じて、選択したコンテンツの結果を後で使用するためにパッケージ化できます。 これを行うには、含める調査結果を選択し、左上の「**パッケージ**」をクリックします。 パッケージ名を入力し、パッケージパスを選択し、**パッケージ** ボタンをクリックしてプロセスを完了します。

   ![ パス 3](/help/sites-deploying/assets/removing-paths-4.png)を削除しています

### 既知の問題 {#known-issues}

* 場合によっては、削除操作で通知が表示されることがあります：*「一部のパスが正常に削除されませんでした。ログを確認して、もう一度試してください。*」 ただし、パスが実際に削除された場合は、このメッセージを無視して構いません
* 同様に、パッケージ操作は次のエラーで失敗する可能性があります：*「目的の操作を実行する際にエラーが発生しました。ログを確認して、もう一度試してください。*」 これはセッションの有効期限が原因である可能性があります。 このような場合、操作を再試行すると、問題が解決されます。
