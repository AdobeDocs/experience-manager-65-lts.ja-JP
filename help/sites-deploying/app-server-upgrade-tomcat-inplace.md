---
title: Application Server インストールのアップグレード手順（Tomcat）
description: Tomcatを介してデプロイされたAEMのインスタンスをアップグレードする方法について説明します。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: a9f7494e-4a09-4999-9164-c369e0989886
source-git-commit: 60809c26ba9591bf9e30a19e25d71ceb449a162e
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 9%
---
# Application Server インストールのアップグレード手順（Tomcat - インプレースアップグレード） {#upgrade-steps-for-application-server-installations-tomcat-inplace}

>[!NOTE]
>
>このページでは、Tomcat上のAEM 6.5 LTSからAEM 6.5 LTS Servicepackへのアップグレード手順（インプレースアップグレード）の概要を説明します。 AEM 6.5から6.5 LTSへのアップグレードについては、[こちらを参照してください](/help/sites-deploying/app-server-upgrade-tomcat.md)。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。 詳しくは、[ アップグレード前のメンテナンスタスク ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。 さらに、お使いのシステムがAEM 6.5 LTS Servicepack](/help/sites-deploying/technical-requirements.md)の[要件を満たしていることを確認し、[ アップグレード計画に関する考慮事項](/help/sites-deploying/upgrade-planning.md)を参照してください。


### 移行の前提条件 {#migration-prerequisites}

* **必要なJava バージョン**&#x200B;の最小値：Tomcat サーバーにOracle® JRE 17/21がインストールされていることを確認してください。
* **Tomcat サーバー**: AEM 6.5 LTSとそのServicePackでサポートされているTomcat サーバーのバージョンは、**10.0.x**&#x200B;および&#x200B;**10.1.x**&#x200B;です。

### アップグレードの実行 {#performing-the-upgrade}

この手順のすべての例では、アプリケーションサーバーとしてTomcatを使用し、AEM 6.5 LTSの動作版が既にデプロイされていることを意味します。 この手順は、AEM バージョン **6.5** LTSから&#x200B;**6.5 LTS** Servicepackに実行されたアップグレードを文書化するためのものです。

1. AEM 6.5 LTSが既にデプロイされている場合は、バンドルが正しく機能していることを確認します。*`https://<serveraddress:port>/system/console/bundles`*
1. 次に、AEM 6.5 LTSを停止します。 これは、次の場所にあるTomcat App Managerから実行できます：*`https://<serveraddress:port>/manager/html`*
1. アップグレード アクティビティを実行する前に、AEM 6.5 LTS サーバーのバックアップなどの[ アップグレード前](#pre-upgrade-steps) アクティビティが完了していることを確認してください
1. AEM 6.5 LTS Tomcat サーバーを停止します。 ほとんどの場合、ターミナルから次のコマンドを実行して、`./catalina.sh` スクリプトを実行することで、これを行うことができます。

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 不要なファイルとフォルダーを削除します。 具体的に削除する必要のある項目は次のとおりです。

   * **cq-quickstart-65.war** ファイルと`webapps` フォルダーの`cq-quickstart-65` フォルダーは、通常`<path-to-aem-server>/webapps`にあります
   * `launchpad/startup` フォルダー。 サーバーフォルダーにいると仮定して、ターミナルで次のコマンドを実行することで削除できます。

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/startup
     ```

   * `base.jar` ファイル。 これには、次のコマンドを実行します。

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \;
     ```

   * `BootstrapCommandFile_timestamp.txt` ファイル：

     ```shell
     rm -f <path-to-aem-server>/bin/crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt
     ```

   * 次を実行して、`sling.options` ファイルを削除します。

     ```shell
     find <path-to-aem-server>/bin/crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \; 
     ```

   * `sling.bootstrap.txt` ファイルを削除します。

     ```shell
     rm -rf <path-to-aem-server>/bin/crx-quickstart/launchpad/sling_bootstrap.txt
     ```

1. `sling.properties` ファイル （通常は`<path-to-aem-server>/bin/crx-quickstart/launchpad/`に存在）のバックアップを作成して削除します
1. AEM 6.5 LTS Servicepack war ファイルを`<path-to-aem-server>/webapps` フォルダーにコピーします
1. 次のコマンドを実行して、AEM 6.5 LTS Tomcat サーバーを起動します。

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEMの起動時にエラーログを監視して、エラーがないことを確認し、AEMがスムーズに動作していることを確認します
1. AEM 6.5 LTSが開始されたら、バンドルが正しく機能していることを確認します。*`https://<serveraddress:port>/cq/system/console/bundles`*

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-checks-and-troubleshooting}

詳しくは、[ アップグレード後の確認とトラブルシューティング ](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を参照してください。
