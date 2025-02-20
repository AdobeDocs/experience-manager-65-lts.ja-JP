---
title: MySQL の 6.5.12.0 へのアップグレード中にデータベースのバックアップに失敗しました。
description: Experience Manager 6.5.12.0 にアップグレードして「Upgrade MySQL」をクリックすると、Configuration Manager で以前のExperience Manager Forms Database のバックアップに失敗します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 30%

---

# MySQL の 6.5.12.0 へのアップグレード中にデータベースのバックアップに失敗しました {#issue}

Experience Manager 6.5.12.0 にアップグレードして「Upgrade MySQL」をクリックすると、Configuration Manager で以前のExperience Manager Forms Database のバックアップに失敗し、次のエラーが表示されます。

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 適用先 {#applies-to}

* Experience Manager 6.5 Forms

## 解決策 {#solution}

この問題を解決するには、{AEM_HOME}/mysql にある my.ini ファイルで、データベースの max_packet_size を 100 M に、または必要に応じて増やします。
