---
title: 埋め込むフォントの指定
description: アダプティブフォームに埋め込むフォントの指定方法について説明します。 Forms サービスで生成されるフォームに埋め込むフォント、または埋め込まないフォントを指定できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 374f9425-b596-4481-8fd0-6df07c521a19
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
source-wordcount: '283'
ht-degree: 100%
---
# 埋め込むフォントの指定{#specify-fonts-to-embed}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Output で使用されるフォームに常に埋め込むフォント、または埋め込まないフォントを指定できます。 フォントを埋め込むと、フォームのファイルサイズが大きくなります。 ユーザーのシステムに通常存在しない珍しいフォントを埋め込みます。インストールされるような一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Output のカスタム XCI ファイルを指定している場合、XCI ファイルのフォント埋め込みオプションがこれらの設定より優先されます。 （[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「フォントの埋め込み設定」の「常に埋め込むフォント」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。 指定するフォントは、生成されたフォームで使用されている場合にのみそのフォームに埋め込まれます。 サービスに渡される XCI ファイルでフォントの埋め込みオプションが有効になっていると、この設定は無視されます。 その場合、PDF で使用されるすべてのフォントが常に埋め込まれます。
1. 「常に埋め込まないフォント」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。 指定するフォントは、生成された PDF で使用されていても、その PDF に埋め込まれません。 サービスに渡される XCI ファイルでフォントの埋め込みオプションが無効になっていると、この設定は無視されます。 その場合、PDF で使用されるフォントは一切埋め込まれません。
1. 「保存」をクリックします。
