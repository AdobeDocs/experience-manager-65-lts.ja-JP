---
title: アプリケーションサーバーインストール（WLP）のアップグレード手順
description: Webspehere Liberty を介してデプロイされたAEMのインスタンスをアップグレードする方法について説明します。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: cd04a7a493a575cabf416b53869dd3fe4df7ab6b
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 17%

---

# アプリケーションサーバーインストール（WLP）のアップグレード手順 {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>ここでは、WLP （WebSphere® Liberty）上のAEM 6.5 LTS のアップグレード手順の概要を説明します。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。さらに、お使いのシステムが [AEM 6.5 LTS の要件 ](/help/sites-deploying/technical-requirements.md) を満たしていることを確認してください。

[ アップグレードの計画 ](/help/sites-deploying/upgrade-planning.md) や、[AEM Analyzer](/help/sites-deploying/pattern-detector.md) を使用してAEMのアップグレードの複雑さを見積もる方法を確認してください。

### 移行の前提条件 {#migration-prerequisites}

* **最低限必要な Java バージョン**:WLP サーバーにIBM® Sumeru JRE 17 がインストールされていることを確認します。

### アップグレードの実行 {#performing-the-upgrade}

1. アップグレードアクティビティを実行する前に、AEM 6.5 サーバーのバックアップなどの [ アップグレード前 ](#pre-upgrade-steps) 手順を完了していることを確認してください
1. 要件に応じて、次のいずれかのアップグレードパスを選択します。
   1. **インプレースアップグレード**：現在の WLP サーバーがサーブレット 6 をサポートしている場合は、インプレースアップグレードを実行して手順 3 を続行できます。
   1. **サイドグレード**：新しい設定を希望する場合、または WLP サーバーがサーブレット 6 をサポートしていない場合は、[AEM AEM 6.5 to AEM 6.5 LTS Content Migration Using Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md) ガイドに従って、新しい WLP インスタンスを設定し、コンテンツを移行します。[ アップグレードされたコードベースのデプロイ ](#deploy-upgraded-codebase) の節にスキップします

1. AEM インスタンスを停止します。通常は、次のコマンドを使用して実行できます。

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 不要なファイルとフォルダーを削除します。具体的に削除する必要のある項目は次のとおりです。

   * 通常、`dropins` フォルダーの **cq-quickstart-65.war** と `expanded` フォルダーはそれぞれ `<path-to-aem-server>/dropins/cq-quickstart-65.war` と `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war` にあります
   * `launchpad/startup` フォルダー。 サーバーフォルダーにいると仮定して、ターミナルで次のコマンドを実行して削除できます。

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar` ファイル。 これを行うには、次のコマンドを実行します。

     ```shell
     find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt` ファイル：

     ```shell
     rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 次のコマンドを実行して `sling.options` ファイルを削除します。

     ```shell
     find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * `sling.bootstrap.txt` ファイルを削除します。

     ```shell
     rm -rf crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. `sling.properties` ファイル（通常 `crx-quickstart/conf/` に存在）のバックアップを作成して削除します
1. `server.xml` ファイルで servlet のバージョンを **6.0** に変更します
1. Java 17 をインストールし、次を実行して正しくインストールされていることを確認します。

   ```shell
   java -version
   ```

1. AEM サーバーの開始パラメーターを確認し、必要に応じてパラメーターを更新してください。 詳しくは、[Java 17 に関する考慮事項 ](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations) を参照してください
1. 新しい 6.5 LTS war をダウンロードし、`/<path-to-aem-server>/dropins/` にある dropins フォルダーにコピーします。
1. AEM インスタンスを起動します。通常は、次のコマンドを使用して起動できます。

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. `sling.properties` にカスタムの変更がある場合は、次の手順に従ってください。

   1. `<path-to-wlp-directory>/bin/server stop server_name` を実行して、AEM インスタンスを停止します。
   1. 手順 5 で作成したバックアップファイルを参照して、カスタム `sling.properties` の変更を新しく生成された `sling.properties` ファイルに適用します。
   1. AEM インスタンスを起動します。 通常は、次を実行することで実行できます。`<path-to-wlp-directory>/bin/server start server_name`

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

アップグレードプロセスが完了したら、更新されたコードベースをデプロイする必要があります。 ターゲットバージョンの AEM で動作するようにコードベースを更新するための手順については、[コードおよびカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)のページを参照してください。

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-checks-and-troubleshooting}

[アップグレード後のチェックおよびトラブルシューティング](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を参照してください。
