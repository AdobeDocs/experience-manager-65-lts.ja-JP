---
title: OSGi でのAEM 6.5 Forms LTS へのアップグレード
description: AEM 6.5.22.0 FormsからAEM 6.5 Forms LTS に直接アップグレードすることができます。
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 81%

---

# OSGi でのAEM 6.5 Forms LTS へのアップグレード {#upgrade-to-aem-forms-osgi}

[AEM 6.5 からAEM 6.5 LTS へのアップグレード ](/help/sites-deploying/upgrade.md) を行うには、AEM 6.5.22.0 Forms以降にアップグレードします。 AEM 6.5.22.0 からAEM 6.5 Forms LTS への直接アップグレードがサポートされています。

AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms、AEM 6.3 Forms、AEM 6.4 FormsまたはAEM 6.5 Formsを使用している場合、AEM 6.5 Forms LTS に直接アップグレードすることはできません。 アップグレードパスについて詳しくは、「[ アップグレードパス ](/help/forms/using/upgrade.md) ドキュメントを参照してください。

サービスパック AEM Forms 6.5.22.0 にアップグレードした後、次の手順に従ってAEM 6.5 LTS Formsにアップグレードします。

1. AEM Forms アドオンパッケージのインストール. 手順は次のとおりです。

   1. [ソフトウェア配布](https://experience.adobe.com/jp/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
   1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」を選択します。
   1. 「**[!UICONTROL フィルター]**」セクションで、
      1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
      1. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
   1. お使いのオペレーティングシステムに適した Forms アドオンパッケージの名前を選択し、「**[!UICONTROL EULA 利用条件に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」を選択します。
   1. [パッケージマネージャー](/help/sites-administering/package-manager.md)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
   1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
   1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

      「[AEM Forms リリース](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)」記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

      パッケージのインストールが完了したら、AEM インスタンスを再起動します。**その際、すぐにサーバーを停止しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが &lt;crx-repository>/error.log ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ちます。また、いくつかのパッケージについては、インストールされたままの状態になる場合があります。これらのパッケージの状態は無視しても問題ありません。


      **次の追加の JVM コマンドラインパラメーターを使用してAEM インスタンスを再起動します**。
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      サーバーがスクリプトまたはサービスを使用して起動された場合は、上記の内容を含めるようにサーバーを適切に更新し、その後の再起動後も有効になるようにします。

1. AEM インスタンスを再起動します。

   >[!NOTE]
   >
   > 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

1. インストール後のアクティビティを実行します。

   * **移行ユーティリティを実行**

     移行ユーティリティにより、以前のバージョンのアダプティブフォームや対応する管理アセットが AEM 6.5 Forms で使用できるようになります。このユーティリティは、AEM ソフトウェア配布からダウンロードできます。 移行ユーティリティの詳しい設定方法と使用方法については、[移行ユーティリティ](../../forms/using/migration-utility.md)に関する説明を参照してください。

     [ドラフト統合とコンポーネント送信のサンプル](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)をデータベースで使用して旧バージョンのアップグレードを行う場合は、アップグレードの実行後に、以下の SQL クエリを実行してください。

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **Adobe Sign の再設定（AEM 6.2 Forms 以前のバージョンをアップグレードする場合のみ）**

     Adobe Sign を以前のバージョンの AEM Forms で設定してある場合は、AEM Cloud サービスから Adobe Sign を再設定します。詳しくは、[Adobe Sign と AEM Forms の統合](../../forms/using/adobe-sign-integration-adaptive-forms.md)を参照してください。

   * **jQuery のサポート**

     AEM 6.5 Forms では、jQuery のバージョンが 3.2.1 に、jQuery UI のバージョンが1.12.1に更新されます。AEM Form は、**noConflict** モードの JQuery を使用します。そのため、他の jQuery バージョンを使用している場合、アップグレードの実行中に問題は表示されません。 ただし、AEM 6.5 Forms にアップグレードする場合は、次の手順を実行します。

      * カスタムコンポーネントが（存在する場合）、サポートされる jQuery バージョンと互換性があることを確認します。
      * サポートされていない API をカスタムコンポーネントから削除します。 削除された API のリストについては、[アップグレードガイド](https://jquery.com/upgrade-guide/3.0/)を参照してください。 例えば、load()、.unload()、.error() の各 API のサポートは削除されています。 前述の API の代わりに.on() メソッドを使用します。 例えば、$(&quot;img&quot;).load(fn) を $(&quot;img&quot;).on(&quot;load&quot;, fn) に変更します。

   * **分析機能とレポートの再設定（バージョン 6.2 以前の AEM Forms をアップグレードする場合のみ）** 

     AEM 6.4 Forms では、ソースのトラフィック変数とインプレッションの成功イベントは使用できません。そのため、バージョン 6.2 以前の AEM Forms をアップグレードすると、AEM Forms から Adobe Analytics サーバーにデータが送信されなくなり、アダプティブフォームの分析レポートが使用できなくなります。さらに、AEM 6.4 Forms では、フォーム分析のバージョンのトラフィック変数と、フィールドでの滞在時間の成功イベントが導入されています。そのため、AEM Forms 環境で分析とレポートを再設定します。詳しい手順については、[分析とレポートの設定](../../forms/using/configure-analytics-forms-documents.md)を参照してください。

1. サーバーのアップグレードが成功し、すべてのデータが正常に移行され、問題なく動作することを確認してください。

   * **バンドルのステータスを確認：**&#x200B;すべてのバンドルがアクティブ状態になっていることを確認します。
   * **レプリケーションとリバースレプリケーションの検証：**&#x200B;移行されたフォームをいくつか公開、入力および送信します。送信されたデータも検証します。
   * **管理者および開発者のユーザーインターフェイスへのアクセスを確認：**&#x200B;管理者アカウントで AEM インスタンスにログインし、次の URL にアクセスできることを確認します。

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >AEM 6.4 Forms では crx-repository の構造が変更されています。6.3 Forms から AEM 6.5 Forms にアップグレードした場合、新規作成するカスタマイズについては、変更後のパスを使用してください。変更後のパスの一覧については、「[AEM Forms におけるリポジトリの再構築](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)」を参照してください。
