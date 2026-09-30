---
title: AEM 6.5からAEM 6.5へのLTS コンテンツの移行Oakのアップグレードを使用
description: Oak アップグレードツールを使用して、AEM 6.5からAEM 6.5 LTSにコンテンツを移行する方法について説明します
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8c4ffb0e-b4dc-4a81-ac43-723754cbc0de
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
source-wordcount: '580'
ht-degree: 2%
---
# AEM 6.5からAEM 6.5へのLTS コンテンツの移行Oakのアップグレードを使用 {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

このドキュメントでは、コンテンツリポジトリの移行に重点を置いて、Adobe Experience Managerを&#x200B;**6.5**&#x200B;から&#x200B;**6.5 LTS**&#x200B;にアップグレードする方法について説明します。 Oakのアップグレードツールを使用して、リポジトリ間でコンテンツを正確かつ制御しながら転送する方法について説明します。

## 前提条件 {#prerequisites}

移行を開始する前に、次の要件が満たされていることを確認してください。

1. Java互換性：Java™ 17で実行するには、AEM 6.5 LTSをインストールして設定する必要があります。 設定が完了したら、AEM インスタンスを起動し、すべてのバンドルがアクティブで問題なく実行されていることを確認します
1. システムリソース：移行プロセス中に両方のリポジトリを処理するのに十分なディスク容量とメモリが利用可能であることを確認します
1. Oak-upgrade Tool: [公式Maven リポジトリ ](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade)から`oak-upgrade` jarをダウンロードします。 バージョンが、AEM 6.5 LTSで使用されるOak コアバージョンと一致していることを確認します。 Oak アップグレードツールは、Oracle® Java™ 11以降で実行されます

## 移行プロセス {#step-by-step-migration-process}

### AEM 6.5およびAEM 6.5 LTSの停止 {#stopping-aem65-and-aem65lts}

移行を開始する前に、AEM 6.5およびAEM 6.5 LTS インスタンスを停止します。 これにより、リポジトリが安定した状態になり、移行中に追加の書き込みが発生しないようにします。

### AEM 6.5 インスタンスのバックアップ {#backing-up-the-aem65-instance}

まだ実行していない場合は、AEM 6.5 インスタンスの完全バックアップを作成します。

### Oak アップグレードツールを使用したコンテンツの移行 {#using-the-oak-upgrade-tool-for-content-migration}

Oakのアップグレードツールは、次に示すように、コマンドラインを介して実行されます。

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

以下に、必須のコマンドとオプションを示します。

**主要オプション**

* `--include-paths`：移行に含めるサブツリーを指定します。 コマンドの使用例については、次を参照してください。

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`：移行から特定のパスを除外します。 このオプションを使用する際は注意が必要です。パスがターゲットシステムに存在する場合は、パスが削除されます。 コマンドの使用例については、次を参照してください。

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`: デフォルトでは、Oak-upgradeはバイナリへの参照のみを移行し、実際のファイルは元のBLOB/データストアに残されます。 その結果、新しいリポジトリは依然としてバイナリのソースストアに依存しています。 リポジトリのコンテンツと共にバイナリを移行するには、`--copy-binaries` パラメーターを使用してすべてのバイナリデータを新しいストアにコピーします。次に示します。

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### チェックポイントの移行 {#migratiing-checkpoints}

古いSegmentMK リポジトリ（Oak 1.6以前）を新しいSegmentMK （Oak バージョン 1.6以上）に移行する場合、チェックポイントも移行されます。 このプロセスにより、新しいリポジトリでOakを初めて実行する際のインデックスの再作成が回避されます。 ただし、次の場合、チェックポイントは移行されません。

1. カスタムインクルード、除外、または結合パスが指定されているか
1. 参照によってバイナリがコピーされます。 ソースデータストアが指定されておらず、2つの異なるチェックポイントに同じパスの下に異なるバイナリが含まれています。

2つ目のケースでは、Oak-upgradeで次の警告が発生し、ブレークします。

```
Checkpoints are not copied, because no external datastore has been specified. This results in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

この問題を解決する最も簡単な方法は、コマンドラインオプションでソースデータストアを指定することです（例：`--src-datastore`または`--src-s3datastore`）。

警告も無視される可能性がありますが、この場合、リポジトリは最初の起動時に完全にインデックスが作成されます。 特に大規模な組織にとっては、長いプロセスかもしれません。 インデックス再作成プロセスが完了するまで、リポジトリは使用できません。 警告を抑制するには、`--skip-checkpoints` オプションを使用します。

また、AEMを開始する前に、[ オフラインのインデックス再作成](/help/sites-deploying/offline-reindexing.md)を使用してリポジトリをオフラインでインデックス再作成し、最初の起動時に完全なインデックス再作成を行わないようにすることもできます。

Oak アップグレードツールと高度な使用方法について詳しくは、[公式ドキュメント ](https://jackrabbit.apache.org/oak/docs/migration.html)を参照してください。
