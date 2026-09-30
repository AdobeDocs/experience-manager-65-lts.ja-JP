---
title: Dynamic Mediaでのホットリンク保護の有効化
description: Dynamic Media でホットリンク保護を有効化する方法について説明します。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
feature: Configuration
solution: Experience Manager, Experience Manager Assets
exl-id: 56eb956e-c6a8-464b-980a-28e0dab0da7c
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 100%
---
# Dynamic Media でのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

ホットリンクは、サードパーティの Web サイトで HTML コードを使用して自社 Web サイト内の画像を表示する場合に行われます。 訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。 ホットリンク&#x200B;*保護*&#x200B;は、自社 web サイト上の画像、CSS、JavaScript などに他の web サイトが直接リンクできないようにするための方法です。 このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Experience Manager カスタマーサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&lang=ja#support)では、コンテンツ配信ネットワーク（CDN）レベルでリファラーフィルターを設定することができます。これにより、ドメインに許可された web サイトにのみ Dynamic Media コンテンツが提供されるようになります。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。 この機能では、その他のカスタム CDN はサポートされません。 ホットリンク保護を有効化するには、Dynamic Media アカウントの設定変更を要求する Adobe カスタマーサポートチケットを管理者が作成する必要があります。 ホットリンク保護を有効化するための追加費用は発生しません。
