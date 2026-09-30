---
title: 早期導入機能とプレリリース機能を統合するために、機能切替スイッチを有効にする
description: 機能切替スイッチは、管理者がランタイム環境で新機能を有効にできる AEM の機能です。
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 8b6dea41-540b-498a-b52b-e584a9255f25
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: ae206583-dab1-444b-b978-a37aad4a988c
    internal-label: Experience Manager 6.5 LTS
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 100%
---
# Adobe Experience Manager（AEM）6.5 の機能切替スイッチ{#enable-feature-toggle-aem-forms-65}

機能切替スイッチは、管理者が特定の機能を動的に有効または無効にできる AEM の機能です。 この機能は、大規模なデプロイメントやコードベースの変更を必要とせずに、**早期導入機能**&#x200B;や&#x200B;**プレリリース機能**&#x200B;を管理する場合に特に役立ちます。 これにより、AEM 環境でアクセスできる機能に対する柔軟性と制御が確保されます。

## 機能切替スイッチの有効化 {#enable-feature-toggle-65}

早期導入用の機能切替スイッチや新機能は、次の手順に従って、**AEM web コンソール**&#x200B;を通じて設定できます。

1. AEM Forms インスタンスにログインします。
2. `http://<author-instance-url>:portnumber/system/console/configMgr` に移動します。
3. Configuration Manager で **Adobe Granite Dynamic Toggle Provider** を検索します。
4. アイコン ![鉛筆アイコン](assets/illustratorcc_penciltool_cur_edit_2_17.png) をクリックします。
5. 「[!UICONTROL 有効な切替スイッチ]」セクションで、![鉛筆アイコン](assets/aem6forms_add.png) をクリックします。
6. 以下の画像に示すように、機能の機能切替スイッチ ID を追加します。
   ![機能切替スイッチの追加](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >機能切替スイッチ ID は、早期導入機能に固有のドキュメントで確認できます。

7. 「保存」をクリックします。

## 機能切替スイッチの無効化 {#disable-feature-toggle-65}

切替スイッチが有効になっている機能の切替スイッチを無効にするには、次の手順に従います。

1. AEM Forms インスタンスにログインします。
2. `http://<author-instance-url>:portnumber/system/console/configMgr` に移動します。
3. Configuration Manager で **Adobe Granite Dynamic Toggle Provider** を検索します。
4. アイコン ![鉛筆アイコン](assets/illustratorcc_penciltool_cur_edit_2_17.png) をクリックします。
5. 「[!UICONTROL 無効な切替スイッチ]」セクションで、![鉛筆アイコン](assets/aem6forms_add.png) をクリックします。
6. 無効にする機能の切替スイッチ番号を追加します。
   ![切替スイッチの削除](assets/remove_toggle_feature_forms.png)
7. 「保存」をクリックします。

## 技術的な考慮事項

機能切替スイッチは環境に固有で、実行時に管理されるので、サーバーの再起動は必要ありません。 ただし、一部の機能では、変更を反映するために、関連するページを更新したり、キャッシュを消去したりする必要がある可能性があります。
`http://<author-instance-url>:4502/etc.clientlibs/toggles.json` 経由で、環境の機能切替スイッチを通じて有効になっている機能のリストにアクセスできます。
