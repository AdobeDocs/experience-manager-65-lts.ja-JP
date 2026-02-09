---
title: アプリケーションサーバーのインストールのアップグレード手順（Tomcat）
description: Tomcat を使用してデプロイされたAEMのインスタンスをアップグレードする方法について説明します。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: b3c4e946a3f235fa0e3a0945f1ad692ee195e3ef
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 9%

---

# アプリケーションサーバーのインストールのアップグレード手順（Tomcat - インプレースアップグレード） {#upgrade-steps-for-application-server-installations-tomcat-inplace}

>[!NOTE]
>
>ここでは、Tomcat 上のAEM 6.5 LTS からAEM 6.5 LTS Servicepack へのアップグレード（インプレースアップグレード）手順の概要を説明します。 AEM 6.5 から 6.5 LTS へのアップグレードについては [ こちらを参照 ](/help/sites-deploying/app-server-upgrade-tomcat.md)。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。詳しくは [ アップグレード前のメンテナンスタスク ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) を参照してください。 また、システムが [AEM 6.5 LTS Servicepack の要件 ](/help/sites-deploying/technical-requirements.md) を満たしていることを確認し、[ アップグレード計画に関する考慮事項 ](/help/sites-deploying/upgrade-planning.md) を参照してください。


### 移行の前提条件 {#migration-prerequisites}

* **最低限必要な Java バージョン**:Tomcat サーバーにOracle® JRE 17/21 がインストールされていることを確認します。
* **Tomcat サーバー**:AEM 6.5 LTS 用 Tomcat サーバーとそのサービスパックのサポート対象バージョンは、**10.0.x** と **10.1.x** です。

### アップグレードの実行 {#performing-the-upgrade}

この手順のすべての例では、Tomcat をアプリケーションサーバーとして使用しており、AEM 6.5 LTS の作業用バージョンが既にデプロイされていることを示しています。 ここでは、AEM バージョン **6.5** LTS から **6.5 LTS** Servicepack へのアップグレードについて説明します。

1. AEM 6.5 LTS が既にデプロイされている場合は、*`https://<serveraddress:port>/system/console/bundles`* にアクセスしてバンドルが正常に動作していることを確認します。
1. 次に、AEM 6.5 LTS を停止します。 これは、次の場所にある Tomcat App Manager から実行できます。*`https://<serveraddress:port>/manager/html`*
1. アップグレードアクティビティを実行する前に、AEM 6.5 LTS サーバーのバックアップなどの [ アップグレード前 ](#pre-upgrade-steps) アクティビティが完了していることを確認してください
1. AEM 6.5 LTS Tomcat サーバーを停止します。 ほとんどの状況で、`./catalina.sh` スクリプトを実行することで設定できます。このために、ターミナルから次のコマンドを実行します。

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 不要なファイルとフォルダーを削除します。具体的に削除する必要のある項目は次のとおりです。

   * **cq-quickstart-65.war** ファイルと、通常 `cq-quickstart-65` に配置され `webapps` フォルダーの `<path-to-aem-server>/webapps` フォルダー
   * `launchpad/startup` フォルダー。 サーバーフォルダーにいると仮定して、ターミナルで次のコマンドを実行して削除できます。

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/startup
     ```

   * `base.jar` ファイル。 これを行うには、次のコマンドを実行します。

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt` ファイル：

     ```shell
     rm -f <path-to-aem-server>/bin/crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 次のコマンドを実行して `sling.options` ファイルを削除します。

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * `sling.bootstrap.txt` ファイルを削除します。

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. `sling.properties` ファイル（通常 `<path-to-aem-server>/bin/crx-quickstart/launchpad/` に存在）のバックアップを作成して削除します
1. AEM 6.5 LTS Servicepack war ファイルを `<path-to-aem-server>/webapps` フォルダーにコピーします。
1. 次のコマンドを実行して、AEM 6.5 LTS Tomcat サーバーを起動します。

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEMの起動中にエラーログを監視し、エラーがなく、AEMがスムーズに実行されていることを確認します
1. AEM 6.5 LTS が起動したら、*`https://<serveraddress:port>/cq/system/console/bundles`* にアクセスしてバンドルが正常に機能していることを確認します。

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-checks-and-troubleshooting}

詳しくは、[ アップグレード後のチェックとトラブルシューティング ](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md) を参照してください。
