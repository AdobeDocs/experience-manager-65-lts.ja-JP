---
title: OSGi 上の AEM Forms のグループと権限
description: ユーザーをグループに割り当てて OSGi 上の Adobe Experience Manager（AEM）Forms を管理
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 1681e92b-2d88-4b10-a700-a516aa5a02c8
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 92%

---

# OSGi 上の AEM Forms のグループと権限{#aem-forms-on-osgi-groups-and-privileges}

## 適用先 {#applies-to}

このドキュメントは、**AEM 6.5 LTS Forms** に適用されます。

AEM as a Cloud Serviceのドキュメントについては、[Cloud ServiceのAEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html?lang=ja) を参照してください。

Adobe Experience Manager（AEM）では、[グループを作成](/help/sites-administering/user-group-ac-admin.md#group-administration)して、そのグループにポリシーと[ユーザー](/help/sites-administering/user-group-ac-admin.md#user-administration)を割り当てることができます。これらのポリシーは、グループに含まれるユーザーの権限を制御します。

[AEM Forms アドオンパッケージ](../../forms/using/installing-configuring-aem-forms-osgi.md)をインストールすると、この記事に記載されている forms-user や forms-power-user などのグループが、自動的に割り当て可能になります。次の表に、ユーザーが OSGi 上の AEM Forms でグループの割り当てに基づいて実行できるタスクを示します。

<table>
 <tbody>
  <tr>
   <td>グループ</td> 
   <td>タスク</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームを作成、プレビュー、公開、送信</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、公開</li> 
     <li>AEM インスタンスにアセットをアップロード</li> 
     <li>テーマを作成</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>アダプティブフォームを作成、プレビュー、公開、送信</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、公開</li> 
     <li>コードエディターを使用してアダプティブフォームのスクリプトを作成</li> 
     <li>スクリプトを含むアセットをアップロード</li> 
     <li>テーマを作成</li> 
     <li>XDP を含むパッケージを読み込み</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>送信されたフォームをレビュー</li> 
     <li>送信されたフォームを承認または拒否</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームやインタラクティブ通信テンプレートを作成およびプレビューする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>フォームデータモデルを作成および変更</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>エージェント UI を使用して Correspondence Management レターまたはインタラクティブ通信にアクセス</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>インボックスアプリケーションを作成</li> 
     <li>ワークフローモデルを作成</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>AEM インボックスアプリケーションを使用<br /> <strong>メモ：</strong>AEM インボックスのインタラクティブ通信エージェント UI にアクセスするには、cm-agent-users グループと workflow-users グループに割り当てられている必要があります。</li> 
     <li>ワークフローインスタンスを管理</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>PDF Generator を設定</li> 
     <li>監視フォルダーを設定</li> 
     <li>ワークフローアプリケーションを管理する</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. forms-user グループ権限を持つユーザーは、アダプティブフォームのスクリプトを書くことができません。
1. template-authors グループ権限を持つユーザーは、テンプレートのスクリプトを書くことができません。
