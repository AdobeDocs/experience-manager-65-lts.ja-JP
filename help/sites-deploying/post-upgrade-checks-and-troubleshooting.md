---
title: アップグレード後のチェックおよびトラブルシューティング
description: アップグレード後に発生する可能性がある問題のトラブルシューティング方法について説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8b3d8d0f-10f7-4736-881d-8f1f21c69182
source-git-commit: a037dc7cbb13abfeb8a7289baded50d3d788cbf6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 80%

---

# アップグレード後のチェックおよびトラブルシューティング{#post-upgrade-checks-and-troubleshooting}

## アップグレード後のチェック {#post-upgrade-checks}

[インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)の後に、次のアクティビティを実行してアップグレードを完了してください。AEM 6.5 LTS jar でAEMが起動され、アップグレードされたコードベースがデプロイされていることを前提としています。

* [ログでアップグレードの成功を確認](#verify-logs-for-upgrade-success)

* [OSGi バンドルの確認](#verify-osgi-bundles)

* [Oak バージョンの確認](#verify-oak-version)

* [ページの初期検証](#initial-validation-of-pages)

* [スケジュールされたメンテナンス設定の確認](#verify-scheduled-maintenance-configurations)

* [レプリケーションエージェントの有効化](#enable-replication-agents)

* [スケジュール済みカスタムジョブの有効化](#enable-custom-scheduled-jobs)

* [テスト計画の実行](#execute-test-plan)


### ログでアップグレードの成功を確認 {#verify-logs-for-upgrade-success}

**upgrade.log**

以前は、インスタンスのアップグレード後の状態を調べるには、様々なログファイル、リポジトリの一部および Launchpad を慎重に調査する必要がありました。アップグレード後のレポートを生成すると、不具合があるアップグレードを稼動前に検出できることがあります。

この機能の主な目的は、アップグレードの成功を確認するために必要な、手動による解釈や複数のエンドポイントにわたる複雑な解析ロジックの必要性を減らすことです。このソリューションは、更新の成功または確認された失敗に外部の自動処理システムが対応するための明確な情報を提供することを目的としています。

具体的には、次のことが行われます。

* アップグレードフレームワークで検出されたアップグレードの失敗は、1 つのアップグレードレポートに一元化されます。
* アップグレードレポートには、手動で対応する必要がある事項が記載されています。

これに対応するために、`upgrade.log` ファイルにログを生成する方法が変更されました。

**error.log**

ターゲットバージョンの jar を使用した AEM の起動時および起動後に、error.log を注意深く確認してください。すべての警告やエラーを確認する必要があります。一般に、ログの先頭で問題を探すことをお勧めします。ログの後半で発生したエラーは、実際はファイルの前の方で発生した根本原因の副次的な影響である可能性があります。エラーや警告が繰り返し発生する場合は、以下の[アップグレードによる問題の分析](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)を参照してください。

### OSGi バンドルの確認 {#verify-osgi-bundles}

OSGi コンソール `/system/console/bundles` に移動し、開始されていないバンドルがあるかどうかを確認します。いずれかのバンドルがインストール済み状態の場合は、`error.log` を調べて根本的な問題を特定します。

### Oak バージョンの確認 {#verify-oak-version}

アップグレード後、Oakのバージョンが **1.68.x** に更新されていることがわかります。 Oak バージョンを確認するには、OSGi コンソールに移動し、Oak バンドル（Oak Core、Oak Commons、Oak Segment Tar）に関連付けられているバージョンを調べます。

### ページの初期検証 {#initial-validation-of-pages}

AEM の複数のページに対して初期検証を実行します。オーサー環境をアップグレードする場合は、開始ページとようこそページ（`/aem/start.html`、`/libs/cq/core/content/welcome.html`）を開きます。オーサー環境とパブリッシュ環境の両方で、アプリケーションページをいくつか開き、正しくレンダリングされるかどうかスモークテストを行います。問題が発生した場合は、`error.log` を調べてトラブルシューティングをおこないます。

### スケジュールされたメンテナンス設定の確認 {#verify-scheduled-maintenance-configurations}

#### データストアのガベージコレクションの有効化 {#enable-data-store-garbage-collection}

ファイルデータストアを使用する場合は、データストアのガベージコレクションタスクが有効になっていて、週別メンテナンスリストに追加されていることを確認します。手順については、[リビジョンクリーンアップ](/help/sites-administering/data-store-garbage-collection.md)を参照してください。

>[!NOTE]
>
>S3 カスタムデータストアのインストール環境の場合や、共有データストアを使用する場合、この手順はお勧めしません。

#### オンラインでのリビジョンクリーンアップの有効化 {#enable-online-revision-cleanup}

MongoMK または新しい TarMK セグメント形式を使用する場合は、リビジョンクリーンアップタスクが有効になっていて、日別メンテナンスリストに追加されていることを確認します。手順については、[リビジョンクリーンアップ](/help/sites-deploying/revision-cleanup.md)を参照してください。

### レプリケーションエージェントの有効化 {#enable-replication-agents}

パブリッシュ環境を完全にアップグレードして検証したら、オーサー環境でレプリケーションエージェントを有効にします。エージェントがそれぞれのパブリッシュインスタンスに接続できることを確認します。イベントの順序について詳しくは、[ アップグレード手順 ](/help/sites-deploying/upgrade-procedure.md) を参照してください。

### スケジュール済みカスタムジョブの有効化 {#enable-custom-scheduled-jobs}

この時点で、コードベースの一部としてのスケジュール済みジョブを有効にすることができます。

### テスト計画の実行 {#execute-test-plan}

[ コードとカスタマイズのアップグレード **の「テスト手順** セクション ](/help/sites-deploying/upgrading-code-and-customizations.md#testing-procedure-testing-procedure) の定義に従って、詳細なテスト計画を実行します。

## アップグレードに関する問題の分析 {#analyzing-issues-with-the-upgrade}

ここでは、AEM 6.5 LTS へのアップグレード手順で発生する可能性のあるいくつかの問題について説明します。

### パッケージとバンドルを更新できない  {#packages-and-bundles-fail-to-update}

アップグレード時にパッケージがインストールされなかった場合は、パッケージに含まれるバンドルも更新されません。この種の問題は、データストアの設定ミスが原因で発生します。また、この問題は、error.log で **ERROR** メッセージや **WARN** メッセージとしても出現します。このような場合はほとんど、デフォルトのログインが機能しない可能性があるので、CRXDE を直接使用して設定の問題を調べ、見つけることができます。

### アップグレードが実行されない {#the-upgrade-did-not-run}

準備手順を開始する前に、`java -jar aem-quickstart.jar` コマンドを使用して **source** インスタンスを実行することで、最初にインスタンスが実行されていることを確認します。 これは、quickstart.properties ファイルを正しく生成するために必要な手順です。このファイルがないと、アップグレードはうまくいきません。あるいは、ソースインスタンスのインストールフォルダーの `crx-quickstart/conf` の下を探して、このファイルが存在するかどうかを確認します。また、アップグレードを開始するためにAEMを起動する場合は、`java -jar <aem-quickstart-6.5-LTS.jar>` コマンドを使用してアップグレードを実行する必要があります。 起動スクリプトから起動した場合、AEM はアップグレードモードで起動しません。

### 一部の AEM バンドルがアクティブな状態に切り替わらない {#some-aem-bundles-are-not-switching-to-the-active-state}

起動しないバンドルがある場合は、未解決の依存関係がないかを確認してください。

この問題が発生し、その原因がパッケージのインストールの失敗にあり、その結果、バンドルがアップグレードされない場合は、新しいバージョンとの互換性がないと見なされます。この問題のトラブルシューティング方法について詳しくは、前述の&#x200B;**パッケージとバンドルを更新できない**&#x200B;を参照してください。

また、新しいAEM 6.5 LTS インスタンスのバンドルリストと、アップグレードされたインスタンスを比較して、アップグレードされなかったバンドルを検出することもお勧めします。 この比較によって、`error.log` で検索すべき問題を絞り込むことができます。

### カスタムバンドルがアクティブ状態に切り替わらない {#custom-bundles-not-switching-to-the-active-state}

カスタムバンドルがアクティブ状態に切り替わっていない場合は、変更された API を読み込んでいないコードが存在する可能性が最も高くなります。 これは、多くの場合、未解決の依存関係につながります。

また、問題の原因となった変更が必要だったかどうかを確認し、必要でなかった場合は元に戻すことをお勧めします。 さらに、パッケージエクスポートのバージョンが必要以上に増えていないかを確認し、意味のある厳密なバージョン定義に従ってください。

### error.log と upgrade.log の分析 {#analyzing-the-error.log-and-upgrade.log}

ほとんどの状況では、ログでエラーを調べて問題の原因を突き止める必要があります。ただし、アップグレードの場合は、古いバンドルが適切にアップグレードされていない場合があるので、依存関係の問題を監視する必要もあります。

そのための最適な方法は、現在発生している問題には関係がないと思われるメッセージをすべて削除して、error.log の情報を絞り込むことです。次のように grep などのツールを使用して実行できます。

```shell
grep -v UnrelatedErrorString
```

中には、即座に内容がわからないエラーメッセージもあります。その場合は、そのエラーメッセージが発生しているコンテキストを確認すると、エラーの発生場所の理解に役立ちます。以下のように使用して、エラーを区別することができます。

* `grep -B`（エラーの前の行を追加）

または

* `grep -A`（エラーの後の行を追加）

場合によっては、エラーが警告メッセージ内にも見つかることがあります。警告の状態につながる妥当なケースも存在し、それが実際にはエラーであるかどうかをアプリケーションで常に判断できるわけではないからです。これらの警告メッセージについても必ず確認してください。

### アドビサポートのご案内 {#contacting-adobe-support}

このページのアドバイスを実行しても問題が解決しない場合は、アドビサポートに連絡してください。担当ケースを担当するサポートエンジニアに可能な限り多くの情報を提供するには、アップグレードから `error.log` ファイルと `upgrade.log` ファイルを必ず含めてください。
