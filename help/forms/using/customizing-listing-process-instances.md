---
title: プロセスインスタンスのリストのカスタマイズ
description: AEM Forms Workspace のプロセスインスタンスで表示されるプロパティをカスタマイズする方法。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 7ffde604-2f56-4b53-88ab-5fac321e4753
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---

# プロセスインスタンスのリストのカスタマイズ {#customizing-the-listing-of-process-instances}

プロセスインスタンスリストは、AEM Forms Workspace のトラッキングタブに表示されます。

プロセスインスタンスリストで、各プロセスインスタンスに対して AEM Forms Workspace はそのインスタンスのいくつかのプロパティを表示します。次のプロパティを各プロセスインスタンスで使用できます。これらのプロパティは、プロセスインスタンスのコンポーネントモデルに属性として格納されていて、表示やテンプレートで使用できます。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>説明</td>
   <td>プロセスインスタンスの説明。</td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>プロセスインスタンスのイニシエーターの名前。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>プロセスインスタンスのイニシエーターの ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>プロセスが完了したときのタイムスタンプ。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>プロセスインスタンスの ID。</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = 起動済み<br /> 1 = 実行中<br /> 2 = 完了<br /> 3 = 完了中<br /> 4 = 終了<br /> 5 = 終了中<br /> 6 = 休止<br /> 7 = 休止中<br /> 8 = 休止解除中</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>プロセスの名前。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>プロセスが開始したときのタイムスタンプ。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>プロセス変数のオブジェクトの配列。各プロセス変数オブジェクトは、<strong>名前</strong>（プロセス変数の名前）、<strong>値</strong>（プロセス変数の値）、および<strong>タイプ</strong>（プロセス変数のタイプ）を含みます。</td>
  </tr>
 </tbody>
</table>

**例：**

プロセスインスタンスのカードにプロセスインスタンスの `description` プロパティを表示するには、次の手順を実行します。

1. 「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に従います。
1. 以下の操作を実行します。

   1. 存在しない場合は、/libs/ws/js/runtime/templates/processinstance.html を /apps/ws/js/runtime/templates/ にコピーします。「**すべて保存**」をクリックします。
   1. processinstance.html に class = &#39;processDescription&#39; を指定した div をプロセス説明として追加します。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 次を実行します。

   1. /apps/ws/js/registry.js を開いて編集します。
   1. `text!/lc/libs/ws/js/runtime/templates/processinstance.html` を検索して `text!/lc/`**アプリ**/ws/js/runtime/templates/processinstance.html と置き換えます。

1. 上記の変更を行うには、次のように、スタイルシート /apps/ws/css/newStyle.css にエントリを追加することによって、CSS ファイルを更新する必要があります。

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement and user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
