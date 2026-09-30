---
title: Application Server インストールのアップグレード手順（Tomcat）
description: Tomcatを介してデプロイされたAEMのインスタンスをアップグレードする方法について説明します。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 7f8de16f-9e9a-4d37-9978-d26c496b911c
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
source-wordcount: '504'
ht-degree: 16%
---
# Application Server インストールのアップグレード手順（Tomcat - Sidegrade） {#upgrade-steps-for-application-server-installations-tomcat}

>[!NOTE]
>
>このページでは、Tomcat上のAEM 6.5からAEM 6.5 LTSへのアップグレード手順の概要を説明します。 AEM 6.5 LTSからAEM 6.5 LTS Servicepack [へのアップグレードについては、こちらを参照してください](/help/sites-deploying/app-server-upgrade-tomcat-inplace.md)

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。 詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。 さらに、お使いのシステムがAEM 6.5 LTS](/help/sites-deploying/technical-requirements.md)の[要件を満たしていることを確認し、[ アップグレード計画に関する考慮事項](/help/sites-deploying/upgrade-planning.md)と、[Analyzer](/help/sites-deploying/aem-analyzer.md)による複雑性の見積もり方法を参照してください。


### 移行の前提条件 {#migration-prerequisites}

* **必要なJava バージョン**&#x200B;の最小値：Tomcat サーバーにOracle® JRE 17/21がインストールされていることを確認してください。
* **Tomcat サーバー**: AEM 6.5 LTS用のTomcat サーバーでサポートされているバージョンは、**10.0.x**&#x200B;および&#x200B;**10.1.x**&#x200B;です。

### アップグレードの実行 {#performing-the-upgrade}

この手順では、どの例でも JBoss をアプリケーションサーバーとして使用し、有効な AEM のバージョンが既にデプロイされているものとします。 この手順は、AEM バージョン **6.5**&#x200B;から&#x200B;**6.5 LTS**&#x200B;に実行されたアップグレードを文書化するためのものです。

1. AEM 6.5が既にデプロイされている場合は、バンドルが正しく機能していることを確認します。*`https://<serveraddress:port>/system/console/bundles`*
1. 次に、AEM 6.5を停止します。 これは、次の場所にあるTomcat App Managerから実行できます：*`https://<serveraddress:port>/manager/html`*
1. アップグレード アクティビティを実行する前に、AEM 6.5 サーバーのバックアップなどの[ アップグレード前](#pre-upgrade-steps) アクティビティが完了していることを確認してください
1. Java 17/Java 21をインストールし、コマンドを実行して正しくインストールされていることを確認します。

   ```
   java –version
   ```

1. AEM 6.5 LTS互換Tomcat サーバーのセットアップ
1. AEM サーバーの開始パラメーターを確認し、必要システム構成に応じてパラメーターを更新してください。 詳しくは、[Java 17/Java 21の考慮事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)を参照してください
1. Java 17/Java 21を使用して、新しくダウンロードした6.5 LTS warをTomcat サーバーにデプロイし、次のコマンドを実行してAEM 6.5 LTS Tomcat サーバーを起動します。

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEMを起動して実行したら、すべてのバンドルが実行状態であることを確認します。*`https://<serveraddress:port>/cq/system/console/bundles`*
1. AEM 6.5 LTS Tomcat サーバーを停止します。 ほとんどの場合、ターミナルから次のコマンドを実行して、`./catalina.sh` スクリプトを実行することで、これを行うことができます。

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 次の手順に従って、AEM 6.5からAEM 6.5 LTSにコンテンツを移行します。[AEM 6.5からAEM 6.5 LTSへのコンテンツの移行Oak – アップグレードを使用](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)
1. コンテンツを移行したら、`sling.properties` ファイルに必要なカスタム変更を適用します
1. 次のコマンドを実行して、AEM 6.5 LTS Tomcat サーバーを起動します。

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEMの起動時にエラーログを監視して、エラーがないことを確認し、AEMがスムーズに動作していることを確認します
1. AEM 6.5 LTSが開始されたら、バンドルが正しく機能していることを確認します。*`https://<serveraddress:port>/cq/system/console/bundles`*

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

アップグレードプロセスが完了したら、更新されたコードベースをデプロイする必要があります。 ターゲットバージョンの AEM で動作するようにコードベースを更新するための手順については、[コードおよびカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)のページを参照してください。

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-checks-and-troubleshooting}

詳しくは、[ アップグレード後の確認とトラブルシューティング ](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を参照してください。
