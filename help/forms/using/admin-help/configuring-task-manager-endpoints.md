---
title: タスクマネージャーエンドポイントの設定
description: サービスを呼び出せるようにタスクマネージャーエンドポイントを設定する方法について説明します。タスクマネージャーエンドポイントを設定するには、様々な設定が必要です。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 57fd8b5d-6347-4b83-9489-e8ee59ee39a5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 100%

---

# タスクマネージャーエンドポイントの設定 {#configuring-task-manager-endpoints}

タスクマネージャーエンドポイントを使用すると、Workspace ユーザーがサービスを呼び出せるようになります。

**タスクマネージャーエンドポイントの設定**

タスクマネージャーエンドポイントを設定するには、次の設定を使用します。

**名前：**（必須）エンドポイントを識別します。名前は Workspace のカードビューで表示されます。&lt; は含めないでください。含めると、Workspace に表示される名前の一部が省略されます。エンドポイント名として URL を入力する場合は、RFC1738 で指定された構文規則に準拠していることを確認します。

**説明：** エンドポイントの説明。&lt; は含めないでください。含めると、Workspace に表示される説明の一部が省略されます。

**タスクの手順：**&#x200B;このワークフローを開始するユーザーに対する指示です。

**プロセスの所有者：**&#x200B;プロセスを所有する個人の名前です。

**ユーザーはタスクの転送が可能：**&#x200B;初期タスクの転送をユーザーに許可します。

**添付ファイルウィンドウを表示：**&#x200B;添付ファイルウィンドウの表示をユーザーに許可します。

**添付ファイルの追加を許可：**&#x200B;添付ファイルとメモの追加をユーザーに許可します。

**初期タスクをロック：**&#x200B;初期タスクをロックします。

**共有キュー用の ACL を追加：**&#x200B;共有キューユーザー用の ACL で初期タスクを作成します。

**分類：**（必須）Workspace でフォームが表示されるカテゴリです。リストからカテゴリを選択するか、「新規カテゴリ」を選択して、カテゴリを追加します。

**操作名：**（必須）エンドポイントに割り当てることができる操作のリストです。
