---
title: 多言語のアセット
description: バイナリ、メタデータ、タグなどのアセットを複数の言語に翻訳するワークフローを自動化する方法を学習します。
contentOwner: AG
feature: Asset Management
role: Admin
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 512bd351-2e6b-47a2-85c6-a23ea2c7102f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 100%

---

# 多言語のアセット {#multilingual-assets}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=ja) |
| AEM 6.5 | この記事 |

[!DNL Adobe Experience Manager Assets] を使用して、アセット（バイナリ、メタデータ、タグを含む）に対する翻訳ワークフローを自動化し、多言語プロジェクトで使用するために他の言語のアセットを生成できます。

翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと [!DNL Experience Manager] とを統合して、アセットを複数の言語に翻訳するためのプロジェクトを作成してください。[!DNL Experience Manager] では人間による翻訳と機械翻訳のワークフローがサポートされます。

人間翻訳：翻訳済みアセットが返されて、[!DNL Experience Manager] にインポートされます。翻訳プロバイダーと [!DNL Experience Manager] を連携すると、[!DNL Experience Manager] と翻訳プロバイダーとの間でアセットが自動的に送信されます。

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には次の手順が含まれます。

1. [Experience Manager と翻訳サービスプロバイダーの接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳するアセットの準備](preparing-assets-for-translation.md)
1. [フォルダーへの翻訳クラウドサービスの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

翻訳サービスプロバイダーによって[!DNL Experience Manager]と統合するためのコネクタが提供されない場合は、[別の方法](/help/sites-administering/tc-manage.md#exporting-a-translation-job)を使用してください。

[コンテンツフラグメントの翻訳プロジェクトの作成](creating-translation-projects-for-content-fragments.md)も参照してください。
