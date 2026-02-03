---
title: AEM Forms Workspace のアーキテクチャ
description: LiveCycle AEM Forms workspace の概要と概念情報です。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
exl-id: d317274f-2c9a-4809-b43e-2efebc8fcb3f
source-git-commit: 5995dda0aac101e6c0d506ac5bba786674b0735b
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 53%

---

# AEM Forms workspace のアーキテクチャ {#aem-forms-workspace-architecture}

AEM Forms Workspace は、CRX™ にホスティングされている web アプリケーションです。ブラウザーでワークスペースを開くと、CRX リソースがアクセスされ、アプリケーションはHTML ページとしてブラウザーにレンダリングされます。

REST エンドポイント上のAEM Forms サーバーにアクセスして、次の操作を実行します。

* ユーザーのタスク、プロセススタートポイント、プロセス履歴、およびユーザー情報の取得
* タスクに対するアクションの実行
* データベースでのクエリタスク
* ユーザーの環境設定の更新など

AEM Forms サーバーは、JDBC を使用してAEM Forms データベースにアクセスします。 データベースは、タスク、プロセスとそのインスタンス、ユーザー、および関連情報を維持します。

AEM Forms Workspace は、モジュール型のJavaScript コンポーネントで構成されており、これらのコンポーネントは他の web アプリケーションで個別にカスタマイズしたり再利用したりできます。 コンポーネントは、web アプリケーションに構造を提供するJavaScript ライブラリである BackBone に基づいています。 コンポーネントと BackBone の相互作用を説明する詳細な記事は [ こちら ](/help/forms/using/backbone-interaction.md) です。 CRX フォルダー構造のコンポーネントの組織については、[この記事](/help/forms/using/folder-structure.md)で説明しています。

AEM Forms Workspace のために配信されるパッケージを以下に示しています。

* `adobe-lc-workspace-pkg-<version>.zip`：これは CRX パッケージです。すなわち、パッケージマネージャーを使用して CRX 内にデプロイできます。
* `adobe-lc-workspace-<version>-src.zip`：デプロイパッケージ（Ship、Debug、および Dev パッケージ）を作成するための AEM Forms Workspace とスクリプトの完全なコードを含むアーカイブです。
