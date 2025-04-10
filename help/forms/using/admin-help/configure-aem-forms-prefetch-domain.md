---
title: ドメイン情報をプリフェッチするための AEM Forms の設定
description: グループのネストが深いことによって応答時間が遅くなる場合や、多くのグループのメンバーである場合、ドメイン情報をプリフェッチするように AEM Forms を設定します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 61328a32-d014-4a90-b142-169f4f73b35f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 100%

---

# ドメイン情報をプリフェッチするための AEM Forms の設定 {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

ユーザーが多数のグループに属している場合（例：500 以上）や、グループのネストが深い場合（例：30 レベル）、応答時間が遅くなる可能性があります。この問題が発生している場合は、特定のドメインから情報をプリフェッチするように AEM Forms を設定できます。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／設定／既存の設定ファイルのインポートとエクスポート]**&#x200B;をクリックします。
1. ファイルに現在の設定をエクスポートするには、「**[!UICONTROL エクスポート]**」をクリックして別の場所に設定ファイルを保存します。
1. 次のノード（太字でマーク）を追加します。

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   この例では、複数のドメインがプリフェッチ用に設定されています。ドメイン名は「/」によって区切られます。このことは、上の例において *Domain_Name1*、*Domain_Name2* および *Domain_Name3* として示されています。

1. 更新したファイルをインポートするには、User Management で、「**[!UICONTROL 設定ファイルのインポートとエクスポート]**」をクリックします。
1. 「**[!UICONTROL 参照]**」をクリックしてファイルを探し、「インポート」をクリックして「**[!UICONTROL OK]**」をクリックします。
