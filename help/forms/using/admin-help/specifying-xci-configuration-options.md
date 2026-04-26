---
title: XCI 設定オプションの指定
description: XCI 設定オプションの指定方法について説明します。 アダプティブフォームのカスタム XCI ファイル値を指定すると、フォームのレンダリング中に使用できるようになります。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 198016d7-0fb5-47e6-91ed-f2f0c98b2224
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 90%

---

# XCI 設定オプションの指定 {#specifying-xci-configuration-options}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Forms では、レンダリングに使用するカスタム XCI ファイルを指定できます （[Forms の場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)を参照）。 デフォルトでは、FormsはXCI ファイルで指定されたオプションの一部を上書きします。これには次のものが含まれます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

前述のオプションの上書きをキャンセルするオプションを選択できます。この場合、Forms では、カスタム XCI ファイルで指定されている値が使用されます。

1. 管理コンソールで、**サービス**／**Forms** をクリックします。
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。 このオプションを選択すると、Forms では、パケット、作成者、プロデューサーおよび compressObjectStream の設定にデフォルト値が使用されます。 このオプションを選択しない場合、Forms では、カスタム XCI ファイルで指定された値が使用されます。
1. 「**保存**」をクリックします。
