---
title: 権限管理のプリンシパルビュー
description: 権限管理を容易にする新しいタッチ UI インターフェイスについて説明します。
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: 7f952e69-f219-4ade-a187-2a4cbc1600f3
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 100%

---

# 権限管理のプリンシパルビュー{#principal-view-for-permissions-management}

## 概要 {#overview}

AEM 6.5 では、ユーザーとグループに対する権限管理が導入されました。主な機能は従来の UI と同じですが、よりユーザーフレンドリーで効率的です。

## 使用方法 {#how-to-use}

### UI へのアクセス {#accessing-the-ui}

次に示すように、新しい UI ベースの権限管理は、セキュリティの下の権限カードからアクセスします。

![権限管理 UI](assets/screen_shot_2019-03-17at63333pm.png)

新しいビューでは、権限が明示的に付与されているすべてのパスで、特定のプリンシパルに対する特権と制限のセット全体を簡単に確認できます。高度な特権と制限を管理するのに

CRXDE に移動する必要がなくなります。同じビューに統合されました。デフォルトでは、グループ「everyone」が表示されます。

![「everyone」グループの表示](assets/unu-1.png)

ユーザーが参照するプリンシパルの種類を、**ユーザー**、**グループ**&#x200B;または&#x200B;**すべて**&#x200B;から選択して、プリンシパルを検索できるフィルターがあります&#x200B;**。**

![プリンシパルのタイプの検索](assets/image2019-3-20_23-52-51.png)

### プリンシパルの権限の表示 {#viewing-permissions-for-a-principal}

左側のフレームでは、下にスクロールしてプリンシパルを見つけるか、下に示すように、選択したフィルターに基づいてグループまたはユーザーを検索できます。

![プリンシパルの権限の表示](assets/doi-1.png)

名前をクリックすると、割り当てられた権限が右側に表示されます。権限ウィンドウに、特定のパス上のアクセス制御エントリと、設定された制限の一覧が表示されます。

![ACL リストを表示](assets/trei-1.png)

### プリンシパルに対する新しいアクセス制御エントリの追加 {#adding-new-access-control-entry-for-a-principal}

新しい権限は、アクセス制御エントリを追加することで追加できます。「ACE を追加」ボタンをクリックします。

![プリンシパルに新しい ACL を追加](assets/patru.png)

これにより、以下のウィンドウが表示されます。次の手順では、許可を設定する必要があるパスを選択します。

![権限パスを設定](assets/cinci-1.png)

ここでは、パスを選択し、そこで **dam-users** の権限を設定できます。

![dam-users の設定例](assets/sase-1.png)

パスが選択された後、ワークフローはこの画面に戻るので、以下に示すように、利用可能な名前空間（`jcr`、`rep`、`crx` など）から 1 つ以上の権限を選択します。

テキストフィールドを使用して検索し、リストから選択することで権限を追加できます。

>[!NOTE]
>
>権限と説明の詳細なリストについては、[ユーザー、グループおよびアクセス権限の管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)を参照してください。

![特定のパスの権限の検索](assets/image2019-3-21_0-5-47.png) ![選択したパスの表示に従い、「dam-users」の新しいエントリを垂直列に追加します。](assets/image2019-3-21_0-6-53.png)

権限のリストが選択された後、以下に示すように、「拒否」または「許可」からアクセス権の種類を選択できます。

![権限の選択](assets/screen_shot_2019-03-17at63938pm.png) ![権限の選択](assets/screen_shot_2019-03-17at63947pm.png)

### 制限の使用 {#using-restrictions}

与えられたパス上の特権と許可の種類のリストに加えて、この画面では、以下に示すように、きめ細かいアクセス制御の制限を追加することもできます。

![制限を追加](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>各制限の意味について詳しくは、[Jackrabbit Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)を参照してください。

以下に示すように、制限タイプを選択し、値を入力して **+** アイコンを押すと、制限を追加できます。

![制限タイプを追加](assets/sapte-1.png) ![制限タイプを追加](assets/opt-1.png)

次のように、新しい ACE がアクセス制御リストに反映されます。`jcr:write` は、上で追加された `jcr:removeNode` を含む集計権限ですが、`jcr:write` でカバーされているので、下に表示されません。

### ACE の編集 {#editing-aces}

アクセス制御エントリは、プリンシパルを選択し、編集する ACE を選択して編集できます。

例えば、ここでは **dam-users** の以下のエントリを、右側の鉛筆アイコンをクリックして編集できます。

![制限を追加](assets/image2019-3-21_0-35-39.png)

編集画面には事前に選択された設定済み ACE が表示されます。これらは ACE の横にある × アイコンをクリックすると削除できます。また、下に示すように、指定したパスに新しい権限を追加できます。

![エントリを編集](assets/noua-1.png)

ここでは、与えられたパス上の **dam-users** に、`addChildNodes` 権限が追加されます。

![権限を追加](assets/image2019-3-21_0-45-35.png)

右上の「**保存**」ボタンをクリックして変更を保存します。以下のように、変更内容が **dam-users** の新しい権限に反映されます。

![変更を保存](assets/zece-1.png)

### ACE の削除 {#deleting-aces}

アクセス制御エントリを削除して、特定のパス上のプリンシパルに与えられているすべての権限を削除できます。次に示すように、ACE の横にある X アイコンを使用して ACE を削除できます。

![ACE を削除](assets/image2019-3-21_0-53-19.png) ![ACE を削除](assets/unspe.png)

### クラシック UI 権限の組み合わせ {#classic-ui-privilege-combinations}

新しい権限 UI では、付与された基本的な権限が正確に反映されていない事前定義の組み合わせの代わりに、基本的な権限のセットが明示的に使用されます。

その結果、設定内容に関して混乱が生じました。次の表に、クラシック UI の権限の組み合わせと、それらを構成する実際の権限とのマッピングを示します。

<table>
 <tbody>
  <tr>
   <th>クラシック UI 権限の組み合わせ</th>
   <th>権限 UI の権限</th>
  </tr>
  <tr>
   <td>読み取り</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>変更</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>作成</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>削除</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>ACL 読み取り</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>ACL 編集</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>レプリケーション</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
