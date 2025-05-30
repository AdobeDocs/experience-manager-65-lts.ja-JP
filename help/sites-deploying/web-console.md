---
title: Adobe Experience Manager の web コンソール
description: Adobe Experience Manager（AEM）の web コンソールを使用する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 55d4f34c-6766-48b7-86a1-689901e8871f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 100%

---

# Web コンソール{#web-console}

Adobe Experience Manager（AEM）の web コンソールは、[Apache Felix web 管理コンソール](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html)に基づいています。Apache Felix は、OSGi R4 サービスプラットフォームを実装するためのコミュニティによる取り組みです。このプラットフォームには、OSGi フレームワークと標準サービスが含まれています。

>[!NOTE]
>
>Web コンソールでは、デフォルト設定に言及している説明はすべて、Sling のデフォルトに関連しています。
>
>AEM には独自のデフォルトがあるので、設定されたデフォルトは、コンソールに記載された設定とは異なる場合があります。

Web コンソールには、OSGi バンドルを維持するために次のような一連のタブがあります。

* [設定](#configuration)：OSGi バンドルの設定に使用します。AEM システムパラメーターを設定するための基盤となるメカニズムです。
* [バンドル](#bundles)：バンドルのインストールに使用します。
* [コンポーネント](#components)：AEM に必要なコンポーネントのステータスを制御するために使用します。

行われた変更は、実行中のシステムにすぐに適用されます。再起動は不要です。

コンソールには `../system/console`からアクセスできます。次に例を示します。

`http://localhost:4502/system/console/components`

## 設定 {#configuration}

「**設定**」タブは、OSGi バンドルの設定に使用します。AEM システムパラメーターを設定するための基盤となるメカニズムです。

>[!NOTE]
>
>詳しくは、[Web コンソールでの OSGi 設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

「**設定**」タブにアクセスするには、次のいずれかを使用します。

* ドロップダウンメニュー：

  **OSGi >**

* URLは、例えば次のようになります。

  `http://localhost:4502/system/console/configMgr`

設定のリストは以下のように表示されます。

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

この画面のドロップダウンリストから、以下の 2 種類の設定を使用できます。

* **設定**
既存の設定を更新できます。これらは永続 ID（PID）を持ち、次のいずれかになります。

   * 標準かつ AEM に不可欠な設定。これらの設定は必須であり、削除すると値がデフォルト設定に戻ります。
   * ファクトリ設定から作成されたインスタンス。これらのインスタンスはユーザーによって作成され、削除するとインスタンスが削除されます。

* **ファクトリ設定**
必要な機能オブジェクトのインスタンスを作成できます。

  これは永続 ID に割り当てられており、設定ドロップダウンリストに表示されます。

リストからエントリを選択すると、その設定に関連するパラメーターが表示されます。

![chlimage_1-21](assets/chlimage_1-21a.png)

必要に応じて、パラメーターを更新し、次の処理をすることができます。

* **保存**&#x200B;します

  行われた変更を保存します。

  ファクトリ設定の場合は、永続 ID を持つインスタンスが作成されます。新規インスタンスが「設定」の下に表示されます。

* **リセット**

  画面に表示されているパラメーターを、最後に保存した値にリセットします。

* **削除**

  現在の設定を削除します。標準の場合は、パラメーターがデフォルト設定に戻ります。ファクトリ設定から作成した場合は、特定のインスタンスが削除されます。

* **バインド解除**

  現在の設定とバンドルとのバインドを解除します。

* **キャンセル**

  現在の変更をすべてキャンセルします。

## バンドル {#bundles}

「**Bundles**」タブは、AEM で必要な OSGi バンドルをインストールするためのメカニズムです。このタブにアクセスするには、次のいずれかの方法を使用します。

* ドロップダウンメニュー：

  **OSGi >**

* URLは、例えば次のようになります。

  `http://localhost:4502/system/console/bundles`

バンドルのリストは次のように表示されます。

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

このタブでは、次のことができます。

* **「Install」または「Update」**

  バンドルを格納するファイルを&#x200B;**参照**&#x200B;して特定し、すぐに&#x200B;**開始**&#x200B;するかどうか、および&#x200B;**開始レベル**&#x200B;を指定できます。

* **再読み込み**

  表示されているリストを更新します。

* **Refresh Packages**

  すべてのパッケージの参照を確認し、必要に応じて更新します。

  例えば、更新後に、以前の参照が原因で古いバージョンと新しいバージョンの両方が引き続き実行される場合があります。このオプションでは、すべての参照を確認して新しいバージョンに移動し、古いバージョンを停止できるようにします。

* **開始**

  指定した開始レベルに従ってバンドルを開始します。

* **停止**

   バンドルを停止します。

* **アンインストール**

  バンドルをシステムからアンインストールします。

* **ステータスの参照**

  リストでは、バンドルのステータスを指定します。特定のバンドルの名前をクリックすると、詳細な情報が表示されます。

>[!NOTE]
>
>**アップデート**&#x200B;後に、**パッケージの更新**&#x200B;を実行することをお勧めします。

## コンポーネント {#components}

「**コンポーネント**」タブを使用すると、様々なコンポーネントを有効または無効にできます。次のいずれかの方法でアクセスできます。

* ドロップダウンメニュー：

  **メイン >**

* URLは、例えば次のようになります。

  `http://localhost:4502/system/console/components`

コンポーネントのリストが表示されます。様々なアイコンを使用して、特定のコンポーネントを有効または無効にしたり、（必要に応じて）設定の詳細を開いたりすることができます。

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

特定のコンポーネントの名前をクリックして、そのステータスに関する詳細情報を表示します。ここでは、コンポーネントを有効または無効にしたり、再読み込みしたりすることもできます。

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>コンポーネントの有効化または無効化は、AEM／CRX を再起動するまで適用されます。
>
>開始状態はコンポーネントの記述子内で定義されます。この記述子は開発時に生成され、バンドルの作成時にバンドルに格納されます。
