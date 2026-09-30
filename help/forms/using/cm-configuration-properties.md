---
title: Correspondence Management 設定プロパティ
description: このトピックでは、ソリューション固有の設定を使用してAsset Composerを編集する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 23be6248-1013-488e-91e6-ac1f6fb7da50
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 42%
---
# Correspondence Management 設定プロパティ {#correspondence-management-configuration-properties}

これらのプロパティを設定するには、ブラウザーで URL `https://<server>:<port>/<contextPath>/system/console/configMgr` を開き、**Correspondence Management 設定** を選択してください。

Correspondence Management には以下の設定プロパティがあります。

<table>
 <tbody>
  <tr>
   <th><p><strong>プロパティ</strong></p> </th>
   <th><p><strong>説明</strong></p> </th>
   <th><p><strong>デフォルト</strong></p> </th>
   <th><p><strong>指定できる値</strong></p> </th>
  </tr>
  <tr>
   <td><p>インデント</p> </td>
   <td>モジュールのインデント<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td>最小幅の数値</td>
   <td>番号リストをローマ数字から離して使用する場合に、箇条書き/番号フィールドに適用される最小幅。</td>
   <td>8.0mm</td>
   <td>任意の数値</td>
  </tr>
  <tr>
   <td><p>最小幅のローマ数字</p> </td>
   <td><p>ローマ数字を使用する場合に、箇条書き/数値フィールドに適用される最小幅。</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td>レンディションタイプ</td>
   <td>レタープレビューをレンダリングするためにアプリケーションが使用するレンディションのタイプ。 </td>
   <td>HTML レンディション</td>
   <td>HTML レンディション／PDF レンディション</td>
  </tr>
  <tr>
   <td><p>CCR PDF ハイライトの有効化</p> </td>
   <td><p>アプリケーションでPDFのハイライトを有効にします。</p> </td>
   <td><p>true</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>対象のハイライトの種類</p> </td>
   <td><p>アプリケーションのターゲットハイライトタイプ。</p> </td>
   <td><p>境界線</p> </td>
   <td><p>境界線／塗りつぶし／なし</p> </td>
  </tr>
  <tr>
   <td><p>ターゲットハイライトカラー</p> </td>
   <td><p>アプリケーションのハイライトカラーをターゲットにします。</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>任意の RGB カラー（R;G;B の形式）</p> </td>
  </tr>
  <tr>
   <td><p>コンテンツのハイライトの種類</p> </td>
   <td><p>アプリケーションのコンテンツハイライトタイプ。</p> </td>
   <td><p>塗りつぶし</p> </td>
   <td><p>境界線／塗りつぶし／なし</p> </td>
  </tr>
  <tr>
   <td><p>コンテンツのハイライトの色</p> </td>
   <td><p>アプリケーションのコンテンツのハイライトカラー。</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>任意の RGB カラー（R;G;B の形式）</p> </td>
  </tr>
  <tr>
   <td><p>フィールドのハイライトの種類</p> </td>
   <td><p>アプリケーションのフィールドのハイライトタイプ。</p> </td>
   <td><p>塗りつぶし</p> </td>
   <td><p>境界線／塗りつぶし／なし</p> </td>
  </tr>
  <tr>
   <td><p>フィールドのハイライトの色</p> </td>
   <td><p>アプリケーションのフィールドのハイライトカラー。</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>任意の RGB カラー（R;G;B の形式）</p> </td>
  </tr>
  <tr>
   <td><p>アプリケーションのタイムアウト</p> </td>
   <td><p>アプリケーションが数秒でタイムアウトします。</p> </td>
   <td><p>1200</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td><p>PDF ドキュメントのパラメーター名</p> </td>
   <td><p>ポストプロセスにおけるPDF ドキュメントのパラメーター名。</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>XML データのパラメーター名</p> </td>
   <td><p>後処理のXML ドキュメント（データ）のパラメーター名。</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>XDP ドキュメントのパラメーター名</p> </td>
   <td><p>投稿プロセスに送信されるXDP ドキュメントのパラメーター名。</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>リダイレクト URL パラメーター名</p> </td>
   <td><p>ポストプロセスから送信されたリダイレクト URLのパラメーター名。 この値は、任意の文字列変数名にすることができます。</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>PDF 送信の種類</p> </td>
   <td><p>PDF送信タイプ（アプリケーションからの送信時に生成されるPDFのタイプ）。</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>インタラクティブ／非インタラクティブ</p> </td>
  </tr>
  <tr>
   <td><p>データディクショナリインスタンスの最適化</p> </td>
   <td><p>サーバーとクライアントの両方で、データ要素インスタンスの転送を最適化できます。</p> </td>
   <td><p>true</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>不整合の自動修正 </p> </td>
   <td><p>有効にすると、レター割り当てで発生する可能性のある不整合が自動的に処理されます。</p> </td>
   <td><p>true</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>設定済みのデータ形式を使用</p> </td>
   <td><p>設定されたデータ編集フォーマットとデータ表示形式を使用するかどうかを制御します。</p> </td>
   <td><p>true</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>データの表示形式</p> </td>
   <td><p>データのロケール固有の表示形式を指定します。</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>--</p> </td>
  </tr>
  <tr>
   <td><p>データ編集形式</p> </td>
   <td><p>データの形式を編集します。 データを文字列として書き込む場合や、文字列からデータを解析する場合に使用します。</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>「公開」でレターインスタンスを管理</p> </td>
   <td><p>レター機能を有効/無効にします（Publish Serverにのみ適用）。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>監査の有効化</p> </td>
   <td><p>監査機能を有効/無効にします。 falseの場合、すべてのアクションの監査ログは無効になります。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>読み取りの監査を有効化</p> </td>
   <td><p>アセット読み取りの監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>作成の監査を有効化</p> </td>
   <td><p>アセット作成の監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>更新の監査を有効化</p> </td>
   <td><p>アセット更新の監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>復帰の監査を有効化</p> </td>
   <td><p>アセットの復帰の監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>公開の監査を有効化</p> </td>
   <td><p>アセットの公開の監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>SaveAsDraft の監査を有効化</p> </td>
   <td><p>レターの下書きを保存するための監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>送信の監査を有効化</p> </td>
   <td><p>レター送信の監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>メールの監査を有効化</p> </td>
   <td><p>電子メールレターの監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>印刷の監査を有効化</p> </td>
   <td><p>レターを印刷するための監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>カスタム配信の監査を有効化</p> </td>
   <td><p>レターのカスタム配信の監査機能を有効/無効にします。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>添付ドキュメントパラメーター名</p> </td>
   <td><p>後処理に送信される添付ファイル文書のパラメーター名。</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任意の文字列変数名</p> </td>
  </tr>
  <tr>
   <td><p>CM ユーザールート</p> </td>
   <td><p>すべてのCorrespondence Management ユーザーアセットを含むフォルダーのURL。</p> </td>
   <td><p>--</p> </td>
   <td><p>有効なフォルダーの場所</p> </td>
  </tr>
  <tr>
   <td><p>レターのキャッシュサイズ</p> </td>
   <td><p>キャッシュに保持する文字の最大数を指定します。</p> <p>この値を変更すると、<code>in-memory</code> キャッシュがクリーンアップされます。</p> </td>
   <td><p>100</p> </td>
   <td><p>任意の数値</p> </td>
  </tr>
  <tr>
   <td><p>レターキャッシュを有効化</p> </td>
   <td><p>レターキャッシュを有効/無効にします。</p> <p>この値を変更すると、<code>in-memory </code> キャッシュがクリーンアップされます。</p> </td>
   <td><p>true</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>データ要素の順序</p> </td>
   <td><p>データ要素は、レターのシーケンスに従ってインターフェイス内で順序付けされます。</p> </td>
   <td><p>true</p> </td>
   <td><p>true／false</p> </td>
  </tr>
  <tr>
   <td><p>サポートの再読み込み</p> </td>
   <td><p>サーバーサイドでレンダリングされるレターのリロードサポートを有効/無効にします。</p> <p>無効にすると、レターのレンダリングのパフォーマンスが向上します。</p> </td>
   <td><p>false</p> </td>
   <td><p>true／false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>一時フォルダー</td>
   <td>一時フォルダーの場所</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>リモート保存</td>
   <td>レターインスタンスを指定された処理中の作成者で保存します。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>互換性オプション</td>
   <td>形式configname :configvalueの互換性オプションをコンマで区切ります。</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Debug ディレクトリ </p> <p> </p> </td>
   <td>デバッグのファイルシステムフォルダーの場所。 ディレクトリが<code>exists</code>でない場合、デバッグダンプは生成されません。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
