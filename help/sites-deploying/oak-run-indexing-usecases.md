---
title: oak-run.jar でのインデックス作成のユースケース
description: Oak-run ツールを使用してインデックス作成を実行する様々なユースケースについて説明します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: a7a8a20a-e513-43df-80b7-1e6daf957f20
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: c191041a-8b54-4bde-9e43-bc8d8f8cea74
    internal-label: Deploying
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 47%
---
# oak-run.jar でのインデックス作成の使用例{#oak-run-jar-indexing-use-cases}

Oak-run は、コマンドラインでインデックス作成のユースケースをサポートします。AEM の JMX コンソールを使用したこれらのユースケースの実行は必要はありません。

Oak インデックスの管理に`oak-run.jar` index コマンド アプローチを使用する全体的な利点は次のとおりです。

* Oak-run インデックスコマンドは、AEM 6.4のリリース以降に新しいインデックスツールセットを提供します。
* Oak-run を使用すると、インデックス再作成の時間を短縮でき、大規模なリポジトリでのインデックス再作成時間を削減できます。
* Oak-run を使用すると、インデックス再作成中の AEM でのリソース消費を低減できるので、システム全体のパフォーマンスが向上します。
* Oak-run は out-of-band のインデックス再作成機能を備えており、実稼動環境を利用できる状態で、メンテナンスやダウンタイムが許容されない場合にインデックスを再作成する必要がある状況をサポートします。

以下の節では、コマンドの例を示します。 Oak-run インデックスコマンドは、すべての NodeStore および BlobStore 設定をサポートしています。 以下に示す例は、FileDataStoreとSegmentNodeStoreを持つ設定の例です。

## ユースケース 1 - インデックスの一貫性チェック {#usercase1indexconsistencycheck}

このユースケースは、インデックスの破損に関連しています。 以前は、破損しているインデックスを特定できない場合もありました。 このため、次の特長を持つツールが用意されています。

* すべてのインデックスに対してインデックスの一貫性チェックを実行し、有効なインデックスと無効なインデックスのレポートを提供します。
* このツールは、AEM にアクセスできない場合でも使用可能です。
* このツールは簡単に使用できます。

`--index-consistency-check`を使用して、壊れたインデックスを確認します。

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

この操作は、`indexing-result/index-consistency-check-report.txt`にレポートを生成します。 サンプルレポートについては、以下を参照してください。

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### メリット {#uc1benefits}

サポートおよびシステム管理者は、ツールを使用して、破損したインデックスをすばやく特定し、インデックスを再作成できます。

## ユースケース 2 - インデックス統計 {#usecase2indexstatistics}

クエリのパフォーマンスに関するいくつかのケースを診断するために、Adobeでは、多くの場合、お客様の設定から既存のインデックス定義とインデックス関連の統計情報が必要でした。 トラブルシューティングを容易にするために、Adobeでは次のツールを作成しました。

1. システムに存在するすべてのインデックス定義を 1 つの JSON ファイルにダンプします。

1. 既存のインデックスの重要な統計をダンプします。

1. オフライン分析のためにインデックスコンテンツをダンプします。

1. AEMにアクセスできない場合でも使用できます

上記の操作は、次のインデックスコマンドを使用して実行できます。

* `--index-info` - インデックスに関連するさまざまな統計を収集してダンプします。

* `--index-definitions` - インデックス定義を収集してダンプします。

* `--index-dump` - インデックスコンテンツをダンプします。

コマンドが実際にどのように機能するかについての例は、次を参照してください。

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

これらのレポートは、`indexing-result/index-info.txt` および `indexing-result/index-definitions.json` に生成されます。

さらに、Web コンソールを介して同じ詳細が提供され、設定ダンプ zipの一部になります。 この詳細には、次の場所からアクセスできます。

`https://serverhost:serverport/system/console/status-oak-index-defn`

### メリット {#uc2benefits}

このツールを使用すると、インデックス作成またはクエリの問題に関連するすべての必要な詳細をすばやく収集できるので、この情報の抽出にかかる時間を短縮できます。

## ユースケース 3 – インデックス再作成 {#usecase3reindexing}

[シナリオ](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)によっては、インデックス再作成の実行が必要な場合があります。 現在、CRXDEまたはIndex Manager ユーザーインターフェイスを使用して、インデックス定義ノードの`reindex` フラグを`true`に設定して、インデックスを再作成します。 フラグを設定すると、インデックス再作成が非同期で実行されます。 このフラグが設定されると、インデックス再作成が非同期的に行われます。

次に、インデックス再作成に関するいくつかの注意点を示します。

* インデックス再作成を `DocumentNodeStore` 設定で行うと、すべてのコンテンツがローカルにある `SegmentNodeStore` 設定で行う場合より、大幅に時間がかかります。

* 現在の設計では、インデックス再作成中に非同期インデクサーがブロックされます。他のすべての非同期インデックスが古くなり、インデックス作成中に更新が取得されません。 その結果、システムが使用中の場合、ユーザーは最新の結果を見ることができない可能性があります。
* インデックス再作成は、AEMの設定に大きな負荷がかかる可能性があり、エンドユーザーエクスペリエンスに影響を与える可能性のあるリポジトリ全体のトラバーサルを伴います。
* インデックス再作成にかなりの時間がかかる`DocumentNodeStore` インストールの場合、操作中にMongo データベース接続エラーが発生すると、インデックス作成が中断される可能性があります。 その場合は、インデックス作成を最初から再開する必要があります。


* テキスト抽出が原因で、インデックス再作成に時間がかかる場合があります。 このような問題は、PDF ファイルが多い設定で、テキスト抽出に費やした時間がインデックス作成時間に影響を与える場合に発生する可能性があります。

これらの目的を達成するために、Oak実行のインデックスツールは、必要に応じて使用できるインデックス再作成の様々なモードをサポートしています。 Oak-run index コマンドには、次の利点があります。

* **帯域外インデックス再作成** - Oakで実行するインデックス再作成は、実行中のAEM セットアップとは別に実行できるため、使用中のAEM インスタンスへの影響を最小限に抑えることができます。

* **out-of-lane のインデックス再作成** - インデックス再作成は、インデックス作成操作に影響を与えずに行われます。 非同期インデクサーは、他のインデックスを引き続きインデックス化できます。

* **インストールでの簡略化されたインデックス再作成** - `DocumentNodeStore`DocumentNodeStore インストールでは、インデックス再作成が単一のコマンドで実行できます。これにより、インデックス再作成が確実に最適な方法で実行されます。

* **インデックス定義の更新および新しいインデックス定義の導入のサポート**

### インデックス再作成 - DocumentNodeStore {#reindexdocumentnodestore}

`DocumentNodeStore`回のインストールでは、1つのOak実行コマンドを使用してインデックス再作成を実行できます。

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

この操作には、次の利点があります。

* 実行中の AEM インスタンスへの影響が少ない。 ほとんどの読み取りはセカンダリサーバーから実行できます。実行中の AEM のキャッシュは、インデックス再作成に必要とされるトラバーサルをすべて考慮しても、悪影響は受けません。
* ユーザーは、`--index-definitions-file` オプションを使用して新しいインデックスまたは更新されたインデックスの JSON を提供することもできます。

### インデックス再作成 - SegmentNodeStore {#reindexsegmentnodestore}

`SegmentNodeStore` インストールでは、次のいずれかの方法でインデックス再作成を行うことができます。

#### オンラインのインデックス再作成 – SegmentNodeStore {#onlinereindexsegmentnodestore}

既定の方法に従い、`reindex` フラグを設定してインデックス再作成を行います。

#### Online reindex - SegmentNodeStore - AEM インスタンスが実行中です {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

`SegmentNodeStore` インストールでは、セグメントファイルに読み取り／書き込みモードでアクセスできるのは 1 つのプロセスのみです。 そのため、Oakで実行するインデックス作成の一部の操作では、次の手順を手動で実行する必要があります。

1. ステップテキスト。
1. AEMが読み取り専用モードで使用するリポジトリと同じリポジトリに`oak-run`を接続します。
1. 次の例を使用して、インデックス作成を実行します。

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後に、上記のコマンドを実行した後、Oak-runがインデックスファイルを保存したパスから`IndexerMBean#importIndex`操作を介して、作成したインデックスファイルを読み込みます。

このシナリオでは、AEM サーバーを停止したり、新しいインスタンスをプロビジョニングしたりする必要はありません。 ただし、インデックス作成にはリポジトリ全体のトラバーサルが伴うので、インストールへの I/O 負荷が増加し、実行時のパフォーマンスに悪影響があります。

#### Online reindex - SegmentNodeStore - AEM インスタンスがシャットダウンされました {#onlinereindexsegmentnodestoreaeminstanceisdown}

`SegmentNodeStore`回のインストールでは、1つのOak実行コマンドを使用してインデックス再作成を実行できます。 ただし、AEM インスタンスをシャットダウンする必要があります。

次のコマンドを使用して、インデックス再作成を開始できます。

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

この方法と前述の方法の違いは、チェックポイントの作成とインデックスの読み込みが自動的に行われることです。 欠点は、処理中に AEM を終了する必要があることです。

#### アウトオブバンドの再インデックス - SegmentNodeStore {#outofbandreindexsegmentnodestore}

この使用例では、クローン作成された設定でインデックス再作成を実行して、実行中の AEM インスタンスへの影響を最小限に抑えることができます。

1. JMX操作を使用してチェックポイントを作成します。 [JMX コンソール &#x200B;](/help/sites-administering/jmx-console.md)に移動し、`CheckpointManager`を検索します。 次に、**createCheckpoint(long p1)** 操作をクリックして、秒単位の有効期限に大きい値（**2592000** など）を使用します。
1. `crx-quickstart` フォルダーを新しいコンピューターにコピーします。
1. Oak-run index コマンドを使用してインデックス再作成を実行します。

1. 生成されたインデックスファイルをAEM サーバーにコピーします。

1. JMX を使用してインデックスファイルを読み込みます。

この使用例では、データストアは別のインスタンスからアクセスできる必要があります。これは、`FileDataStore`がEBSのようなクラウドベースのストレージソリューションに存在する場合は不可能です。 この状況では、`FileDataStore`も複製されるシナリオは除外されます。 インデックス定義でフルテキストのインデックス作成が実行されない場合は、`DataStore` へのアクセスは必要ありません。

## ユースケース 4 - インデックス定義の更新 {#usecase4updatingindexdefinitions}

現在、[ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) パッケージを使用して、インデックス定義の変更を出荷できます。 コンテンツパッケージ内にインデックス定義を配信し、`reindex` フラグを`true`に設定してインデックス再作成を実行できます。


これは、インデックス再作成に時間がかからない小規模なインストールに適しています。 ただし、大きいリポジトリでは、インデックス再作成にかなりの時間がかかります。 このような場合は、Oak実行インデックスツールを使用できるようになりました。

oak-run では、インデックス定義を JSON 形式で提供したり、out-of-band モードでインデックスを作成したりすることができます。out-of-band モードの場合、ライブインスタンスでは変更が行われません。

このユースケースで考慮すべきプロセスは次のとおりです。

1. 開発者は、ローカルインスタンスのインデックス定義を更新し、`--index-definitions` オプションを使用してインデックス定義JSON ファイルを生成します。
1. 更新されたJSONは、システム管理者に与えられます。
1. システム管理者は帯域外アプローチに従い、別のインストールでインデックスを準備します。
1. 完了すると、生成されたインデックスファイルは、実行中のAEM インストールに読み込まれます。
