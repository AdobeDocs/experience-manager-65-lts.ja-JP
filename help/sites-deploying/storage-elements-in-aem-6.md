---
title: AEM 6.5 LTS のストレージ要素
description: AEM 6.5 LTS で使用可能なノードストレージ実装およびリポジトリのメンテナンス方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: e51842b5-fa91-42d2-a490-5a7e867dada7
source-git-commit: 0e60c406a9cf1e5fd13ddc09fd85d2a2f8a410f6
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 75%

---

# AEM 6.5 LTS のストレージ要素{#storage-elements-in-aem}

この記事では、次の内容について説明します。

* [AEM 6.5 LTS のストレージの概要](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [リポジトリのメンテナンス](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6.5 LTS のストレージの概要 {#overview-of-storage-in-aem}

AEM 6.5 LTS で最も重要な変更の 1 つは、リポジトリレベルでのイノベーションです。

現在、AEM 6.5 LTS では 2 つのストレージ実装（Tar ストレージと MongoDB ストレージ）を使用できます。

### Tar ストレージ {#tar-storage}

#### 新規にインストールした AEM インスタンスと Tar ストレージの実行 {#running-a-freshly-installed-aem-instance-with-tar-storage}

デフォルトでは、AEM 6.5 LTS は Tar ストレージを使用して、デフォルトの設定オプションを使用してノードとバイナリを保存します。 次の操作を行うことで、ストレージ設定を手動で設定できます。

1. AEM 6.5 LTS クイックスタート jar をダウンロードして、新しいフォルダーに配置します。
1. 次を実行して AEM を解凍します。

   `java -jar <aem-65-lts>.jar -unpack`

1. インストールディレクトリ内に `crx-quickstart\install` というフォルダーを作成します。

1. 新しく作成したフォルダー内に `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` というファイルを作成します。

1. ファイルを編集して、設定オプションを指定します。AEM Tar ストレージ実装の基盤となるセグメントノードストアでは、次のオプションを使用できます。

   * `repository.home`：リポジトリのホームのパスで、リポジトリ関連の様々なデータが格納されます。デフォルトでは、crx-quickstart/segmentstore ディレクトリにセグメントファイルが格納されます。
   * `tarmk.size`：セグメントの最大サイズ（MB 単位）です。デフォルトは 256 MB です。

1. AEM を起動します。

### Mongo ストレージ {#mongo-storage}

>[!NOTE]
>
>Mongo のサポートされている最小バージョンは Mongo 6 です。

#### 新規にインストールした AEM インスタンスと Mongo ストレージの実行 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

次の手順に従って、AEM 6.5 LTS を MongoDB ストレージと共に実行するように設定できます。

1. AEM 6.5 LTS クイックスタート jar をダウンロードし、新しいフォルダーに配置します。
1. 次のコマンドを実行して AEM を解凍します。

   `java -jar <aem-65-lts>.jar -unpack`

1. MongoDB がインストールされていること、および `mongod` のインスタンスが実行されていることを確認します。詳しくは、[MongoDB のインストール](https://docs.mongodb.org/manual/installation/)を参照してください。
1. インストールディレクトリ内に `crx-quickstart\install` というフォルダーを作成します。
1. 使用する設定の名前を持つ設定ファイルを `crx-quickstart\install` ディレクトリに作成することで、ノードストアを設定します。

   ドキュメントノードストア（AEM の MongoDB ストレージ実装の基盤）では、`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` というファイルを使用します。

1. ファイルを編集して、設定オプションを指定します。以下のオプションが利用できます。

   * `mongouri`：Mongo データベースに接続するために必要な [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) です。デフォルトは `mongodb://localhost:27017` です
   * `db`：Mongo データベースの名前です。新しいAEM 6.5 LTS のインストールでは、デフォルトのデータベース名として **aem-author** を使用します。
   * `cache`：キャッシュサイズ（メガバイト単位）です。このキャッシュサイズは、DocumentNodeStore で使用される様々なキャッシュに分散されます。デフォルトは 256 です。
   * `changesSize`：Mongo で差分出力のキャッシュに使用される capped コレクションのサイズ（MB 単位）です。デフォルトは 256 です。
   * `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。デフォルトは false です。

1. 使用するデータストアの PID を持つ設定ファイルを作成し、そのファイルを編集して設定オプションを指定します。詳しくは、[ノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

1. 次のコマンドを実行して、AEM 6.5 LTS jar を MongoDB ストレージバックエンドと共に起動します。

   ```shell
   java -jar <aem-65-lts>.jar -r crx3,crx3mongo
   ```

   バックエンドの実行モードが **`-r`** の場合、MongoDB のサポートで始まる例です。

#### Transparent Huge Pages の無効化 {#disabling-transparent-huge-pages}

Red Hat Linux では、Transparent Huge Pages（THP）と呼ばれるメモリ管理アルゴリズムが使用されます。AEM は詳細な読み取りと書き込みを実行しますが、THP は大規模な操作に最適化されています。したがって、Tar と Mongo ストレージの両方で THP を無効にすることをお勧めします。アルゴリズムを無効にするには、次の手順に従います。

1. `/etc/grub.conf` ファイルを任意のテキストエディターで開きます。
1. **grub.conf** ファイルに次の行を追加します。

   ```
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が反映されていることを確認します。

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効になっている場合、上記のコマンドの出力は次のようになります。

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>次のリソースを参照してください。
>
>* Red Hat® Linux® の Transparent Huge Pages について詳しくは、Red Hat® カスタマーポータルの [Red Hat Enterprise Linux 6、7 および 8 で Transparent Huge Page を使用、監視、無効化するにはどうすればよいですか？](https://access.redhat.com/solutions/46111)の記事を参照してください。
>* Linux® のチューニングのヒントについて詳しくは、[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)を参照してください。
>

## リポジトリのメンテナンス {#maintaining-the-repository}

リポジトリを更新するたびに、コンテンツのリビジョンが作成されます。その結果、更新のたびにリポジトリのサイズが大きくなります。リポジトリの制御不能な増加を回避するには、古いリビジョンをクリーンアップして、ディスクリソースを解放する必要があります。このメンテナンス機能は、リビジョンクリーンアップと呼ばれます。リビジョンクリーンアップのメカニズムによって、ディスク領域を再利用するために、リポジトリから古いデータが削除されます。リビジョンクリーンアップについて詳しくは、[リビジョンクリーンアップのページ](/help/sites-deploying/revision-cleanup.md)を参照してください。
