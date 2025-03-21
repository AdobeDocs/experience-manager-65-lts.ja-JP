---
title: 監視フォルダーのバックアップ方法
description: ここでは、監視フォルダーが様々なバックアップと回復のシナリオから受ける影響、それらのシナリオの制限事項や結果、データ損失を最小限に抑える方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5955deb0-9d1c-4b61-a202-41ef03a23cf8
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 100%

---

# 監視フォルダーのバックアップ方法 {#backup-strategies-for-watched-folders}

ここでは、監視フォルダーが様々なバックアップと回復のシナリオから受ける影響、それらのシナリオの制限事項や結果、データ損失を最小限に抑える方法について説明します。

「*監視フォルダー*」は、ファイルシステムベースのアプリケーションです。監視フォルダーによって、監視フォルダー階層にあるファイルを操作するように設定されたサービス操作が呼び出されます。このファイルは、監視フォルダー階層の次のいずれかのフォルダーに含まれています。

* 必要情報
* ステージ
* 出力
* 失敗
* 保存

ユーザーまたはクライアントアプリケーションは、まずファイルやフォルダーを入力フォルダーに配置します。次に、サービス操作によりファイルが処理対象としてステージフォルダーに移動されます。サービスによって指定の操作が実行されると、変更済みのファイルが出力フォルダーに保存されます。正常に処理されたソースファイルは保存用フォルダーに、処理に失敗したファイルは失敗フォルダーに移動されます。監視フォルダーの `Preserve On Failure` 属性が有効な場合は、処理に失敗したソースファイルは保存用フォルダーに移動されます（[監視フォルダーエンドポイントの設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)を参照）。

監視フォルダーのバックアップは、ファイルシステムをバックアップすることによって実行できます。

>[!NOTE]
>
>このバックアップは、データベースやドキュメントストレージバックアップおよび回復プロセスに依存しません。

## 監視フォルダーの動作方法 {#how-watched-folders-work}

ここでは、監視フォルダーのファイル操作プロセスを説明します。このプロセスを理解してから、回復計画を立てることが重要です。この例では、監視フォルダーの `Preserve On Failure` 属性が有効になっています。ファイルは、到着した順序で処理されます。

次の表は、プロセス全体での 5 つのサンプルファイル（file1、file2、file3、file4、file5）のファイル操作を示しています。表では、横軸は時間（Time 1 つまり T1）を表し、縦軸は監視フォルダー階層内のフォルダー（入力など）を表しています。

<table>
 <thead>
  <tr>
   <th><p>フォルダー</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>必要情報</p></td>
   <td><p>file1、file2、file3、file4</p></td>
   <td><p>file2、file3、file4</p></td>
   <td><p>file3、file4</p></td>
   <td><p>file4</p></td>
   <td><p>empty</p></td>
   <td><p>file5</p></td>
   <td><p>empty</p></td>
  </tr>
  <tr>
   <td><p>ステージ</p></td>
   <td><p>empty</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>empty</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>出力</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out、file2_out</p></td>
   <td><p>file1_out、file2_out</p></td>
   <td><p>file1_out、file2_out、file4_out</p></td>
   <td><p>file1_out、file2_out、file4_out</p></td>
  </tr>
  <tr>
   <td><p>失敗</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file3_fail、file3 </p></td>
   <td><p>file3_fail、file3 </p></td>
   <td><p>file3_fail、file3 </p></td>
  </tr>
  <tr>
   <td><p>保存</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1 </p></td>
   <td><p>file1、file2 </p></td>
   <td><p>file1、file2 </p></td>
   <td><p>file1、file2、file4 </p></td>
   <td><p>file1、file2、file4 </p></td>
  </tr>
 </tbody>
</table>

各時間のファイル操作について、次に説明します。

**T1：** 4 つのサンプルファイルが入力フォルダーに配置されます。

**T2：**&#x200B;サービス操作により、file1 が操作対象としてステージフォルダーに移動されます。

**T3：**&#x200B;サービス操作により、file2 が操作対象としてステージフォルダーに移動されます。file1 の結果は出力フォルダーに配置され、file1 は保存フォルダーに移動されます。

**T4：**&#x200B;サービス操作により、file3 が操作対象としてステージフォルダーに移動されます。file2 の結果は出力フォルダーに配置され、file2 は保存フォルダーに移動されます。

**T5：**&#x200B;サービス操作により、file4 が操作対象としてステージフォルダーに移動されます。file3 の操作は失敗し、file3 はサービス操作により失敗フォルダーに配置されます。

**T6：**&#x200B;サービス操作により、file5 が入力フォルダーに配置されます。file4 の結果は出力フォルダーに配置され、file4 は保存フォルダーに移動されます。

**T7：**&#x200B;サービス操作により、file5 が操作対象としてステージフォルダーに移動されます。

## 監視フォルダーのバックアップ {#backing-up-watched-folders}

監視フォルダーファイルシステム全体を他のファイルシステムにバックアップすることをお勧めします。

## 監視フォルダーの復元 {#restoring-watched-folders}

ここでは、監視フォルダーの復元方法について説明します。監視フォルダーは、1 分以内に完了する有効期限の短いプロセスを呼び出すことがよくあります。このような場合は、何時間単位のバックアップを使用した監視フォルダーの復元では、データ損失を防ぐことができません。

例えば、時間 T1 においてバックアップし、T7 でサーバーに障害が発生した場合、file1、file2、file3 および file4 は既に処理されています。T1 で取得したバックアップを使用して監視フォルダーを復元してもデータ損失を防げません。

より新しいバックアップを取得している場合、これらのファイルを復元できます。ファイルを復元するときは、現在のファイルが存在する監視フォルダーの階層フォルダーを考慮します。

**ステージ：**&#x200B;このフォルダー内のファイルは、監視フォルダーの復元後に再処理されます。

**入力：**&#x200B;このフォルダー内のファイルは、監視フォルダーの復元後に再処理されます。

**結果：** このフォルダー内のファイルは、処理されません。

**出力：** このフォルダー内のファイルは、処理されません。

**保存：** このフォルダー内のファイルは、処理されません。

## データ損失を最小限に抑える方法 {#strategies-to-minimize-data-loss}

次の方法を使用すると、監視フォルダーを復元するときに出力および入力フォルダーのデータ損失を最小限に抑えることができます。

* 出力フォルダーおよび失敗フォルダーを頻繁に（例えば 1 時間ごとに）バックアップし、結果ファイルおよび失敗ファイルの損失を回避します。
* 監視フォルダー以外のフォルダーに入力ファイルをバックアップします。これによって、出力フォルダーと失敗フォルダーのどちらにもファイルが見つからない場合でも、回復後にファイルを確実に利用できるようになります。ファイルの命名スキームを一貫したものにしてください。

  例えば、出力を&#x200B;`%F.`*拡張子*&#x200B;で保存する場合、出力ファイルは入力ファイルと同じ名前になります。これにより、操作される入力ファイルおよび再送信が必要な入力ファイルを判別できます。結果フォルダーに file1_out ファイルしか確認できず、file2_out、file3_out および file4_out が見つからない場合、file2、file3 および file4 を再送信する必要があります。

* 使用可能な監視フォルダーのバックアップが、ジョブの処理時間より古い場合は、システムが監視フォルダーを作成し、ファイルを自動的に入力フォルダーに配置できるようにする必要があります。
* 使用可能な最新のバックアップが完全な最新版ではなく、バックアップ時間がファイルの処理時間より短く、監視フォルダーが復元されている場合は、ファイルは、次のいずれかのステージで操作されています。

   * **ステージ 1：**&#x200B;入力フォルダー内にあります。
   * **ステージ 2：**&#x200B;ステージフォルダーにコピーされましたが、プロセスはまだ開始されていません。
   * **ステージ 3：**&#x200B;ステージフォルダーにコピーされており、プロセスが開始されています。
   * **ステージ 4：**&#x200B;プロセスが進行中です。
   * **ステージ 5：**&#x200B;結果が返されています。

  ファイルがステージ 1 にある場合、ファイルは操作されます。ファイルがステージ 2 または 3 にある場合、再操作用に入力フォルダーに配置されます。

  >[!NOTE]
  >
  >ファイルの操作が複数回発生した場合は、データ損失は防げますが、結果が重複する場合があります。

## まとめ {#conclusion}

監視フォルダーの動的かつ継続的に変化する特性により、監視フォルダーの復元は 1 日以内にバックアップされたファイルで行われる必要があります。ベストプラクティスは、結果をバックアップし、入力フォルダーをサーバーに格納し、入力ファイルを追跡して、障害の発生時にジョブを再送信できるようにすることです。
