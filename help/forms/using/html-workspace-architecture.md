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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 53%
---
# AEM Forms workspace architecture {#aem-forms-workspace-architecture}

AEM Forms Workspace は、CRX™ にホスティングされている web アプリケーションです。 ブラウザーでワークスペースを開くと、CRX リソースにアクセスし、アプリケーションがブラウザー内のHTML ページとしてレンダリングされます。

アプリケーションは、REST エンドポイント上のAEM Forms Serverにアクセスして、次の操作を行います。

* ユーザーのタスク、プロセススタートポイント、プロセス履歴、およびユーザー情報の取得
* タスクに対するアクションの実行
* データベースでのクエリタスク
* ユーザーの環境設定の更新など

AEM Forms Serverは、JDBC経由でAEM Forms データベースにアクセスします。 データベースは、タスク、プロセスとそのインスタンス、ユーザー、および関連情報を維持します。

AEM Forms Workspaceは、JavaScriptのモジュラーコンポーネントとして設計されており、個別にカスタマイズしたり、他のweb アプリケーションで再利用したりできます。 コンポーネントは、Web アプリケーションに構造を与えるJavaScript ライブラリであるBackBoneに基づいています。 コンポーネントとBackBoneの相互作用について詳しく説明する記事は、[こちら](/help/forms/using/backbone-interaction.md)です。 CRX フォルダー構造のコンポーネントの組織については、[この記事](/help/forms/using/folder-structure.md)で説明しています。

AEM Forms Workspace のために配信されるパッケージを以下に示しています。

* `adobe-lc-workspace-pkg-<version>.zip`：これは CRX パッケージです。すなわち、パッケージマネージャーを使用して CRX 内にデプロイできます。
* `adobe-lc-workspace-<version>-src.zip`：デプロイパッケージ（Ship、Debug、および Dev パッケージ）を作成するための AEM Forms Workspace とスクリプトの完全なコードを含むアーカイブです。
