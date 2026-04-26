---
title: インプレースアップグレードの実行
description: AEM 6.5 LTSのインプレースアップグレードを実行する方法について説明します。
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: c7351625-b29e-45a7-b966-e7c0f56d4f22
source-git-commit: f015c4fb30bbba2ec0de7290d37ee56e182d2ddc
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 46%

---

# インプレースアップグレードの実行 {#performing-an-in-place-upgrade}

>[!NOTE]
>
>このページでは、AEM 6.5 LTSのインプレースアップグレード手順の概要を説明します。 インストールがアプリケーションサーバーにデプロイされている場合は、[&#x200B; アプリケーションサーバーインストールのアップグレード手順](/help/sites-deploying/app-server-upgrade.md)を参照してください。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。 詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。 さらに、お使いのシステムがAEM 6.5 LTS[&#128279;](/help/sites-deploying/technical-requirements.md)の要件を満たしていることを確認し、[&#x200B; アップグレード計画に関する考慮事項](/help/sites-deploying/upgrade-planning.md)と、[Analyzer](/help/sites-deploying/pattern-detector.md)による複雑性の見積もり方法を確認してください。

## 移行の前提条件 {#migration-prerequisites}

* **必要なJava バージョンの最小値：** Oracle Java™ 17/21がシステムにインストールされていることを確認します。

## AEM クイックスタート jar ファイルの準備 {#prep-quickstart-file}

1. 新しいAEM 6.5 LTS jar ファイルのダウンロード

1. [適切なアップグレード開始コマンドの決定](#determining-the-correct-upgrade-start-command)

1. 実行中のインスタンスを停止します

1. 新しいAEM 6.5 LTS JARを使用して、`crx-quickstart` フォルダー外の古いJARを置き換えます

1. `sling.properties` ファイル （通常は`crx-quickstart/conf/`に存在）のバックアップを取り、それを削除します

1. 次のコマンドを実行して新しいクイックスタート jar を解凍します。

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

1. カスタム sling.propertiesを適用する必要がある場合は、新しいローカル AEM インスタンスを作成し、crx-quickstart/conf ディレクトリからsling.properties ファイルを取得します。 必要なカスタム変更をこのファイルに適用し、アップグレード中のAEM インスタンスのcrx-quickstart/conf ディレクトリにコピーします。 カスタムプロパティがない場合は、この手順をスキップできます。

<!--
Alexandru: drafting temporarily

## Content Repository Migration {#content-repository-migration}

This migration is not required if you are upgrading from AEM 6.3. For versions older than 6.3, Adobe provides a tool that can be used to migrate the repository to the new version of the Oak Segment Tar present in AEM 6.3. It is provided as part of the quickstart package and is mandatory for any upgrades that will be using TarMK. Upgrades for environments that are using MongoMK do not require repository migration. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool to simplify the upgrade and make it more robust.

>[!NOTE]
>
>If you are performing TarMK repository content migration using the CRX2Oak Quickstart extension, you might remove the **samplecontent** runmode by adding the following to the migration command line:
>
>* `--promote-runmode nosamplecontent`
>

To determine the command that you should run, use the following command:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

<table>
 <tbody>
  <tr>
   <td><strong>Source Repository</strong></td>
   <td><strong>Target Repository</strong></td>
   <td><strong>Profile</strong></td>
   <td><strong>Additional Flags</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 or TarMK with <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK or crx2 with <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>TarMK with no datastore</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No migration is needed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Where:**

* `mongo-host` is the MongoDB server IP (for example, 127.0.0.1)

* `mongo-port` is the MongoDB server port (for example: 27017)

* `mongo-database-name` represents the name of the database (for example: aem-author)

**You may also require additional switches for the following scenarios:**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, add the `--disable-mmap` parameter to the command.

For additional instructions on using the crx2oak tool, see Using the [CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md). The crx2oak helper JAR can be manually upgraded if needed, by manually replacing it with newer versions after unpacking the quickstart. Its location in the AEM installation folder is: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. The newest version of the CRX2Oak migration tool is available for download from the Adobe Repository at: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

If the migration has completed successfully, the tool will exit with an exit code of zero. Additionally, check for WARN and ERROR messages in the `upgrade.log` file, located under `crx-quickstart/logs` in the AEM installation directory, as these could indicate non-fatal errors that occurred during the migration.

Check the configuration files beneath `crx-quickstart/install` folder. If a migration was necessary these will be updated to reflect the target repository.

**A note on datastores:**

While `FileDataStore` is the new default for AEM 6.3 installations, using an external datastore is not required. While using an external datastore is recommended as a best practice for production deployments, it is not a prerequisite to upgrade. Due to the complexity already present in upgrading AEM, Adobe recommends performing the upgrade without doing a datastore migration. If desired, a datastore migration can be executed afterwards as a separate effort.

## Troubleshooting Migration Issues {#troubleshooting-migration-issues}

Skip this section if you are upgrading from 6.3. While the provided crx2oak profiles should meet the needs of most customers, there are times when additional parameters will be necessary. If you run into an error during your migration, it is possible that there are aspects of your environment that require additional configuration options to be provided. If so, you will likely encounter the following error:

**Checkpoints are not copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info.**

For some reason, the migration process needs access to binaries in the datastore and is unable to find it. To specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**For S3 datastores:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**For File datastores:**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

-->

## アップグレードの実行 {#performing-the-upgrade}

**S3 を使用している場合：**

1. 以前のバージョンの S3 コネクタに関連する、`crx-quickstart/install` 内の jar を削除します。

1. [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) <!-- Alexandru: this is a stub link for now -->から1.60.2 S3 コネクタの最新リリースをダウンロードします

1. S3 コネクタ （バージョン 1.60.2）を展開し、`crx-quickstart/install`の下にある次のフォルダーの内容を次のようにコピーします。

   1. `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/1`を`crx-quickstart/install/1`の下にコピー
   1. `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/15`を`crx-quickstart/install/15`の下にコピー

次に、[正しいアップグレード開始コマンドの決定](#determining-the-correct-upgrade-start-command) セクションの情報を使用して決定された新しいコマンドを使用して、AEM インスタンスを開始します。

### 適切なアップグレード開始コマンドの確認 {#determining-the-correct-upgrade-start-command}

>[!NOTE]
>
>Java 8/11引数の一部のサポートは、Java 17/21で削除されました。AEM 6.5 LTS[&#128279;](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations)の[Oracle Java™ 17 documents](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html)、[Oracle Java™ 21 documents](https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html)およびJava&amp;trade arguments considerationsを参照してください。

アップグレードを実行するには、jar ファイルを使用して AEM を起動し、インスタンスを起動することが重要です。

起動スクリプトから AEM を起動した場合、アップグレードは開始されません。 ほとんどの顧客は、起動スクリプトを使用して AEM を起動します。また、起動スクリプトをカスタマイズし、メモリ設定やセキュリティ証明書など、環境設定に関するスイッチを含めています。 そのため、次の手順に従って、適切なアップグレードコマンドを確認することをお勧めします。

1. 実行中の AEM インスタンスで、コマンドラインから次のコマンドを実行します。

   ```shell
   ps -ef | grep java
   ```

1. AEM プロセスを探します。 次のように表示されます。

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 既存のjarへのパス（この場合は`crx-quickstart/app/aem-quickstart*.jar`）を、`crx-quickstart` フォルダーの兄弟である新しいAEM 6.5 LTS jarに置き換えて、コマンドを変更します。 例として前述のコマンドを使用すると、コマンドは次のようになります。

   ```shell
   /usr/bin/java -server -Xmx4096m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar <AEM-6.5-LTS.jar> -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   これにより、適切なメモリ設定、カスタム実行モードおよびその他の環境パラメーターすべてがアップグレードに適用されます。 アップグレードが完了すると、それ以降の起動時には起動スクリプトからインスタンスを起動できます。

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

インプレースアップグレードプロセスが完了したら、更新したコードベースをデプロイする必要があります。 ターゲットバージョンの AEM で動作するようにコードベースを更新するための手順については、[コードおよびカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)のページを参照してください。

## アップグレード後のチェックおよびトラブルシューティングを実行 {#perform-post-upgrade-check-troubleshooting}

[アップグレード後のチェックおよびトラブルシューティング](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を参照してください。
