---
title: 埋め込むフォントの指定
description: アダプティブフォームに埋め込むフォントの指定方法について説明します。Forms サービスで生成されるフォームに埋め込むフォント、または埋め込まないフォントを指定できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c73dced8-7242-465c-85bc-9315a9a08605
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 100%

---

# 埋め込むフォントの指定 {#specifying-fonts-to-embed}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Forms サービスで生成されるフォームに常に埋め込むフォント、または埋め込まないフォントを指定できます。フォントを埋め込むと、フォームのファイルサイズが大きくなります。ユーザーのシステムに通常存在しない珍しいフォントを埋め込みます。通常インストールされているような一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Forms のカスタム XCI ファイルを指定している場合、これらの設定より、XCI ファイルのフォントの埋め込みオプションが優先されます（[Forms の場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)を参照）。

1. 管理コンソールで、**[!UICONTROL サービス／Forms]** をクリックします。
1. 「**[!UICONTROL フォントの埋め込み設定]**」の「**[!UICONTROL 常に埋め込むフォント]**」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。指定するフォントは、生成されたフォームで使用されている場合にのみそのフォームに埋め込まれます。サービスに渡される XCI ファイルでフォントの埋め込みオプションが有効になっていると、この設定は無視されます。この場合は、PDF で使用されるすべてのフォントが常に埋め込まれるためです。
1. 「**[!UICONTROL 常に埋め込まないフォント]**」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。指定するフォントは、生成された PDF で使用されていても、その PDF に埋め込まれません。サービスに渡される XCI ファイルでフォントの埋め込みオプションが無効になっている場合、PDF で使用されるフォントが一切埋め込まれないため、この設定は無視されます。
1. 「**[!UICONTROL 保存]**」をクリックします。
