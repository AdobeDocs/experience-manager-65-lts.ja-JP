---
title: Oak-upgrade を使用したAEM 6.5 からAEM 6.5 LTS へのコンテンツの移行
description: oak-upgrade ツールを使用してAEM 6.5 からAEM 6.5 LTS にコンテンツを移行する方法について説明します
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8c4ffb0e-b4dc-4a81-ac43-723754cbc0de
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Oak-upgrade を使用したAEM 6.5 からAEM 6.5 LTS へのコンテンツの移行 {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

このドキュメントでは、Adobe Experience Managerをバージョン **6.5** から **6.5 LTS** にアップグレードするための包括的なガイドを、oak-upgrade ツールを使用したコンテンツリポジトリの移行に重点を置いて説明します。oak-upgrade ツールは、精度と制御により、異なるリポジトリ間でコンテンツを転送するための強力なユーティリティです。

## 前提条件 {#prerequisites}

移行を開始する前に、次の要件が満たされていることを確認します。

1. Java との互換性：AEM 6.5 LTS は、Java™ 17 で実行するようにインストールおよび設定する必要があります。 設定が完了したら、AEM インスタンスを起動し、すべてのバンドルがアクティブで問題なく動作していることを確認します
1. システムリソース：移行プロセス中に両方のリポジトリを処理するのに十分なディスク領域とメモリを確保してください
1. Oak アップグレードツール：（公式の Maven リポジトリ [ から `oak-upgrade` jar をダウンロード ](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) ます。 バージョンが、AEM 6.5 LTS で使用されている oak-core のバージョンと一致していることを確認します。 Oak アップグレードツールは、Oracle® Java™ 11 以降で実行されます

## ステップバイステップの移行プロセス {#step-by-step-migration-process}

### AEM 6.5 およびAEM 6.5 LTS の停止 {#stopping-aem65-and-aem65lts}

移行を開始する前に、AEM 6.5 およびAEM 6.5 LTS インスタンスを停止します。 これにより、リポジトリが安定した状態になり、移行中に追加の書き込みが行われなくなります。

### AEM 6.5 インスタンスのバックアップ {#backing-up-the-aem65-instance}

まだ完了していない場合は、AEM 6.5 インスタンスの完全バックアップを作成します。

### Oak-upgrade Tool を使用したコンテンツ移行 {#using-the-oak-upgrade-tool-for-content-migration}

Oak-Upgrade ツールは、次に示すように、コマンドラインを使用して実行されます。

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

次に、基本的なコマンドとオプションを示します。

**主要オプション**

* `--include-paths`：移行に含めるサブツリーを指定します。 コマンドの使用方法については、次の例を参照してください。

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`：特定のパスを移行から除外します。 このオプションを使用する場合は注意が必要です。パスがターゲットシステムに存在する場合は、削除されます。 コマンドの使用方法については、次の例を参照してください。

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`: デフォルトでは、oak-upgrade はバイナリへの参照のみを移行し、実際のファイルは元の BLOB/データストアに残ります。 その結果、新しいリポジトリは引き続きバイナリのソースストアに依存します。 リポジトリコンテンツと共にバイナリを移行するには、次に示すように、`--copy-binaries` パラメーターを使用してすべてのバイナリデータを新しいストアにコピーします。

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### チェックポイントの移行 {#migratiing-checkpoints}

古い SegmentMK リポジトリ（Oak 1.6 以前）を新しい SegmentMK （Oak バージョン 1.6 以降）に移行すると、チェックポイントも移行されます。 これにより、新しいリポジトリでOakが初めて実行される際に、インデックス再作成を避けることができます。 ただし、次の場合、チェックポイントは移行されません。

1. カスタムの包含、除外、結合のパスが指定されている。
1. バイナリは参照によってコピーされます。ソースデータストアが指定されておらず、2 つの異なるチェックポイントに同じパスの異なるバイナリが含まれています。

2 つ目のケースでは、oak-upgrade で次の警告が表示されて破損しています。

```
Checkpoints won't be copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

この問題を修正する最も簡単な方法は、コマンドラインオプションでソースデータストアを指定することです（例：`--src-datastore` または `--src-s3datastore`）。

この警告は無視される場合もありますが、この場合、リポジトリは最初の起動時に完全にインデックスが再作成されます。 これは、特に大きなインスタンスにとっては長いプロセスになる可能性があります。 リポジトリーは、インデックス再作成プロセスが完了するまで使用できません。 `--skip-checkpoints` オプションを使用して、警告を抑制します。

AEMを起動する前に、[ オフラインでのインデックス再作成 ](/help/sites-deploying/upgrade-offline-reindexing.md) を使用してリポジトリのオフラインでのインデックス再作成を行うこともできます。初回の起動時には、完全なインデックス再作成を回避してください。
