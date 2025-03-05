---
title: AEM Analyzer を使用したアップグレードの複雑性の評価
description: AEM アナライザーを使用して、アップグレードの複雑さを評価する方法を説明します。
topic-tags: upgrading
content-type: reference
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 2645745a83477509bac81cb5e122eabc44db3961
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 23%

---


# AEM Analyzer を使用したアップグレードの複雑性の評価 {#assessing-the-upgrade-complexity-with-the-aem-analyzer}

## 概要 {#overview}

AEM 6.5 LTS アナライザーは、6.5 LTS へのシームレスなアップグレードエクスペリエンスを提供するために更新が必要な領域を示すことで、現在のAEMの実装を評価します。

このツールは、リファクタリングの可能性がある領域を特定するレポートを生成します。

## AEM 6.5 LTS アナライザーレポート {#aem-65lts-analyzer-report}

AEM 6.5 LTS アナライザーレポートは、アップグレードの全般的な準備状況を大まかに理解するために使用します。 このレポートは、AEM 6.5 LTS へのアップグレードを正常に行うために対応が必要な問題について、カテゴリー別に考察しています。

AEM 6.5 LTS アナライザーレポートには、次のカテゴリが含まれます。

* リファクタリングが必要なアプリケーション機能
* サポートされている場所に移動する必要があるリポジトリ項目
* 設定の問題
* AEM 6.5 の機能は、新機能によって削除されたか、AEM 6.5 LTS で現在サポートされていません
* Java および Guava API の使用を削除

カテゴリ、およびそれらのカテゴリに関連する可能性のある影響や解決策に関する追加情報は、AEM 6.5 LTS アナライザーレポート内のリンクから提供されます。

## 入手方法 {#analyzer-availability}

AEM Analyzer は、[ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aemcloud.html) から zip ファイルでダウンロードできます。 [ パッケージマネージャー ](/help/sites-administering/package-manager.md) を使用して、このパッケージをソース AEM インスタンスにインストールできます。

## AEM Analyzer 使用時の重要な考慮事項 {#important-considerations-for-using-aem-analyzer}

AEM アナライザーを実行する際の重要な考慮事項については、次の節に従います。

* アナライザーレポートは、AEMの出力 [ パターン検出 ](/help/sites-deploying/pattern-detector.md) を使用して作成されています。 Analyzer で使用するパターン検出ツールのバージョンは、AEM Analyzer のインストール・パッケージに含まれています
* AEM Analyzer を実行できるのは、**admin** ユーザーまたは **administrators** グループに属するユーザーのみです
* Analyzer は、バージョン 6.5 以降のAEM インスタンスでサポートされます。

>[!NOTE]
>
>ビジネスクリティカルなインスタンスへの影響を回避するために、カスタマイズ、設定、コンテンツ、ユーザーアプリケーションの領域で、実稼動環境にできる限り近いステージング環境でAEM アナライザーを実行することをお勧めします。 または、実稼動版のオーサー環境のクローンで実行することもできます。

* AEM アナライザーのレポートコンテンツの作成には、数分から数時間もの長い時間がかかる場合があります。 所要時間は、AEM リポジトリコンテンツのサイズと特性、AEMのバージョン、その他の要因に大きく依存します
* レポートコンテンツの生成には多くの時間が必要になる場合があるので、コンテンツはバックグラウンドプロセスで生成され、キャッシュに保持されます。 レポートの表示とダウンロードは、期限が切れるか、レポートが明示的に更新されるまでコンテンツキャッシュを利用するので、比較的高速で行われます。レポートコンテンツの生成中、ブラウザータブを閉じて、後で戻って、キャッシュでそのコンテンツが使用可能になった時点でレポートを表示することができます。

## AEMアナライザーレポートの表示 {#viewing-the-aem-analyzer-report}

AEM アナライザーレポートを表示するには、次の手順に従います。

1. Adobe Experience Managerを選択し、**ツール/操作/6.5 LTS Modernizer** に移動します。

   ![ アナライザーレポート 1 を表示 ](/help/sites-deploying/assets/view-analyzer-report-1.png)

1. **AEM 6.5 LTS アナライザー** をクリックして開きます

   ![ アナライザーレポート 2 を表示 ](/help/sites-deploying/assets/view-analyzer-report-2.png)

1. 「**レポートを生成**」をクリックして、AEM アナライザーを実行します

   ![ アナライザーレポート 3 を表示 ](/help/sites-deploying/assets/view-analyzer-report-3.png)

1. AEM アナライザーでレポートを生成している間、ツールによる進行状況を画面で確認できます。 進行状況が完了率で表示されます。 分析された項目の数と結果の数も表示されます

   ![ アナライザーレポート 4 を表示 ](/help/sites-deploying/assets/view-analyzer-report-4.png)

1. 6.5 LTS アナライザーレポートが生成されると、結果の概要と数が、結果のタイプと重要度レベルで整理された表形式で表示されます。 特定の検索結果の詳細を取得するには、テーブルの検索結果の種類に対応する番号をクリックします

   ![ アナライザーレポート 5 を表示 ](/help/sites-deploying/assets/view-analyzer-report-5.png)

1. 「**CSV に書き出し**」をクリックすると、レポートをコンマ区切り値（CSV）形式でダウンロードできます。キャッシュをクリアしてレポートを再生成するには、[**レポートの更新**] をクリックします。 キャッシュの有効期限が切れた場合は、レポートを再生成する必要があります。

## AEM アナライザーレポートの説明 {#interpreting-the-aem-analyzer-report}

6.5 LTS アナライザーツールをAEM インスタンスで実行すると、レポートがツールウィンドウに結果として表示されます。

レポートの形式は次のとおりです。

* **レポートの概要**：次の情報を含む、レポート自体に関する情報。

   * **レポート時間**：レポートコンテンツが生成され、最初に使用可能になった日時
   * **有効期限**：レポートコンテンツのキャッシュがいつ期限切れになるか
   * **生成期間**: レポートが生成された時間
   * **結果数**：レポートに含まれる結果の合計数

* **システム概要**:Analyzer が実行されたAEMシステムに関する情報
* **発見カテゴリ**：各セクションが同じカテゴリの 1 つ以上の発見に対応する複数セクション。各セクションには次の内容が含まれます。カテゴリ名、サブタイプ、発見数と重要度、概要、カテゴリドキュメントへのリンク、個々の発見情報。

  ![ アナライザーレポートの概要 ](/help/sites-deploying/assets/analyzer-report-summary.png)

  アクションの大まかな優先度を示すために、各発見に重要度レベルが割り当てられます。

>[!NOTE]
>
>各カテゴリの検索について詳しくは、[パターン検出のカテゴリ](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/aso)を参照してください。

重要度レベルを理解するには、次の表に従います。

| 重要度 | 説明 |
|---|---|
| INFO | 情報提供の目的で提供されます。 |
| ADVISORY | アップグレードに関する問題の可能性があります。さらに調査を行うことをお勧めします。 |
| CRITICAL | アップグレードの問題が発生する可能性が高く、機能やパフォーマンスの低下を防ぐために対処する必要があります。 |

## AEM 6.5 LTS アナライザーの CSV レポートの説明 {#interpreting-the-aem-65lts-analyzer-report}

AEM インスタンスで「**CSV**」オプションをクリックすると、アナライザーレポートの CSV フォーマットはコンテンツキャッシュから作成され、ブラウザーに返されます。 ブラウザーの設定に応じて、このレポートは、デフォルト名が `report.csv` のファイルとして自動的にダウンロードされます。

キャッシュの有効期限が切れている場合、CSV ファイルが作成されダウンロードされる前にレポートが再生成されます。

レポートの CSV 形式には、パターン検出の出力から生成され、カテゴリタイプ、サブタイプ、重要度レベルで並べ替え、整理された情報が含まれます。この形式は、Microsoft Excel などのアプリケーションでの表示や編集に適しています。すべての検索情報を繰り返し可能な形式で提供し、レポートを経時的に比較して進行状況を測定する際に役立てることができるようにすることを目的としています。

CSV 形式レポートの列は次のとおりです。

* **コード**：カテゴリコード
* **タイプ**：カテゴリ名
* **サブタイプ**：カテゴリのサブタイプ
* **重要度**：重要レベル
* **識別子**：発見の主な識別子
* **メッセージ**：発見のために提供されたメッセージ
* **コンテキスト**：発見データの JSON 文字列

個々の検索結果の列の値「`\N`」は、データが指定されていないことを示します。

## HTTP インターフェイス {#http-interface}

6.5 LTS アナライザーは、AEM内のユーザーインターフェイスの代わりに使用できる HTTP インターフェイスを提供します。 このインターフェイスは、`HEAD` コマンドと `GET` コマンドの両方をサポートしています。 アナライザーレポートを生成し、JSON、CSV、タブ区切り値（TSV）の 3 つの形式のいずれかで返すために使用できます。

次の URL を使用して HTTP アクセスを行うことができます。`<host>` は Analyzer がインストールされているサーバのホスト名（必要に応じてポートとともに指定）。

* `http://<host>/apps/aem66-analyzer/analysis/report.json` JSON 形式の場合
* `http://<host>/apps/aem66-analyzer/analysis/report.csv` CSV 形式の場合
* `http://<host>/apps/aem66-analyzer/analysis/report.tsv` TSV 形式の場合

### HTTP リクエストの実行 {#executing-an-http-request}

HTTP リクエストを簡単に実行する方法の 1 つは、管理者として既にAEMにログインしているのと同じブラウザーでタブを開くことです。 「ブラウザー」タブに URL を入力して、結果をブラウザーで表示またはダウンロードすることができます。

また、`curl` または `wget` などのコマンドラインツールおよび HTTP クライアントアプリケーションも使用できます。認証済みのセッションで「ブラウザー」タブを使用しない場合は、コメントの一部として管理ユーザー名とパスワードを指定する必要があります。

これを行う方法の例を次に示します。

```shell
curl -u admin:admin 'http://localhost:4502/apps/aem66-analyzer/analysis/report.csv' > report.csv.
```

## キャッシュ有効期間の調整 {#adjusting-the-cache-lifetime}

AEM 6.5 LTS Analyzer のデフォルトのキャッシュ有効期間は 24 時間です。 AEM インスタンスと HTTP インターフェイスの両方でレポートの更新とキャッシュの再生成を行うオプションがあるので、このデフォルト値は、多くの場合、AEM 6.5 LTS アナライザーの使用に適しています。 AEM インスタンスに対してレポート生成時間が特に長い場合は、レポートの再生成を最小限に抑えるためにキャッシュの有効期間を調整することをお勧めします。

キャッシュの有効期間の値は、次のリポジトリーノードに `maxCacheAge` プロパティとして保存されます。

```
/apps/aem66-analyzer/content/modernizer/analyzer/jcr:content
```

このプロパティの値は、キャッシュの有効期間（秒）です。管理者は、CRX／DE Lite を使用してキャッシュの有効期間を調整できます。

## コンテンツ変換サービスの使用 {#using-content-transformer}

### 入手方法 {#content-transformer-availability}

Content Transformer は、AEM 6.5 LTS アナライザーにバンドルされており、ソフトウェア配布ポータルから zip ファイルでダウンロードできます。

### コンテンツ変換サービスを使用する際の重要な考慮事項 {#important-considerations-for-using-content-transformer}

コンテンツトランスフォーマー（CT）を使用する際の重要な考慮事項については、次の節を参照してください。

* Content Transformer を使用するには、まずAEM環境でAEM アナライザーを実行する必要があります
* 実稼動環境でコンテンツ変換サービスを実行できますが、実稼動環境のクローンでコンテンツ変換サービスを実行することをお勧めします。さらに重要なのは、AEM アナライザーと CT を同じ環境で実行している必要があることです
* コンテンツトランスフォーマーを実行する環境の管理者である必要があります
* ソースコンテンツを変更できる削除操作では、デフォルトで、変換前にソースパスのバックアップパッケージが `/etc/packages/modernizer-content-transformation` 下に作成されます。 削除オペレーションダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、常に「パッケージの作成を有効にする」を選択することを強くお勧めします
* Content Transformer の各ページは、最大 50 個の結果をリストするように設定されています。 したがって、一度に変換できる結果は最大 50 個までです。 これは、UI でタイムリーに応答するために行われます。

### コンテンツ変換サービスを開く {#opening-the-content-transformer}

1. ソース AEM インスタンスに管理者としてログインし、「スタート」ページ（*https://host:port/aem/start.htm*）に移動します
1. **ツール/操作/6.5 LTS Modernizer** に移動します。

   ![ コンテンツトランスフォーマー 1 を開く ](/help/sites-deploying/assets/opening-content-transformer-1.png)

1. **Content Transformer for 6.5 LTS Analyzer report** カードをクリックします。

   ![ コンテンツトランスフォーマー 2 を開く ](/help/sites-deploying/assets/opening-content-transformer-2.png)

1. アナライザーレポートが生成されない場合、「**コンテンツを変換** ページは **レポートなし** と表示されます。 コンテンツ関連のすべての結果が削除された場合にも、同じ **レポートなし** メッセージが表示されます

   ![ コンテンツトランスフォーマー 3 を開く ](/help/sites-deploying/assets/opening-content-transformer-3.png)

1. AEM アナライザーレポートの作成が成功した場合や、コンテンツ関連の問題が見つかった場合の「Content Transformer の概要」ページの表示例を以下に示します。

AEM アナライザーレポートの残りの有効期限がサイドパネルに表示されます。 コンテンツ関連の結果が見つからないようにするには、最新のAEM アナライザーレポートと共に Content Transformer を実行することをお勧めします

![ コンテンツトランスフォーマー 4 を開く ](/help/sites-deploying/assets/opening-content-transformer-4.png)

1. このイシューは、パターンコード、サブタイプ、重要度、Sourceに基づいてフィルタリングできます

   ![ コンテンツトランスフォーマー 5 を開く ](/help/sites-deploying/assets/opening-content-transformer-5.png)

### パスの削除 {#removing-paths}

1. すべてのイシューまたは特定のイシューを選択し、「**削除**」を選択して解決できます

   ![ パス 1 を削除しています ](/help/sites-deploying/assets/removing-paths-1.png)

   >[!NOTE]
   >削除操作は、デフォルトで、変換の前に、`/etc/packages/modernizer-content-transformation` の下にソースパスのバックアップパッケージを作成します。 削除オペレーションダイアログには、バックアップパッケージの作成を無効または有効にするオプションがありますが、常に「パッケージの作成を有効にする」を選択することを強くお勧めします。

   ![ パス 2 を削除しています ](/help/sites-deploying/assets/removing-paths-2.png)

1. 次に、パスの削除操作用に作成されたバックアップパッケージの例を示します。 「**インストール**」をクリックして、ソースパスを戻すことができます

   ![ パス 3 を削除しています ](/help/sites-deploying/assets/removing-paths-3.png)

   >[!CAUTION]
   >
   >`/etc/packages/modernizer-content-transformation` はバックアップパッケージが存在する場所なので、削除しないでください。 これらのパッケージがこれ以上必要ないと確信できる場合にのみ、この場所を削除してリポジトリサイズを小さくすることができます。

1. オプションで、選択したコンテンツの結果を後で使用するためにパッケージ化できます。 それには、含める結果を選択し、左上の「**パッケージ**」をクリックします。 パッケージ名を入力してパッケージパスを選択し、「**パッケージ**」ボタンをクリックしてプロセスを完了します。

   ![ パス 3 を削除しています ](/help/sites-deploying/assets/removing-paths-4.png)

### 既知の問題 {#known-issues}

* 削除操作で「*一部のパスが正常に削除されていません。ログを確認して、もう一度試してください。*」と表示されます。 ただし、パスが実際に削除されている場合は、このメッセージを無視しても問題ありません
* 同様に、パッケージ操作が次のエラーで失敗する場合があります。*「目的の操作を実行中にエラーが発生しました。ログを確認して、もう一度試してください。*」と表示されます。 これは、セッションの有効期限が切れていることが原因である可能性があります。 このような場合は、操作を再試行すると問題が解決します。





