---
title: 文字セットの変更
description: 出力ストリームをエンコードするための文字セットを指定できます。 文字セットの変更方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 1d614736-5897-4fd3-9ca4-94b115139ba3
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-wordcount: '144'
ht-degree: 100%
---
# 文字セットの変更 {#change-the-character-set}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

出力ストリームをエンコードするための文字セットを指定できます。

1. 管理コンソールで、**[!UICONTROL サービス／Output]** をクリックします。
1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。 この設定は、API 経由で指定する `TransformationFormat` と `PrintFormat` の値によって異なります。 リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   `TransformationFormat` が PDF か PDF/A である場合、または `PrintFormat` が PCL、PostScript、Zebra Label、IPL、DPL、TPCL、GenericColorPCL または GenericPSLevel3 である場合、特定の文字セットのみがサポートされます。

   文字セットは、有効な正規名で指定する必要があります。 デフォルト値は「ISO-8859-1」です。

1. 「**[!UICONTROL 保存]**」をクリックします。
