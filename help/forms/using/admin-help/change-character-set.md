---
title: 文字セットの変更
description: 出力ストリームをエンコードするための文字セットを指定できます。文字セットの変更方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 100%

---

# 文字セットの変更 {#change-the-character-set}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

出力ストリームをエンコードするための文字セットを指定できます。

1. 管理コンソールで、**[!UICONTROL サービス／Output]** をクリックします。
1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。この設定は、API 経由で指定する `TransformationFormat` と `PrintFormat` の値によって異なります。リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   `TransformationFormat` が PDF か PDF/A である場合、または `PrintFormat` が PCL、PostScript、Zebra Label、IPL、DPL、TPCL、GenericColorPCL または GenericPSLevel3 である場合、特定の文字セットのみがサポートされます。

   文字セットは、有効な正規名で指定する必要があります。デフォルト値は「ISO-8859-1」です。

1. 「**[!UICONTROL 保存]**」をクリックします。
