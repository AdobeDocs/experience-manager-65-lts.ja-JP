---
title: アプリケーションサーバーのインストール（WLP）のアップグレード手順
description: Webspehere Libertyを介してデプロイされたAEMのインスタンスをアップグレードする方法について説明します。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 2a5d9026-49bc-4766-bcbe-38d834c14f72
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
source-wordcount: '511'
ht-degree: 18%
---
# アプリケーションサーバーのインストール（WLP）のアップグレード手順 {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>このページでは、WLP （WebSphere® Liberty）上のAEM 6.5 LTSのアップグレード手順の概要を説明します。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。 詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。 さらに、お使いのシステムがAEM 6.5 LTS](/help/sites-deploying/technical-requirements.md)の[要件を満たしていることを確認してください。

[ アップグレードの計画](/help/sites-deploying/upgrade-planning.md)と、[AEM Analyzer](/help/sites-deploying/aem-analyzer.md)がAEMのアップグレードに関する複雑さを見積もるのに役立つことを確認してください。

### 移行の前提条件 {#migration-prerequisites}

* **必要なJava バージョン**&#x200B;の最小値：WLP サーバーにIBM® Sumeru JRE 17/21がインストールされていることを確認してください。

### アップグレードの実行 {#performing-the-upgrade}

1. アップグレード アクティビティを実行する前に、AEM 6.5 サーバーのバックアップなど、[ アップグレード前](#pre-upgrade-steps)の手順を完了していることを確認してください
1. 要件に応じて、次のいずれかのアップグレードパスを選択します。
   1. **インプレースアップグレード**：現在のWLP サーバーがServlet 6をサポートしている場合、インプレースアップグレードを実行して手順3に進むことができます。
   1. **Sidegrade**：新しいセットアップを希望する場合、またはWLP サーバーがServlet 6をサポートしていない場合は、[AEM 6.5からAEM 6.5 LTSへのコンテンツ移行Oak-upgrade](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md) ガイドに従って新しいWLP インスタンスを設定し、[ アップグレードされたCodebase](#deploy-upgraded-codebase) セクションにスキップしてコンテンツを移行します

1. AEM インスタンスを停止します。 これは通常、次のコマンドを使用して実行できます。

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 不要なファイルとフォルダーを削除します。 具体的に削除する必要のある項目は次のとおりです。

   * `dropins` フォルダーの&#x200B;**cq-quickstart-65.war**&#x200B;と、通常はそれぞれ`<path-to-aem-server>/dropins/cq-quickstart-65.war`と`<path-to-aem-server>/apps/expanded/cq-quickstart-65.war`にある`expanded` フォルダー
   * `launchpad/startup` フォルダー。 サーバーフォルダーにいると仮定して、ターミナルで次のコマンドを実行することで削除できます。

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar` ファイル。 これには、次のコマンドを実行します。

     ```shell
     find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt` ファイル：

     ```shell
     rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 次を実行して、`sling.options` ファイルを削除します。

     ```shell
     find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * `sling.bootstrap.txt` ファイルを削除します。

     ```shell
     rm -rf crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. `sling.properties` ファイル （通常は`crx-quickstart/conf/`に存在）のバックアップを作成して削除します
1. サーブレットのバージョンを`server.xml` ファイルの&#x200B;**6.0**&#x200B;に変更します
1. Java 17/Java 21をインストールし、次のコマンドを実行して正しくインストールされていることを確認します。

   ```shell
   java -version
   ```

1. AEM サーバーの開始パラメーターを確認し、要件に応じてパラメーターを更新してください。 詳しくは、[Java 17/Java 21の考慮事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)を参照してください。
1. 新しい6.5 LTS戦争をダウンロードし、次の場所にあるDropins フォルダーにコピーします：`/<path-to-aem-server>/dropins/`
1. AEM インスタンスを起動する：通常、次のコマンドを使用して実行できます。

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. `sling.properties`にカスタム変更がある場合は、次の手順に従ってください。

   1. `<path-to-wlp-directory>/bin/server stop server_name`を実行してAEM インスタンスを停止します
   1. カスタム `sling.properties`の変更を、新しく生成された`sling.properties` ファイルに適用します（手順5で作成したバックアップファイルを参照します）
   1. AEM インスタンスを起動します。 通常は、次を実行して実行できます：`<path-to-wlp-directory>/bin/server start server_name`

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

アップグレードプロセスが完了したら、更新されたコードベースをデプロイする必要があります。 ターゲットバージョンの AEM で動作するようにコードベースを更新するための手順については、[コードおよびカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)のページを参照してください。

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-checks-and-troubleshooting}

[アップグレード後のチェックおよびトラブルシューティング](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を参照してください。
