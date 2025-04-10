---
title: XCI 設定オプションの指定
description: XCI 設定オプションの指定方法について説明します。アダプティブフォームのカスタム XCI ファイル値を指定すると、フォームのレンダリング中に使用できるようになります。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5fb6e6cc-6af7-4cf5-804b-bb3030079383
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 100%

---

# XCI 設定オプションの指定 {#specify-xci-configuration-options}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Output では、レンダリングに使用するカスタム XCI ファイルを指定できます（[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。

デフォルトでは、Output が、以下をはじめとする XCI ファイルで指定されている一部のオプションより優先されます。

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

前述のオプションの上書きをキャンセルするオプションを選択できます。この場合、Output では、カスタム XCI ファイルで指定されている値が使用されます。

1. 管理コンソールで、**サービス**／Output をクリックします。
1. 「システムデフォルトの XCI オプションを使用」チェックボックスをオンまたはオフにします。このオプションを選択すると、Output では、パケット、作成者、プロデューサーおよび compressObjectStream の設定にデフォルト値が使用されます。このオプションを選択しない場合、Output では、カスタム XCI ファイルで指定された値が使用されます。
1. 「**保存**」をクリックします。
