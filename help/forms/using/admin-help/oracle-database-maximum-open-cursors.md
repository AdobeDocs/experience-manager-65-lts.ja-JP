---
title: Oracle データベースの最大オープンカーソル数のしきい値
description: Oracle でオープンカーソルの最大値を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 98663f16-6c05-4485-9bf2-a2de9d1975c8
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 100%

---

# Oracle データベースの最大オープンカーソル数のしきい値 {#oracle-database-maximum-open-cursors-threshold}

Oracle でオープンカーソルの最大値を設定する場合、使用しているアプリケーションに適合するように数値を調整することが必要な場合があります。一般的な読み込みでは、平均的なオープンカーソル数は 2,700 なので、上限の指定を 3,000 から開始することをお勧めします。詳しくは、[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758) を参照してください。
