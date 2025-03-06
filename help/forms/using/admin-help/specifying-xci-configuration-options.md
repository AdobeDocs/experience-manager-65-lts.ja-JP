---
title: XCI 設定オプションの指定
description: XCI 設定オプションの指定方法について説明します。アダプティブフォームのカスタム XCI ファイル値を指定すると、フォームのレンダリング中に使用できるようになります。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 198016d7-0fb5-47e6-91ed-f2f0c98b2224
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 100%

---

# XCI 設定オプションの指定 {#specifying-xci-configuration-options}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Forms では、レンダリングに使用するカスタム XCI ファイルを指定できます（[Forms の場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)を参照）。デフォルトでは、次のような XCI ファイルで指定されている一部のオプションは、Forms によって上書きされます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

前述のオプションの上書きをキャンセルするオプションを選択できます。この場合、Forms では、カスタム XCI ファイルで指定されている値が使用されます。

1. 管理コンソールで、**サービス**／**Forms** をクリックします。
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。このオプションを選択すると、Forms では、パケット、作成者、プロデューサーおよび compressObjectStream の設定にデフォルト値が使用されます。このオプションを選択しない場合、Forms では、カスタム XCI ファイルで指定された値が使用されます。
1. 「**保存**」をクリックします。
