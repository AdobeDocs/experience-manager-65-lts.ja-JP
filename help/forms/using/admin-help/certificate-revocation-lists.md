---
title: 証明書失効リストの管理
description: 証明書失効リストの管理方法について説明します。Trust Store の管理を使用して、証明書失効リスト（CRL）の読み込み、編集および削除を行うことができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: a5e49cc8-cd46-47e6-8ff3-655dcf23296a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 100%

---

# 証明書失効リストの管理{#managing-certificate-revocationlists}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Trust Store の管理では、証明書失効リスト（CRL）の読み込み、編集および削除を行うことができます。Base64 および DER でエンコードされた証明書失効リストがサポートされます。

## CRL を読み込み {#import-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックして、「読み込み」をクリックします。
1. 「エイリアス」ボックスに、CRL の ID を入力します。
1. 「参照」をクリックして CRL を見つけ、「OK」をクリックします。

## CRL を書き出し {#export-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックします。
1. 書き出す CRL のエイリアス名をクリックし、「書き出し」をクリックします。
1. 指示に従って CRL を書き出します。CRL は Base64 エンコードで書き出されます。
1. 「OK」をクリックします。

## CRL を削除 {#delete-a-crl}

1. 管理コンソールで、設定／Trust Store の管理／証明書の失効リストをクリックします。
1. 削除する CRL のチェックボックスをオンにして「削除」をクリックし、「OK」をクリックします。
