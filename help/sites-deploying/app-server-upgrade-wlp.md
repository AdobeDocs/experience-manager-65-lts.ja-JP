---
title: アプリケーションサーバーインストール（WLP）のアップグレード手順
description: Webspehere Liberty を介してデプロイされたAEMのインスタンスをアップグレードする方法について説明します。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 6a62741ee0ce22a6fb80cf8c68c6eeafacd2e873
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 15%

---

# アプリケーションサーバーインストール（WLP）のアップグレード手順 {#upgrade-steps-for-application-server-installations-wlp}

>[!NOTE]
>
>ここでは、WLP （WebSphere Liberty）でのAEM 6.5 LTS 戦争のアップグレード手順の概要を説明します。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。さらに、お使いのシステムがAEM 6.5 LTS の要件を満たしていることを確認してください。 アップグレードの複雑さを見積もるのに Analyzer がどのように役立つかを確認し、アップグレードのプランを作成するも参照してください（詳しくは [ アップグレードの計画 ](/help/sites-deploying/upgrade-planning.md) を参照）。

### 移行の前提条件 {#migration-prerequisites}

* **最低限必要な Java バージョン**:WLP サーバーにIBM Sumeru JRE 17 がインストールされていることを確認してください。

### アップグレードの実行 {#performing-the-upgrade}

1. アップグレードアクティビティを開始する前に、インスタンスのバックアップを実行します。
1. 使用している WLP サーバーのバージョンに応じて、インプレースアップグレードまたはサイドグレードが必要かどうかを特定します。 現在の WLP サーバーが Servlet 6 をサポートしている場合は、インプレースアップグレードを実行し、このドキュメントを続行できます。 そうでなければ、あなたはサイドグレードを実行する必要があります。 サイドグレードについては、Oakとのコンテンツの移行 – アップグレードのドキュメント - [ 未定のリンクを追加する予定 ] す。
1. AEM インスタンスを停止します。通常は、次のコマンドを使用して実行できます。

   ```shell
   <path-to-wlp-directory>/bin/server stop server_name
   ```

1. 不要なファイルとフォルダーを削除します。具体的に削除する必要のある項目は次のとおりです。

   * 通常、`dropins` フォルダーの `cq-quickstart-65.war` は `<path-to-aem-server>/dropins/cq-quickstart-65.war` に、展開フォルダーの URL は `<path-to-aem-server>/apps/expanded/cq-quickstart-65.war` に配置されます
   * `launchpad/startup` フォルダー。 サーバーフォルダーにいると仮定して、ターミナルで次のコマンドを実行して削除できます。

     ```shell
     rm -rf crx-quickstart/launchpad/startup
     ```

   * `base.jar` ファイル。 これを行うには、次のコマンドを実行します。

     ```shell
     find crx-quickstart/launchpad -type f -name 
     "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
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
1. AEM サーバーの開始パラメーターを確認し、必要なシステム構成に合わせてパラメーターを更新してください。 詳しくは、[ カスタムスタンドアロンインストール ](/help/sites-deploying/custom-standalone-install.md) を参照してください
1. Java 17 をインストールし、次を実行して正しくインストールされていることを確認します。

   ```shell
   java -version
   ```

1. ソフトウェア配布から新しい war 6.5 LTS をダウンロードし、`/<path-to-aem-server>/dropins/` にある dropins フォルダーにコピーします。
1. AEM インスタンスを起動します。通常は、次のコマンドを使用して起動できます。

   ```shell
   <path-to-wlp-directory>/bin/server start server_name
   ```

1. `sling.properties` にカスタムの変更がある場合は、次の手順に従ってください。

   1. `<path-to-wlp-directory>/bin/server stop server_name` を実行して、AEM インスタンスを停止します。
   1. （手順 6 で作成したバックアップファイルを参照して）新しく生成された `sling.properties` ファイルにカスタム `sling.properties` の変更を適用します
   1. AEM インスタンスを起動します。 通常は、次を実行することで実行できます。`<path-to-wlp-directory>/bin/server start server_name`

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

インプレースアップグレードプロセスが完了したら、更新したコードベースをデプロイする必要があります。ターゲットバージョンのAEMで動作するようにコードベースを更新するための手順については、「コードおよびカスタマイズのアップグレード [ ページを参照し ](/help/sites-deploying/upgrading-code-and-customizations.md) ください。

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-checks-and-troubleshooting}

詳しくは、[ アップグレード後のチェックとトラブルシューティング ](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md) を参照してください。