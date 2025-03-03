---
title: アプリケーションサーバーのインストールのアップグレード手順（Tomcat）
description: Tomcat を使用してデプロイされたAEMのインスタンスをアップグレードする方法について説明します。
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 8798c608ea168d753be2a08b25a0d0d344b0fef6
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 15%

---

# アプリケーションサーバーのインストールのアップグレード手順（Tomcat） {#upgrade-steps-for-application-server-installations-tomcat}

>[!NOTE]
>
>ここでは、Tomcat でのAEM 6.5 LTS war のアップグレード手順の概要を説明します。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。さらに、お使いのシステムがAEM 6.5 LTS の要件を満たしていることを確認してください。 アップグレードの複雑さを見積もるのに Analyzer がどのように役立つかを確認し、アップグレードのプランを作成するも参照してください（詳しくは [ アップグレードの計画 ](/help/sites-deploying/upgrade-planning.md) を参照）。

### 移行の前提条件 {#migration-prerequisites}

* **最低限必要な Java バージョン**:Tomcat サーバーにIBM Sumeru JRE 17 がインストールされていることを確認します。
* **Tomcat サーバー**: 6.5 LTS に必要な Tomcat サーバーのバージョンは **11.0.x** です。

### アップグレードの実行 {#performing-the-upgrade}

この手順では、どの例でも JBoss をアプリケーションサーバーとして使用し、有効な AEM のバージョンが既にデプロイされているものとします。ここでは、AEM バージョン **6.5** から **6.5 LTS** へのアップグレードについて説明します。

1. AEM 6.5 が既にデプロイされている場合は、*`https://<serveraddress:port>/cq/system/console/bundles`* にアクセスしてバンドルが正常に動作していることを確認します。
1. 次に、AEM 6.5 を停止します。これは、次の場所にある Tomcat App Manager から実行できます。*`https://<serveraddress:port>/manager/html`*
1. アップグレードアクティビティを実行する前に、AEM 6.5 サーバーのバックアップなどの [ アップグレード前 ](#pre-upgrade-steps) アクティビティが完了していることを確認してください
1. Java 17 をインストールし、次のコマンドを実行して正しくインストールされていることを確認します。

   ```
   java –version
   ```

1. AEM 6.5 LTS 互換の Tomcat サーバーの設定
1. AEM サーバーの開始パラメーターを確認し、システム要件に従ってパラメーターを更新してください。 詳しくは、[ カスタムスタンドアロンインストール ](/help/sites-deploying/custom-standalone-install.md) を参照してください
1. Java 17 を使用して、新しくダウンロードした 6.5 LTS war を Tomcat サーバーにデプロイし、次のコマンドを実行してAEM 6.5 LTS Tomcat サーバーを起動します。

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEMを起動して実行したら、次の場所にアクセスして、すべてのバンドルが実行状態であることを確認します。*`https://<serveraddress:port>/cq/system/console/bundles*`
1. 次に、AEM 6.5 LTS Tomcat サーバーを停止します。 ほとんどの状況で、`./catalina.sh` スクリプトを実行することで設定できます。このために、ターミナルから次のコマンドを実行します。

   ```
   $CATALINA_HOME/bin/catalina.sh stop
   ```

1. 次に、このチュートリアルを使用して、AEM 6.5 からAEM 6.5 LTS にコンテンツを移行します。[AEM 6.5 からAEM 6.5 LTS へのコンテンツの移行Oak-upgrade を使用する ](/help/sites-deploying/aem-65-to-aem-65lts-content-migration-using-oak-upgrade.md)
1. コンテンツが移行されたら、`sling.properties` ファイルに必要なカスタム変更を適用します
1. 次のコマンドを実行して、AEM 6.5 LTS Tomcat サーバーを起動します。

   ```
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEMの起動中にエラーログを監視し、エラーがなく、AEMがスムーズに実行されていることを確認します
1. AEM 6.5 LTS が起動したら、*`https://<serveraddress:port>/cq/system/console/bundles`* にアクセスしてバンドルが正常に機能していることを確認します。

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

インプレースアップグレードプロセスが完了したら、更新したコードベースをデプロイする必要があります。ターゲットバージョンのAEMで動作するようにコードベースを更新するための手順については、「コードおよびカスタマイズのアップグレード [ ページを参照し ](/help/sites-deploying/upgrading-code-and-customizations.md) ください。

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-checks-and-troubleshooting}

詳しくは、[ アップグレード後のチェックとトラブルシューティング ](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md) を参照してください。