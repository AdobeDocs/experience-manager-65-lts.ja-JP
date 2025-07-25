---
title: Adobe Experience Manager のトラブルシューティング
description: Adobe Experience Manager で発生する可能性のあるいくつかのイシューのトラブルシューティングについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 802130c3-9cb8-46b7-98c2-fd9e83d18ec3
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 97%

---

# Adobe Experience Manager のトラブルシューティング {#troubleshooting-aem}

次の節では、AEM（Adobe Experience Manager）の使用時に発生する可能性のあるいくつかの問題を取り上げます。それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>AEM でのオーサリングの問題をトラブルシューティングする場合は、[オーサリング時の AEM のトラブルシューティング](/help/sites-authoring/troubleshooting.md)を参照してください。

>[!NOTE]
>
>問題が発生した場合は、そのインスタンス（リリースおよびサービスパック）の[既知の問題](/help/release-notes/release-notes.md)の一覧を確認すると役に立ちます。

## 管理者向けのトラブルシューティングシナリオ {#troubleshooting-scenarios-for-administrators}

次の表は、管理者がトラブルシューティングできる問題の概要を示します。

<table>
 <tbody>
  <tr>
   <td><strong>役割</strong></td>
   <td><strong>問題 </strong></td>
  </tr>
  <tr>
   <td>システム管理者</td>
   <td><p>クイックスタート jar をダブルクリックしても何も起こらないか、jar ファイルを別のプログラム（アーカイブマネージャーなど）で開かれる</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> </td>
   <td><p>CRX で実行中のアプリケーションでメモリ不足エラーが発生する</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> </td>
   <td><p>AEM CM Quickstart をダブルクリックした後、ブラウザーに AEM ようこそ画面が表示されない</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> <p>管理ユーザー</p> </td>
   <td><p>スレッドダンプの作成</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> <p>管理ユーザー</p> </td>
   <td><p>閉じられていない JCR セッションの確認</p> </td>
  </tr>
 </tbody>
</table>


## トラブルシューティング分析の方法 {#methods-for-troubleshooting-analysis}

### スレッドダンプの作成 {#making-a-thread-dump}

スレッドダンプは、現在アクティブなすべての Java™ スレッドのリストです。AEM が適切に応答しない場合は、デッドロックまたはその他の問題をスレッドダンプで特定できます。

### Sling スレッドダンパーの使用 {#using-sling-thread-dumper}

1. **AEM web コンソール**&#x200B;を開きます（例：`https://localhost:4502/system/console/`）。
1. **ステータス**&#x200B;タブの下の&#x200B;**スレッド**&#x200B;を選択します。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### jstack の使用（コマンドライン） {#using-jstack-command-line}

1. AEM Java™ インスタンスの PID（プロセス ID）を確認します。

   例えば、`ps -ef` や `jps` を使用できます。

1. 実行:

   `jstack <pid>`

1. スレッドダンプを表示します。

>[!NOTE]
>
>`>>` 出力リダイレクトを使用すると、ログファイルにスレッドダンプを追加できます。
>
>`jstack <pid> >> /path/to/logfile.log`

詳しくは、[JVM からのスレッドダンプの取得方法](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=ja)を参照してください。

### 閉じられていない JCR セッションの確認 {#checking-for-unclosed-jcr-sessions}

AEM WCM 用の機能を開発する場合は、JCR セッションが開かれる可能性があります（データベース接続を開く処理に相当します）。開いたセッションが閉じられないと、システムに次の現象が発生する可能性があります。

* システムの速度が低下します。
* 多数の CacheManager を確認できます（ログファイル内の resizeAll エントリ）。次の数値（size=&lt;x>）はキャッシュ数を示しており、各セッションが複数のキャッシュを開きます。
* システムのメモリが不足することがあります（重大度に応じて数時間後、数日後、数週間後に発生）。

閉じられていないセッションの分析を開始するには、ナレッジベースの記事 [ 閉じられていないリソースリゾルバー ](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23761) を参照してください。

### Adobe Experience Manager web コンソールの使用 {#using-the-adobe-experience-manager-web-console}

発生する可能性のある問題の初期の兆候を OSGi バンドルのステータスで確認することもできます。

1. **AEM web コンソール**&#x200B;を（`https://localhost:4502/system/console/` などで）開きます。
1. **OSGI** タブの下の&#x200B;**バンドル**&#x200B;を選択します。
1. チェック項目:

   * バンドルのステータス。「非アクティブ」または「未解決」と表示されているバンドルがある場合は、そのバンドルを停止してから再起動してください。問題が解決しない場合は、その他のメソッドを使用してさらに調査します。
   * 依存関係がないバンドルがあるかどうか。個々のバンドル名（リンク）をクリックすると、詳細を確認できます（次の例では問題が発生していません）。

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
