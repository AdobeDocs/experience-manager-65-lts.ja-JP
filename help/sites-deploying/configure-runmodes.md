---
title: 実行モード
description: 実行モードを使用して、特定の目的に合わせて AEM インスタンスを調整する方法を説明します。
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: b21555f2-bc07-4653-a5da-966b9aa7ea1f
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 96%

---

# 実行モード{#run-modes}

実行モードを使用すると、オーサーまたはパブリッシュ、テスト、開発、イントラネットなど、特定の目的に合わせて AEM インスタンスを調整できます。

以下の操作を実行できます。

* [各実行モードに対する設定パラメーターのコレクションを定義する](#defining-configuration-properties-for-a-run-mode)。

  すべての実行モードに対して基本的な設定パラメーターのセットが適用され、特定の環境の目的に合わせて追加のセットを調整できます。これらは必要に応じて適用されます。

* [特定のモード用にインストールする追加のバンドルを定義する](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

設定および定義はすべて 1 つのリポジトリに格納され、**実行モード**&#x200B;を設定することによってアクティベートされます。

## インストール実行モード {#installation-run-modes}

インストール（固定）実行モードは、インストール時に使用され、インスタンスの全期間にわたって固定されます。変更はできません。

インストール実行モードは標準で提供されています。

* `author`
* `publish`

これらは相互に排他的な実行モードの 2 つのペアです。例えば、次のことが可能です。

* `author` または `publish` を定義できますが、両方を同時に定義することはできません。

>[!CAUTION]
>
>上記のいずれかの実行モード（author、publish）を使用するときは、インストール時に使用する値が、そのインストールの *全期間* の実行モードを定義します。
>
>これらの実行モードは、インストール後は変更できません&#x200B;*。*

## カスタマイズされた実行モード {#customized-run-modes}

独自にカスタマイズした実行モードを作成することもできます。これらを組み合わせて、次のようなシナリオをカバーできます。

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 必要に応じて

カスタマイズされた実行モードは、起動のたびに選択することもできます。

## 実行モードの設定プロパティの定義 {#defining-configuration-properties-for-a-run-mode}

特定の実行モードで使用される設定プロパティの値のコレクションをリポジトリに保存できます。

実行モードは、フォルダー名の接尾辞で示されます。これにより、すべての設定を 1 つのリポジトリに保存できます。例：

* `config`

  すべての実行モードに適用される

* `config.author`

  オーサー実行モードに使用

* `config.publish`

  パブリッシュ実行モードに使用

* `config.<run-mode>`

  該当する実行モードに使用（config など）

これらのフォルダー内で個々の設定ノードを定義する方法と、複数の実行モードの組み合わせに対する設定を作成する方法について詳しくは、[リポジトリ内の OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)を参照してください。

>[!NOTE]
>
>[インストール実行モード](#installation-run-modes)（オーサーなど）の場合、インストール後に実行モードを変更できません。ただし、個々の設定プロパティに対する変更は、再起動時に有効になります。

## 実行モードにインストールする追加バンドルの定義 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

特定の実行モード用にインストールする必要がある追加のバンドルも指定できます。これらの定義に関しては、インストールフォルダーを使用してバンドルが保持されます。繰り返しになりますが、実行モードはプレフィックスで示されます。

* `install.author`
* `install.publish`

これらのフォルダーは、タイプが `nt:folder` であり、適切なバンドルを含む必要があります。

## 特定の実行モードでの CQ の起動 {#starting-cq-with-a-specific-run-mode}

複数の実行モードの設定を定義した場合は、起動時にどれを使用するかを定義する必要があります。使用する実行モードを指定する方法はいくつかあります。解決の順序は次のとおりです。

1. [システムプロパティ (](#using-a-system-property-in-the-start-script)
1. [&#128279;](#using-the-sling-properties-file)
1. [&#128279;](#using-the-r-option)
1. [ファイル名検出](#filename-detection-renaming-the-jar-file)

アプリケーションサーバーを使用している場合は、[web.xml で実行モードを定義](#defining-the-run-mode-in-web-xml-with-application-server)することもできます。

### sling.properties ファイルの使用 {#using-the-sling-properties-file}

`sling.properties` ファイルを使用して必要な実行モードを定義できます。

1. 設定ファイルを編集します。

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 次のプロパティを追加します。この例は、オーサーの場合です。

   `sling.run.modes=author`

### -r オプションの使用 {#using-the-r-option}

カスタム実行モードは、クイックスタート起動時に`-r`オプションを使用することで起動することができます。例えば、次のコマンドを使用して、実行モードを dev &grave;&grave; に設定したAEMインスタンスを起動してください。

```shell
java -jar cq-56-p4545.jar -r dev
```

### 起動スクリプトのシステムプロパティを使用 {#using-a-system-property-in-the-start-script}

起動スクリプトのシステムプロパティを使用して実行モードを指定できます。

* 例えば、US にある実稼動のパブリッシュインスタンスとしてインスタンスを起動するには、以下を使用します。

  `-Dsling.run.modes=publish,prod,us`

### ファイル名検出 - jar ファイルの名前変更 {#filename-detection-renaming-the-jar-file}

インストール前にインストール jar ファイルの名前を変更することにより、次の 2 つのインストール実行モードをアクティベートできます。

* publish
* author

jar ファイルでは、命名規則を使用する必要があります。

`cq5-<run-mode>-p<port-number>`

例えば、`publish` 実行モードを設定するには、jar ファイルの名前を次のように変更します。

`cq5-publish-p4503`

### web.xml での実行モードの定義（アプリケーションサーバーを使用） {#defining-the-run-mode-in-web-xml-with-application-server}

アプリケーションサーバーを使用している場合は、次のプロパティも設定できます。

`sling.run.modes`

プロパティを、次のファイル内で設定することもできます。

`WEB-INF/web.xml`

これは AEM の `war` ファイル内にあり、デプロイメントの前に更新する必要があります。

詳しくは、[AEM をアプリケーションサーバーと共にインストール](/help/sites-deploying/application-server-install.md)を参照してください。
