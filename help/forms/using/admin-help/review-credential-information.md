---
title: 資格情報の使用に関する情報を確認
description: 資格情報の使用に関する情報の確認方法について説明します。その使用法を説明する資格情報の使用に関する情報には、Acrobat Reader 拡張機能を介してアクセスできます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5cc5c9fe-50ce-4863-bfa4-a009a6c3b06f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 100%

---

# 資格情報の使用に関する情報の確認 {#review-credential-use-information}

資格情報には、Acrobat Reader DC Extensions のエンドユーザー web アプリケーションを通じてアクセスできる、その使用目的を説明する情報が含まれています。この情報を使用して、インストールされている資格情報のタイプ (評価または実稼動) とその有効期限を判断できます。

1. Web ブラウザーを開いて、次の URL を入力します。

   http://localhost:[port]/ReaderExtensions （*port* は、アプリケーションサーバーのポート番号です）

1. デフォルトのユーザー名とパスワードを使用してログインします。

   ユーザー名：管理者

   パスワード：password

   >[!NOTE]
   >
   >デフォルトのユーザー名とパスワードを使用してログインするには、管理者またはスーパーユーザーの権限が必要です。他のユーザーが Acrobat Reader DC Extensions にアクセスできるようにするには、ユーザー管理でユーザーアカウントを作成し、ユーザーに Acrobat Reader DC Extensions の web アプリケーションロールを付与します。

1. 「資格情報の選択」リストから資格情報のエイリアスを選択し、有効期限と使用目的の通知に含まれる情報を確認します。

>[!NOTE]
>
>資格情報の有効期限は、管理コンソールの設定／Trust Storeの管理／ローカル秘密鍵証明書ページの有効期限で確認することもできます。
