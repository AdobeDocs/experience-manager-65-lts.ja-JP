---
title: コードのアップグレードとカスタマイズ
description: AEM でのコードのアップグレードとカスタマイズについて説明します。
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 6b94caf1-97b7-4430-92f1-4f4d0415aef3
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
source-wordcount: '1104'
ht-degree: 49%
---
# コードのアップグレードとカスタマイズ{#upgrading-code-and-customizations}

アップグレードを計画するときは、実装の次の領域を調査して対処する必要があります。

* [コードベースのアップグレード](#upgrade-code-base)
* [手順のテスト](#testing-procedure)

## 概要 {#overview}

1. **AEM Analyzer** - アップグレード計画の説明に従ってAEM Analyzerを実行します。詳細については、[AEM Analyzerを使用したアップグレードの複雑さの評価](/help/sites-deploying/aem-analyzer.md) ページを参照してください。 Target バージョンのAEMで使用できないAPI/バンドルに加えて、対処する必要がある領域に関する詳細を含むAEM Analyzer レポートが表示されます。 AEM Analyzer レポートには、コードの互換性がないことが示されます。 存在しない場合、デプロイメントは既に6.5 LTSと互換性があります。 6.5 LTS機能を使用するための新しい開発を選択できますが、互換性を維持するためだけに必要はありません。
1. **6.5 LTSのコードベースを開発**- Target バージョンのコードベース用の専用ブランチまたはリポジトリを作成します。 アップグレード前の互換性の情報を使用して、更新するコードの領域を計画します。
1. **6.5 LTS Uber jarでコンパイルする**- 6.5 LTS Uber jarを指すようにコードベース POMを更新し、それに対してコードをコンパイルします。
1. **6.5 LTS Environment**&#x200B;へのデプロイ - AEM 6.5 LTS （Author + Publish）のクリーンなインスタンスをDev/QA環境で立ち上げる必要があります。 更新したコードベースと、現在の実稼動環境にある代表的なコンテンツのサンプルをデプロイする必要があります。
1. **QA検証とバグ修正** - QAは、6.5 LTSのオーサーインスタンスとパブリッシュインスタンスの両方でアプリケーションを検証する必要があります。 見つかったバグは修正し、6.5 LTS コードベースにコミットする必要があります。 すべてのバグが修正されるまで、必要に応じて開発サイクルを繰り返します。

アップグレードを進める前に、AEM 6.5 LTSに対して徹底的にテストされた安定したアプリケーションコードベースが必要です。

## コードベースのアップグレード {#upgrade-code-base}

### バージョン管理で6.5 LTS コードの専用ブランチを作成する {#create-a-dedicated-branch-for-6.5-lts-code-in-version-control}

AEM 実装に必要なすべてのコードおよび設定は、何らかの形式のバージョン管理を使用して管理する必要があります。 AEM のターゲットバージョンのコードベースに必要な変更を管理するために、バージョン管理に専用ブランチを作成する必要があります。 AEM のターゲットバージョンに対するコードベースの繰り返しテストとその後のバグ修正は、このブランチで管理されます。

### AEM Uber Jar バージョンの更新 {#update-the-aem-uber-jar-version}

AEM Uber Jar では、すべての AEM API を単一の依存関係として Maven プロジェクトの `pom.xml` に含めます。 個々の AEM API の依存関係を含めるのではなく、Uber Jar を単一の依存関係として含めることが常にベストプラクティスです。 コードベースをアップグレードする場合は、Uber Jarのバージョンを6.5 LTS バージョンのAEMを指すように変更します。 AEM のターゲットバージョンとの互換性を確保するために、廃止された API またはメソッドを更新します。 Uber Jar の新しいバージョンに対してコードベースを再コンパイルします。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>AEM 6.5とAEM 6.5 LTS Uber Jarのパッケージ方法にはわずかな違いがあります。 以下の節を参照してください。

AEM 6.5 **の** Uber Jar

1. `uber-jar-6.5.x.jar` - AEM 6.5のすべてのパブリック APIが含まれます。
1. `uber-jar-6.5.x-apis-with-deprecations.jar` - AEM 6.5のパブリック APIと非推奨のAPIの両方が含まれます。

AEM 6.5 LTS **の** Uber Jar

AEM 6.5 LTSの場合、Uber Jarには次の2種類があります。

1. `uber-jar-6.6.x-apis.jar` - AEM 6.5 LTSのすべてのパブリック APIが含まれています。
1. `uber-jar-6.6.x-deprecated-apis.jar` - AEM 6.5 LTSの非推奨APIのみが含まれます。

**主な違い：AEM 6.5とAEM 6.5 LTS Uber Jars**

* AEM 6.5では、公開APIと非推奨APIの両方が必要な場合は、`pom.xml` ファイルでinclude single jar、`uber-jar-6.5.x-apis-with-deprecations.jar`を使用できます。
* AEM 6.5 LTSでは、公開APIと非推奨APIの両方が必要な場合は、公開APIの場合は`uber-jar-6.6.x-apis.jar`、非推奨APIの場合は`uber-jar-6.6.x-deprecated-apis.jar`の2つの別々のjarを含める必要があります。

非推奨のAPI Jar **の** Maven座標

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 開発者向けメモ {#developer-notes}

* AEM 6.5 LTSには、Google guava ライブラリが標準で含まれていません。必要なバージョンは、必要に応じてインストールできます。
* Sling XSS バンドルはJava HTML Sanitizer ライブラリを使用するようになりました。`XSSAPI#filterHTML()` メソッドを使用してHTML コンテンツを安全にレンダリングする必要があります。他のAPIにデータを渡す必要はありません。
* Apache Felix HTTP SSL フィルター設定の更新：AEM 6.5 LTSでは、`org.apache.felix.http.sslfilter` バンドルがバージョン 1.2.6から2.0.2にアップグレードされました。 このアップグレードの一環として、OSGi設定のPID `org.apache.felix.http.sslfilter.SslFilter`は廃止され、新しいPID `org.apache.felix.http.sslfilter.Configuration`に置き換えられました。 デプロイメントでSSL フィルターを使用する場合、既存の設定をOSGi Configuration Manager （`/system/console/configMgr`）を使用して新しいPIDに手動で移行する必要があります。 設定を移行しないと、アップグレード後にSSL フィルターが期待どおりに適用されない場合があります。

## 手順のテスト {#testing-procedure}

アップグレードをテストするための包括的なテスト計画を準備する必要があります。 アップグレードされたコードベースおよびアプリケーションのテストは、最初に下位レベルの環境で実行する必要があります。 コードベースが安定するまで、検出されたすべてのバグを繰り返し修正します。より上位レベルの環境は、その後にアップグレードする必要があります。

### アップグレード手順のテスト {#testing-upgrade-procedure}

ここで説明されているアップグレード手順は、カスタマイズしたランブックに記載されているとおりに開発環境および QA 環境でテストする必要があります（[アップグレードの計画](/help/sites-deploying/upgrade-planning.md)を参照してください）。 アップグレード手順は、すべてのステップがアップグレードランブックに記載され、アップグレードプロセスが問題なく実行されるようになるまで繰り返す必要があります。

### 実装テスト領域  {#implementation-test-areas-}

環境がアップグレードされ、アップグレードされたコードベースがデプロイされた後のテスト計画でカバーする必要がある AEM 実装の重要な領域を次に示します。

<table>
 <tbody>
  <tr>
   <td><strong>機能テスト領域</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>公開済みサイト</td>
   <td>AEM 実装および関連するコードを<br /> Dispatcher を介してパブリッシュ層でテストします。 ページの更新および<br />キャッシュの無効化についての基準を含める必要があります。</td>
  </tr>
  <tr>
   <td>オーサリング</td>
   <td>AEM 実装と関連するコードをオーサー層でテストします。 ページ、コンポーネントオーサリングおよびダイアログを含める必要があります。</td>
  </tr>
  <tr>
   <td>Experience Cloud ソリューションとの統合</td>
   <td>Adobe Analyticsなどの製品との統合を検証する。</td>
  </tr>
  <tr>
   <td>サードパーティシステムとの統合</td>
   <td>オーサー層とパブリッシュ層の両方で、サードパーティ統合を検証します。</td>
  </tr>
  <tr>
   <td>認証、セキュリティおよび権限</td>
   <td>LDAP/SAMLなどの認証メカニズムを検証する必要があります。<br /> 権限とグループは、オーサー層とパブリッシュ層<br />の両方でテストする必要があります。</td>
  </tr>
  <tr>
   <td>クエリ</td>
   <td>カスタムインデックスおよびクエリは、クエリパフォーマンスと共にテストする必要があります。</td>
  </tr>
  <tr>
   <td>UI のカスタマイズ</td>
   <td>オーサー環境での AEM UI の拡張またはカスタマイズ。</td>
  </tr>
  <tr>
   <td>ワークフロー</td>
   <td>カスタムまたは標準のワークフローおよび機能。</td>
  </tr>
  <tr>
   <td>パフォーマンステスト</td>
   <td>実際のシナリオをシミュレートするオーサー層とパブリッシュ層の両方で負荷テストを実行する必要があります。</td>
  </tr>
 </tbody>
</table>

### テスト計画の作成および結果 {#document-test-plan-and-results}

前述の実装テスト領域をカバーするテスト計画を作成する必要があります。 多くの場合、テスト計画をオーサーのタスクリストとパブリッシュのタスクリストに分けることをお勧めします。 このテスト計画は、本番環境をアップグレードする前に、開発環境、QA 環境およびステージング環境で実行する必要があります。 ステージング環境および本番環境をアップグレードするときに比較できるように、下位レベルの環境でテスト結果およびパフォーマンス指標を取得する必要があります。
