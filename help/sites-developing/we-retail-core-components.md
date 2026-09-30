---
title: We.Retailのコアコンポーネントを試す
description: We.Retailを使用してAdobe Experience Managerのコアコンポーネントを操作する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 62b6d299-f44e-4af3-b5e1-b0e92ca0598a
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 50%
---
# We.Retailのコアコンポーネントを試す{#trying-out-core-components-in-we-retail}

コアコンポーネントは、柔軟性の高い最新のコンポーネントです。拡張が容易で、プロジェクトに簡単に統合できます。 コアコンポーネントは、HTL、設定不要の使いやすさ、設定可能、バージョン管理、拡張性など、いくつかの重要な設計の原理に基づいて構築されています。 `We.Retail` サイトはコアコンポーネント上に構築されています。

## 体験版 {#trying-it-out}

1. `We.Retail`個のサンプルコンテンツでAdobe Experience Manager（AEM）を起動し、[ コンポーネントコンソール ](/help/sites-authoring/default-components-console.md)を開きます。

   **グローバルナビゲーション／ツール／コンポーネント**

1. コンポーネントコンソールでパネルを開くと、特定のコンポーネントグループをフィルタリングできます。 コアコンポーネントは次の場所にあります。

   * `.core-wcm`：標準コアコンポーネント
   * `.core-wcm-form`：フォーム送信コアコンポーネント

   `.core-wcm` を選択します。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. すべてのコアコンポーネントは、**v1**&#x200B;名を使用して、各コンポーネントの最初のバージョンを示します。 定期的なバージョンは、今後リリースされる予定です。AEMとバージョン互換性があり、簡単にアップグレードできるため、最新の機能を利用できます。
1. 「**Text (v1)**」をクリックします。

   コンポーネントの&#x200B;**リソースタイプ**&#x200B;が `/apps/core/wcm/components/text/v1/text` であることを確認します。 コアコンポーネントは `/apps/core/wcm/components` の下にあり、コンポーネントごとにバージョン管理されます。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 「**ドキュメント**」タブをクリックして、コンポーネントの開発者用ドキュメントを表示します。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. コンポーネントコンソールに戻ります。 グループ **`We.Retail`**&#x200B;のフィルターを実行し、**テキスト** コンポーネントを選択します。
1. **リソースタイプ**&#x200B;が `/apps/weretail` 下の想定したコンポーネントを指していることを確認します。ただし、**リソースのスーパータイプ**&#x200B;は元のコアコンポーネント `/apps/core/wcm/components/text/v1/text` を指しています。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 「**ライブ使用状況**」タブをクリックして、このコンポーネントが使用されているページを表示します。 最初の&#x200B;**ありがとう**&#x200B;ページをクリックしてページを編集します。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. ありがとうページで、テキストコンポーネントを選択し、コンポーネントの編集メニューで、継承をキャンセルアイコンをクリックします。

   [`We.Retail`にはグローバル化されたサイト構造](/help/sites-developing/we-retail-globalized-site-structure.md)があり、コンテンツは継承](/help/sites-administering/msm.md)と呼ばれるメカニズムを通じて主要言語サイトから[ ライブコピーにプッシュされます。 このため、ユーザーが手動でテキストを編集できるように、継承をキャンセルする必要があります。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 「**はい**」をクリックして、解約を確定します。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 継承をキャンセルしてテキストコンポーネントを選択すると、さらに多くのオプションを使用できるようになります。 「**編集**」をクリックします。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. テキストコンポーネントに使用できる編集オプションが表示されます。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. **ページ情報**&#x200B;メニューから「**テンプレートを編集**」を選択します。
1. ページのテンプレートエディターで、そのページの&#x200B;**レイアウトコンテナ**&#x200B;にあるテキストコンポーネントの&#x200B;**ポリシー**&#x200B;アイコンをクリックします。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. コアコンポーネントを使用すると、テンプレート作成者は、ページ作成者が使用できるプロパティを設定できます。 これらのプロパティには、許可されているペーストソース、書式設定オプション、使用可能な段落スタイルなどの機能が含まれます。

   このようなデザインダイアログボックスは、多くのコアコンポーネントで利用でき、テンプレートエディターと連動して動作します。 有効にした機能は、コンポーネントエディターを通じて作成者に提供されます。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 関連トピック {#further-information}

コアコンポーネントについて詳しくは、オーサリングガイド [ コアコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction)を参照して、機能の概要を確認してください。 技術的な概要については、ガイド [ コアコンポーネントの開発](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/overview)を参照してください。



コアコンポーネントについて詳しくは、オーサリングドキュメント [ コアコンポーネント ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction)でコアコンポーネント機能の概要を参照し、技術情報については開発者ドキュメント [ コアコンポーネントの開発](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/overview)を参照してください。

また、[編集可能なテンプレート ](/help/sites-developing/we-retail-editable-templates.md)を調査することもできます。 編集可能なテンプレートの詳細については、オーサリングドキュメント [ ページテンプレートの作成](/help/sites-authoring/templates.md)または開発者ドキュメント ページ [ テンプレート – 編集可能](/help/sites-developing/page-templates-editable.md)を参照してください。
