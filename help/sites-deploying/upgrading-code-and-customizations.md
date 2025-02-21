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
source-git-commit: 168e9f5865d20a53f9abed4bb90aceae9a1c7b6a
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 49%

---

# コードのアップグレードとカスタマイズ{#upgrading-code-and-customizations}

アップグレードを計画するときは、実装の次の領域を調査して対処する必要があります。

* [コードベースのアップグレード](#upgrade-code-base)
* [6.5 のリポジトリ構造への準拠](#align-repository-structure)
* [AEM のカスタマイズ](#aem-customizations)
* [手順のテスト](#testing-procedure)

## 概要 {#overview}

1. **AEM アナライザー** - アップグレード計画の説明と、「AEM アナライザーによるアップグレードの複雑性の評価 [ ページで詳しく説明しているように、AEM アナライザーを実行し ](/help/sites-deploying/pattern-detector.md) す。 Target バージョンのAEMで使用できない API やバンドルに加え、対処する必要がある領域の詳細を含むAEM アナライザーレポートが得られます。 PAEM アナライザーレポートは、コードに互換性のない箇所があることを示します。 何も存在しない場合、デプロイメントはすでに 6.5 LTS 互換です。 6.5 LTS 機能を使用するために新しい開発を行うことは引き続き選択できますが、互換性を維持するためだけの開発は必要ありません。

1. **6.5 LTS のコードベースの開発** - Target バージョンのコードベース専用のブランチまたはリポジトリを作成します。 アップグレード前の互換性の情報を使用して、更新するコードの領域を計画します。
1. **6.5 LTS Uber Jar でのコンパイル** - 6.5.2025 Uber Jar を指すようにコードベース POM を更新し、それに対してコードをコンパイルします。
1. **6.5 LTS 環境へのデプロイ** - AEM 6.5 LTS のクリーンなインスタンス（オーサー+ パブリッシュ）を開発環境と QA 環境で立ち上げる必要があります。 更新したコードベースと、現在の実稼動環境にある代表的なコンテンツのサンプルをデプロイする必要があります。
1. **QA 検証とバグ修正** - QA では、6.5.2025 のオーサーインスタンスとパブリッシュインスタンスの両方でアプリケーションを検証する必要があります。検出されたバグは修正し、6.5 LTS コードベースにコミットする必要があります。 すべてのバグが修正されるまで、必要に応じて開発サイクルを繰り返します。

アップグレードを進める前に、AEM 6.5 LTS に対して徹底的にテストされた、安定したアプリケーションコードベースが必要です。

## コードベースのアップグレード {#upgrade-code-base}

### Version Control {#create-a-dedicated-branch-for-6.5-lts-code-in-version-control} で 6.5 LTS コード専用のブランチを作成します。

AEM 実装に必要なすべてのコードおよび設定は、何らかの形式のバージョン管理を使用して管理する必要があります。AEM のターゲットバージョンのコードベースに必要な変更を管理するために、バージョン管理に専用ブランチを作成する必要があります。AEM のターゲットバージョンに対するコードベースの繰り返しテストとその後のバグ修正は、このブランチで管理されます。

### AEM Uber Jar バージョンの更新 {#update-the-aem-uber-jar-version}

AEM Uber Jar では、すべての AEM API を単一の依存関係として Maven プロジェクトの `pom.xml` に含めます。個々の AEM API の依存関係を含めるのではなく、Uber Jar を単一の依存関係として含めることが常にベストプラクティスです。コードベースをアップグレードする場合は、Uber Jar のバージョンをAEMの 6.5 LTS バージョンに変更します。 非推奨（廃止予定）の API やメソッドをアップデートして、対象バージョンのAEMと互換性を持つようにします。 新しいバージョンの Uber Jar に対してコードベースを再コンパイルします。

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
>AEM 6.5 とAEM 6.5 LTS Uber Jar のパッケージ化には、わずかな違いがあります。 以下の節を参照してください。

**AEM 6.5.x には、2 種類の Uber Jar があります**

1. `uber-jar-6.5.x.jar` - AEM 6.5.x のすべてのパブリック API が含まれます
1. `uber-jar-6.5.x-apis-with-deprecations.jar` - AEM 6.5.x のパブリック API と非推奨 API の両方が含まれています。

**AEM 6.5.2025.x の Uber Jar**

AEM 6.5.2025.x の場合、Uber Jar にも次の 2 種類があります。

1. `uber-jar-6.5.2025.x.jar` - AEM 6.5.2025.x のすべてのパブリック API が含まれます。
1. `uber-jar-6.5.2025.x-deprecated.jar` - AEM 6.5.2025.x からの非推奨（廃止予定）の API のみが含まれます

**主な違い：AEM 6.5.x とAEM 6.5.2025.x Uber Jar の比較**

* AEM 6.5.x では、パブリック API と非推奨（廃止予定） API の両方が必要な場合は、`pom.xml` ファイルに `uber-jar-6.5.x-apis-with-deprecations.jar` して include single jar を使用できます。
* AEM 6.5.2025.x では、パブリック API と非推奨（廃止予定） API の両方が必要な場合、パブリック API 用の `uber-jar-6.5.2025.x.jar` と非推奨（廃止予定） API 用の `uber-jar-6.5.2025.x-deprecated.jar` という 2 つの異なる jar を含める必要があります。
* AEM 6.5.2025.x では、パブリック API と非推奨（廃止予定） API の両方が必要な場合、パブリック API 用の `uber-jar-6.5.2025.x.jar` と非推奨（廃止予定） API 用の `uber-jar-6.5.2025.x-deprecated.jar` という 2 つの異なる jar を含める必要があります。

**非推奨（廃止予定）の API JAR の Maven 座標**

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 開発者向けメモ {#developer-notes}

* AEM 6.5.2025 には、Google guava ライブラリが標準で含まれていません。必要に応じて、必要なバージョンをインストールできます。
* Sling XSS バンドルで Java HTML Sanitizer ライブラリが使用されるようになりました。HTML コンテンツを安全にレンダリングするには、他の API にデータを渡すには、`XSSAPI#filterHTML()` メソッドを使用する必要があります。

## 手順のテスト {#testing-procedure}

アップグレードをテストするための包括的なテスト計画を準備する必要があります。アップグレードされたコードベースおよびアプリケーションのテストは、最初に下位レベルの環境で実行する必要があります。コードベースが安定するまで、検出されたすべてのバグを繰り返し修正します。より上位レベルの環境は、その後にアップグレードする必要があります。

### アップグレード手順のテスト {#testing-upgrade-procedure}

ここで説明されているアップグレード手順は、カスタマイズしたランブックに記載されているとおりに開発環境および QA 環境でテストする必要があります（[アップグレードの計画](/help/sites-deploying/upgrade-planning.md)を参照してください）。アップグレードの手順は、すべての手順がアップグレード実行ブックに記載され、アップグレードプロセスがスムーズになるまで繰り返す必要があります

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
   <td>AEM 実装および関連するコードを<br /> Dispatcher を介してパブリッシュ層でテストします。ページの更新および<br />キャッシュの無効化についての基準を含める必要があります。</td>
  </tr>
  <tr>
   <td>オーサリング</td>
   <td>AEM 実装と関連するコードをオーサー層でテストします。ページ、コンポーネントオーサリングおよびダイアログを含める必要があります。</td>
  </tr>
  <tr>
   <td>Experience Cloud ソリューションとの統合</td>
   <td>Analytics などの製品との統合を検証します。</td>
  </tr>
  <tr>
   <td>サードパーティシステムとの統合</td>
   <td>オーサー層とパブリッシュ層の両方で、サードパーティ統合を検証します。</td>
  </tr>
  <tr>
   <td>認証、セキュリティおよび権限</td>
   <td>LDAP／SAML などの認証メカニズムを検証する必要があります。<br /> 権限およびグループは、オーサー層とパブリッシュ層<br />の両方でテストする必要があります。</td>
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

前述の実装テスト領域をカバーするテスト計画を作成する必要があります。多くの場合、テスト計画をオーサーのタスクリストとパブリッシュのタスクリストに分けることをお勧めします。このテスト計画は、実稼動環境をアップグレードする前に、開発環境、QA 環境およびステージング環境で実行する必要があります。ステージング環境および実稼動環境をアップグレードするときに比較できるように、下位レベルの環境でテスト結果およびパフォーマンス指標を取得する必要があります。
