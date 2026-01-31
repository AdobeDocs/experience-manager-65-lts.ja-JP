---
title: Oak-upgrade を使用したAEM 6.5 からAEM 6.5 LTS へのコンテンツの移行
description: Oak-upgrade ツールを使用してAEM 6.5 からAEM 6.5 LTS にコンテンツを移行する方法について説明します
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8c4ffb0e-b4dc-4a81-ac43-723754cbc0de
source-git-commit: a85b54d5a7c3b00f95f439941a390dcfee883187
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Oak-upgrade を使用したAEM 6.5 からAEM 6.5 LTS へのコンテンツの移行 {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

このドキュメントでは、コンテンツリポジトリの移行に重点を置いて、Adobe Experience Managerを **6.5** から **6.5 LTS** にアップグレードする方法について説明します。 Oakアップグレード ツールを使用して、リポジトリ間でコンテンツを正確かつ制御可能に転送する方法について説明します。

## 前提条件 {#prerequisites}

移行を開始する前に、次の要件が満たされていることを確認します。

1. Java との互換性：AEM 6.5 LTS は、Java™ 17 で実行するようにインストールおよび設定する必要があります。 設定が完了したら、AEM インスタンスを起動し、すべてのバンドルがアクティブで問題なく動作していることを確認します
1. システムリソース：移行プロセス中に両方のリポジトリを処理するのに十分なディスク領域とメモリを確保してください
1. Oak アップグレードツール：（公式の Maven リポジトリ `oak-upgrade` から [&#x200B; jar をダウンロード &#x200B;](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) ます。 バージョンが、AEM 6.5 LTS で使用されるOak コアバージョンと一致していることを確認します。 Oak アップグレードツールは、Oracle® Java™ 11 以降で実行されます

## 移行プロセス {#step-by-step-migration-process}

### AEM 6.5 およびAEM 6.5 LTS の停止 {#stopping-aem65-and-aem65lts}

移行を開始する前に、AEM 6.5 およびAEM 6.5 LTS インスタンスを停止します。 これにより、リポジトリが安定した状態になり、移行中に追加の書き込みが行われなくなります。

### AEM 6.5 インスタンスのバックアップ {#backing-up-the-aem65-instance}

まだ完了していない場合は、AEM 6.5 インスタンスの完全バックアップを作成します。

### Oak-upgrade ツールを使用したコンテンツ移行 {#using-the-oak-upgrade-tool-for-content-migration}

Oak-Upgrade ツールは、次に示すように、コマンドラインを使用して実行されます。

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

次に、基本的なコマンドとオプションを示します。

**主要なオプション**

* `--include-paths`：移行に含めるサブツリーを指定します。 コマンドの使用方法については、次の例を参照してください。

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`：特定のパスを移行から除外します。 このオプションを使用する場合は注意が必要です。ターゲットシステムにパスが存在する場合は、削除されます。 コマンドの使用方法については、次の例を参照してください。

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`: デフォルトでは、Oakアップグレードはバイナリへの参照のみを移行し、実際のファイルは元の BLOB/データストアに残します。 その結果、新しいリポジトリは引き続きバイナリのソースストアに依存します。 リポジトリコンテンツと共にバイナリを移行するには、次に示すように、`--copy-binaries` パラメーターを使用してすべてのバイナリデータを新しいストアにコピーします。

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### チェックポイントの移行 {#migratiing-checkpoints}

古い SegmentMK リポジトリ（Oak 1.6 以前）を新しい SegmentMK （Oak バージョン 1.6 以降）に移行すると、チェックポイントも移行されます。 これにより、新しいリポジトリでOakを初めて実行する際に、インデックスを再作成するのを回避できます。 ただし、次の場合、チェックポイントは移行されません。

1. カスタムの包含、除外、結合のパスが指定されている。
1. バイナリが参照によってコピーされます。 ソースデータストアが指定されておらず、2 つの異なるチェックポイントに、同じパスの異なるバイナリが含まれています。

2 番目のケースでは、Oak-upgrade が次の警告を表示して中断します。

```
Checkpoints are not copied, because no external datastore has been specified. This results in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

この問題を修正する最も簡単な方法は、コマンドラインオプションでソースデータストアを指定することです（例：`--src-datastore` または `--src-s3datastore`）。

この警告は無視される場合もありますが、この場合は、最初の起動時にリポジトリのインデックスが完全に再作成されます。 特に大規模なインスタンスでは、時間がかかる場合があります。 リポジトリーは、インデックス再作成プロセスが完了するまで使用できません。 `--skip-checkpoints` オプションを使用して、警告を抑制します。

[&#x200B; オフラインでのインデックス再作成 &#x200B;](/help/sites-deploying/offline-reindexing.md) を使用して、AEMを起動する前にリポジトリのオフラインでのインデックス再作成を行って、最初の起動時に完全なインデックス再作成を行わないようにすることもできます。

Oakのアップグレードツールと高度な使用方法について詳しくは、[&#x200B; 公式ドキュメント &#x200B;](https://jackrabbit.apache.org/oak/docs/migration.html) を参照してください。
