---
title: 'プロジェクトワークフローの操作 '
description: すぐに使用できる様々なプロジェクトワークフローが用意されています。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Architect,Developer
exl-id: eb19a269-8b3f-476b-b22b-8116dce70388
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 100%

---

# プロジェクトワークフローの操作  {#working-with-project-workflows}

すぐに使用可能なプロジェクトワークフローには、次のものがあります。

* **プロジェクト承認ワークフロー** - ユーザーへのコンテンツの割り当て、レビューおよび承認を行うことができます。
* **ローンチをリクエスト** - ローンチをリクエストするワークフローです。
* **ランディングページをリクエスト** - ランディングページをリクエストするワークフローです。
* **メールをリクエスト** - メールをリクエストするワークフローです。
* **撮影した製品写真および撮影した製品写真（コマース）** - アセットを製品にマップします。
* **DAM 言語コピー作成／翻訳および DAM 言語コピーを作成** - アセットおよびフォルダー用に翻訳されたバイナリ、メタデータ、タグを作成します。

選択するプロジェクトテンプレートに応じて、次の特定のワークフローを使用できます。

|   | **シンプルなプロジェクト** | **メディアプロジェクト** | **製品撮影プロジェクト** | **翻訳プロジェクト** |
|---|:-:|:-:|:-:|:-:|
| コピーをリクエスト |  | x |  |  |
| 撮影した製品写真 |  | x | x |  |
| 撮影した製品写真（コマース） |  |  | x |  |
| プロジェクト承認 | x |  |  |  |
| ローンチをリクエスト | x |  |  |  |
| ランディングページをリクエスト | x |  |  |  |
| メールをリクエスト | x |  |  |  |
| DAM 言語コピーを作成&amp;ast; |  |  |  | x |
| DAM 言語コピー作成／翻訳&amp;ast; |  |  |  | x |

>[!NOTE]
>
>&amp;ast; これらのワークフローは、プロジェクトの&#x200B;**ワークフロー**&#x200B;タイルからは開始できません。[アセットの言語コピーの作成](/help/sites-administering/tc-manage.md)を参照してください。

ワークフローを開始および完了する手順は、どのワークフローを選択した場合でも同じです。手順が異なるだけです。

ワークフローは、プロジェクト内で直接開始します（「DAM 言語コピーを作成」または「DAM 言語コピー作成／翻訳」を除く）。プロジェクト内の未処理のタスクに関する情報は、**タスク**&#x200B;タイルに表示されます。完了する必要があるタスクに関する通知は、ユーザーアイコンの横に表示されます。

AEM でのワークフローの操作について詳しくは、次のドキュメントを参照してください。

* [ワークフローへの参加 ](/help/sites-authoring/workflows-participating.md)
* [ページへのワークフローの適用 ](/help/sites-authoring/workflows-applying.md)
* [ワークフローの設定](/help/sites-administering/workflows.md)

この節では、プロジェクトに使用可能なワークフローについて説明します。

## コピーをリクエストワークフロー {#request-copy-workflow}

このワークフローでは、ユーザーに原稿をリクエストし、承認することができます。コピーをリクエストのワークフローを開始するには：

1. メディアプロジェクトで、**ワークフロー**&#x200B;タイルの右上にある下向きの山形をクリックし、「**ワークフローを開始**」を選択します。
1. ワークフローウィザードで、「**コピーをリクエスト**」を選択し、「**次へ**」をクリックします。
1. 原稿のタイトルと、リクエストするものの簡単な概要を入力します。必要に応じて、ターゲットの単語数、タスクの優先度および期限を入力します。

   ![コピーをリクエストワークフロー](assets/project-request-copy-workflow.png)

1. 「**送信**」をクリックします。

ワークフローが開始されます。タスクが&#x200B;**タスク**&#x200B;カードに表示されます。

## 撮影した製品写真ワークフロー {#product-photo-shoot-workflow}

**撮影した製品写真**&#x200B;ワークフロー（コマースありとコマースなしの両方）については、[クリエイティブプロジェクト](/help/sites-authoring/managing-product-information.md)ドキュメントで詳しく説明します

## プロジェクト承認ワークフロー {#project-approval-workflow}

**プロジェクト承認**&#x200B;ワークフローでは、コンテンツをユーザーに割り当て、レビューし、コンテンツを承認します。

1. シンプルなプロジェクトで、**ワークフロー**&#x200B;タイルの右上にある下向きの山形をクリックし、「**ワークフローを開始**」を選択します。
1. ワークフローウィザードで、「**プロジェクト承認ワークフロー**」を選択し、「**次へ**」をクリックします。
1. タイトルを入力し、割り当て先を選択します。必要に応じて、説明、コンテンツのパス、タスクの優先度および期限を入力します。

   ![プロジェクト承認ワークフロー](assets/project-approval-workflow.png)

1. 「**送信**」をクリックします。

ワークフローが開始されます。タスクが&#x200B;**タスク**&#x200B;カードに表示されます。

## 「ローンチをリクエスト」ワークフロー {#request-launch-workflow}

このワークフローでは、ローンチをリクエストできます。

1. シンプルなプロジェクトで、**ワークフロー**&#x200B;タイルの右上にある下向きの山形をクリックし、「**ワークフローを開始**」を選択します。
1. ワークフローウィザードで、「**ローンチをリクエストワークフロー**」を選択し、「**次へ**」をクリックします。
1. ローンチのタイトルを入力し、ローンチのソースパスを指定します。必要に応じて、説明とライブ日付も追加できます。希望するローンチの動作に応じて「ソースページのライブデータを継承」または「サブページを除外」を選択します。

   ![ローンチをリクエストワークフロー](assets/project-request-launch-workflow.png)

1. 「**送信**」をクリックします。

ワークフローが開始されます。ワークフローが&#x200B;**ワークフロー**&#x200B;リストに表示されます。

## ランディングページをリクエストワークフロー {#request-landing-page-workflow}

このワークフローでは、ランディングページをリクエストできます。

1. シンプルなプロジェクトで、**ワークフロー**&#x200B;タイルの右上にある下向きの山形をクリックし、「**ワークフローを開始**」を選択します。
1. ワークフローウィザードで、「**ランディングページをリクエスト**」を選択し、「**次へ**」をクリックします。
1. ランディングページのタイトルと親パスを入力します。必要に応じて、ライブ日付を入力するか、ランディングページのファイルを選択します。

   ![ランディングページをリクエストワークフロー](assets/project-request-landing-page-workflow.png)

1. 「**送信**」をクリックします。

ワークフローが開始されます。タスクが&#x200B;**タスク**&#x200B;カードに表示されます。

## メールをリクエストワークフロー {#request-email-workflow}

このワークフローでは、メールをリクエストできます。これは、**メール**&#x200B;タイルに表示されるワークフローと同じです。

1. シンプルなプロジェクトで、**ワークフロー**&#x200B;タイルの右上にある下向きの山形をクリックし、「**ワークフローを開始**」を選択します。
1. ワークフローウィザードで、「**メールをリクエスト**」を選択し、「**次へ**」をクリックします。
1. メールタイトルと、キャンペーンパスおよびテンプレートパスを入力します。さらに、名前、説明、ライブ日付を指定できます。

   ![メールをリクエストワークフロー](assets/project-request-email-workflow.png)

1. 「**送信**」をクリックします。

ワークフローが開始されます。タスクが&#x200B;**タスク**&#x200B;カードに表示されます。

## Assets の言語コピーを作成（および翻訳）するワークフロー {#create-and-translate-language-copy-workflow-for-assets}

**言語コピーを作成**&#x200B;ワークフローおよび&#x200B;**言語コピー作成／翻訳**&#x200B;ワークフローについて詳しくは、[アセットの言語コピーの作成](/help/assets/translation-projects.md)ドキュメントを参照してください。
