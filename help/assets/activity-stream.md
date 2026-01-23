---
title: タイムライン表示でのデジタルアセットのアクティビティストリーム
description: この記事では、アセットのアクティビティログをタイムラインに表示する方法について説明します。
contentOwner: AG
feature: Asset Management
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: 453331b3-41f7-4bf1-90fc-afeaf40577c8
source-git-commit: f27795b9acf834101d82937d9f9f142361816735
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 86%

---

# タイムラインのアクティビティストリーム {#activity-stream-in-timeline}

この機能は、タイムラインにアセットのアクティビティログを表示します。[!DNL Adobe Experience Manager Assets] で以下のアセット関連操作を実行すると、アクティビティストリーム機能により、タイムラインが更新され、そのアクティビティが反映されます。

アクティビティストリームでログに記録される操作は次のとおりです。

* 作成
* 削除
* ダウンロード（レンディションを含む）
* 公開
* 非公開
* 承認
* 非承認
* 移動

タイムラインに表示されるアクティビティログは、ログファイルが格納されている CRX の `/var/audit/com.day.cq.dam/content/dam` から取得されます。また、[!DNL Experience Manager]Experience Manager Asset Link または [Adobe デスクトップアプリケーション ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) により、新しいアセットがアップロードされたり、既存のアセットが変更されて [ にチェックインされたりすると ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja) タイムラインアクティビティがログに記録されます。

>[!NOTE]
>
>一時的なワークフローは、履歴情報が保存されないので、タイムラインに表示されません。

アクティビティストリームを表示するには、アセットに対して 1 つ以上の操作を実行して、アセットを選択してから、グローバルナビゲーションリストから&#x200B;**[!UICONTROL タイムライン]**&#x200B;を選択します。

![timeline-2](assets/timeline-2.png)

タイムラインに、アセットに対して実行した操作のアクティビティストリームが表示されます。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>「**[!UICONTROL 公開]**」および「**[!UICONTROL 非公開]**」タスクのデフォルトのログ保存場所は、`/var/audit/com.day.cq.replication/content` です。**[!UICONTROL 移動]**&#x200B;タスクの場合、デフォルトの場所は `/var/audit/com.day.cq.wcm.core.page` です。
