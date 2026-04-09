---
title: AEM の AI アシスタントの設定
description: Adobe Experience ManagerのAdmin Consoleを使用して、AI アシスタントを設定および設定する方法について説明します。
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin,Developer,User
exl-id: e653d37f-5802-4b0f-a71b-539b33ad5ca5
source-git-commit: e3106e87f72484568667873c1772abd30a108e51
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 4%

---

# AEM の AI アシスタントの設定 {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

AEM（Adobe Experience Manager）でAI アシスタントを使用するには、AI アシスタントを通じて製品情報にアクセスする権限が必要です。 この権限はデフォルトでオンになっています。

製品情報にアクセスできるユーザーを制御するには、Adobe IDに関連付けられている電子メールアドレスから[aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com)に電子メールを送信します。 Adobeでは、ユーザーレベルのアクセス制御を有効にできます。 有効にすると、管理者は次の手順に従ってユーザーレベルのアクセス権を付与できます。

ユーザーレベルのアクセス制御を要求した場合、組織はAdobe Admin Consoleを介してオプトインする必要があります。 製品管理者がユーザーグループを作成（または選択）し、新しい「AI アシスタント」権限を付与します。 グループに追加すれば、誰でもすぐにAEMのAI アシスタントにアクセスできます。 目標が全社的な可用性である場合、管理者は単にそのグループにすべてのユーザーを割り当てます。

従業員の観点からは、このプロセスは簡単です。組織内のAdobe Experience Managerのプロダクト管理者を特定し、AI対応ユーザーグループに追加することをリクエストします。 そのグループに表示されると、次回のログイン時にアシスタントアイコンが自動的に表示されます。

管理者は、通常のCloud Manager ガバナンスを念頭に置く必要があります。 Admin Consoleの製品管理者権限を保持して、プロファイルの作成、ユーザーグループの管理、権限の編集を行うことができます。 ユーザーがアシスタントの組み込み&#x200B;**サポートチケットの作成**&#x200B;機能も必要な場合は、標準の&#x200B;**サポート管理者** ロール（標準のAdmin Console ロール）を同じ個人またはグループに追加します。

AEMのAI アシスタントの設定プロセスは、次の手順で構成されます。

1. [Adobe Admin Console](#create-profile)で新しい商品プロファイルを作成します。
1. [AI アシスタント製品ナレッジ権限を有効にする](#enable-permission)。
1. [新しいユーザーグループを作成する（または既存のユーザーグループを使用する） &#x200B;](#create-user-group)。
1. [&#x200B; ユーザーグループにユーザーを追加](#add-users)。
1. [製品プロファイルをユーザーグループ &#x200B;](#assign-product-profile)に割り当てます。

**前提条件**

開始する前に、次の前提条件を満たしていることを確認してください。

* Adobe Admin Consoleでは、少なくともプロダクト管理者権限が必要です。
* 組織のユーザー管理構造を理解している。

**設定に関する考慮事項**

* 処理時間：Cloud Managerで作成されたリソースは、権限設定のためにAdmin Consoleに表示するのに最大2分かかる場合があります。
* 複数のプロファイル：ユーザーは複数のプロファイルに属することができ、割り当てられたすべてのプロファイルから権限が組み合わされます。
* 組織スコープ：一部の権限は、すべてのプログラムに対して組織レベルで適用される場合があります。
* 定義済みプロファイル：定義済み権限プロファイルをAdmin Consoleから削除しないでください。


## 1 - Adobe Admin Consoleで新しい商品プロファイルを作成する{#create-profile}

1. Experience Platform ドキュメントにあるAdobe Admin Console[で、](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile)Create a new product profileの詳細な手順に従います。

1. 新しい製品プロファイルを作成する際に、AI アシスタントに次の推奨値を使用できます。

   | テキストフィールド | 推奨値 |
   | --- | --- |
   | 製品プロファイル名 | `AI Assistant in AEM` （または任意の記述名） |
   | 表示名（オプション） | `AI Assistant` |
   | 説明（オプション） | `Product profile for managing AI Assistant in AEM access` |
   | 通知 | 組織のプリファレンスに基づく設定 |


## 2 - AI アシスタント製品知識の権限を有効にする{#enable-permission}

製品プロファイルにカスタム権限を割り当てるプロセスは、標準のAdobe Cloud Manager カスタム権限ワークフローに従います。

参照記事：[新しい製品プロファイルへのカスタム権限の割り当て](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Admin Consoleで、新しく作成した製品プロファイルの名前（`AI Assistant in AEM`）をクリックします

   ![スクリーンショット](/help/assets/assets-ai/ai-assistant-console.png)

1. 編集可能な権限のリストを表示するには、「**権限**」タブをクリックします。

1. テーブル リストで、`AI Assistant Product Knowledge`権限を見つけます。

   Admin Consoleの「![AI アシスタント権限」タブ &#x200B;](/help/assets/assets-ai/ai-assistant-permission.png)

1. 権限名の右側にある![鉛筆アイコンまたは編集アイコン &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)をクリックします。

1. **AI アシスタントの権限の編集** ページで、**AI アシスタント製品ナレッジ**&#x200B;の切り替えをオンにします。

   ![AI アシスタント製品知識の権限ページの編集の切り替えオプション &#x200B;](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. ページの右下隅にある「**保存**」をクリックします。

   製品プロファイルで、AI アシスタント製品知識の権限が有効になりました。


## 3 – 新しいユーザーグループを作成（または既存のユーザーグループを使用）{#create-user-group}

1. 次のいずれかの操作を行います。

>[!BEGINTABS]

>[!TAB 新しいユーザーグループを作成]

1. Admin Consoleで、**Users** > **User groups**&#x200B;をクリックします。

   ![ユーザーグループ](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. **ユーザーグループ** ページで、**新規ユーザーグループ**&#x200B;をクリックします。

   ![&#x200B; ユーザーグループ ページの「新しいユーザーグループ」ボタン &#x200B;](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. **新しいユーザーグループを作成** ページで、次の情報を入力します。

   | オプション | 推奨値 |
   | --- | --- |
   | ユーザーグループ名 | `AI Assistant in AEM` （または任意の名前） |
   | 説明（オプション） | `User group for managing AI Assistant in AEM access` |

   ![新しいユーザーグループページを作成](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. ページの右下隅にある「**保存**」をクリックします。

>[!TAB 既存のユーザーグループを使用]

新しいグループを作成する代わりに、AI アシスタントのアクセス要件を満たす既存のAEM ユーザーグループを使用できます。

>[!ENDTABS]

## 4 - ユーザーグループにユーザーを追加する{#add-users}

1. 次のいずれかの操作を行います。

>[!BEGINTABS]

>[!TAB 個々のユーザーを追加]

1. **ユーザーグループ** ページの&#x200B;**グループ名** テーブルで、新しく作成したユーザーグループ名または既存のユーザーグループ名をクリックします。

   ![&#x200B; テーブルのAEM ユーザーグループ名にAI アシスタントが表示されているユーザーグループページ &#x200B;](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. AEM **の** AI アシスタントの&#x200B;**ユーザーグループ** ページで、「**ユーザー**」タブをクリックし、「**ユーザーを追加**」をクリックします。

   AEM ユーザーグループ ページの![AI アシスタント。ユーザーのタブと「ユーザーを追加」ボタンが表示されている](/help/assets/assets-ai/ai-assistant-add-users.png)

1. **`Add users to this user group`** ページで、AEMのAI アシスタントにアクセスする必要があるユーザーを検索して選択します。

   ![このユーザーグループ ページにユーザーを追加](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. ページの右下隅にある「**保存**」をクリックします。
1. 次に、[製品プロファイルをユーザーグループに割り当てます](#assign-product-profile)。

>[!TAB ユーザーの一括追加]

Admin Consoleのバルクアップロード機能を使用できます。

1. ユーザー情報を含むCSV ファイルを準備します。
1. 効率的な一括追加には、**`Add users by CSV`** オプションを使用します。
1. 次に、[製品プロファイルをユーザーグループに割り当てます](#assign-product-profile)。

>[!ENDTABS]


## 5 – 製品プロファイルをユーザーグループに割り当てる{#assign-product-profile}

この手順は、製品プロファイルをユーザーグループに割り当てるための標準のAdobe Admin Console ワークフローに従います。

参照記事：[&#x200B; エンタープライズユーザー向け製品プロファイルの管理](https://helpx.adobe.com/jp/enterprise/using/manage-product-profiles.html)

1. [4からAEM ユーザーグループのAI アシスタントを引き続き使用している間に、「](#add-users)割り当て済み製品プロファイル **」タブをクリックします。**
1. 「**プロファイルを割り当て**」をクリックします。

   「割り当てられた製品プロファイル」タブが選択されたAEM ユーザーグループページの![AI アシスタント &#x200B;](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. **製品とプロファイルの割り当て** ページで、**製品プロファイルの選択** ダイアログボックスで、**AI アシスタント**&#x200B;製品プロファイルを検索して選択します。

   ![製品とプロファイルの割り当てページ。製品プロファイルの選択ダイアログボックスと「AI アシスタント」製品プロファイルが選択されている](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. ダイアログボックスの右下隅付近にある「**適用**」をクリックします。
1. **製品とプロファイルの割り当て** ページの右下隅付近にある「**保存**」をクリックします。

   AEM ユーザーグループでAI アシスタントに割り当てられた![AI アシスタント製品プロファイルが表示されています](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## 設定の確認

* 製品プロファイルに、割り当てられたユーザーグループの正しい数が表示されていることを確認します。
* ユーザーグループに正しいユーザー数が表示されていることを確認します。
* AI アシスタント製品知識の権限が有効で、適切に設定されていることを確認します。


## 設定のテスト

割り当てられたグループのユーザーに次の操作を実行してもらいます。

1. AEM にログインします。
2. AI アシスタント機能にアクセスできることを確認します。
3. AI アシスタントの機能をテストして、適切に活用する。

## 関連トピック

* [AEM の AI アシスタント](/help/ai-assistant-in-aem.md)
* [Adobe Experience Platform アクセス制御](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
