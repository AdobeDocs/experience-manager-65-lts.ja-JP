---
title: '[!DNL Experience Manager Assets] と  [!DNL Adobe Workfront] の統合'
description: ' [!DNL Assets]  と  [!DNL Workfront] の統合の概要'
role: Admin,Leader,Architect
feature: Workfront Integrations and Apps
hide: true
solution: Experience Manager, Workfront
exl-id: 5181d278-2e6e-41f7-891e-1067a03de016
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager Assets] と [!DNL Adobe Workfront] の統合 {#assets-integration-overview}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=ja) |
| AEM 6.5 | この記事 |

[!DNL Adobe Workfront] は作業管理アプリケーションで、作業のライフサイクル全体を一元的に管理するのに役立ちます。[!DNL Workfront] と [!DNL Adobe Experience Manager Assets] の統合により、組織は、作業とデジタルアセット管理を本質的に関連付けることで、コンテンツベロシティを向上させ市場投入までの時間を短縮することができます。Workfront での作業を管理するコンテキスト内で、ユーザーは必要なドキュメントと画像にアクセスできます。

[!DNL Workfront for Experience Manager enhanced connector] により、エンドツーエンドのワークフローでビジネスプロセスが強化され、エンドツーエンドのクライアントエクスペリエンスと一元化されたストレージをパーソナライズできます。アドビでは、標準コネクタと、これら 2 つのソリューションを統合する拡張コネクタを提供します。比較については、以下のサポートされる機能を参照し、[ [!DNL enhanced connector]の新機能を参照してください](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)。

[!DNL Workfront for Experience Manage enhanced connector] を使用すると、組織で次のことが可能です。

* Workfront でリンクされた Experience Manager フォルダーを自動作成し、Workfront のポートフォリオ、プログラム、プロジェクトに基づいてフォルダーを整理します。
* Workfront プロジェクトメタデータをリンクされた Experience Manager フォルダーと同期してください。
* Experience Manager メタデータを新しいバージョンで更新します。
* Experience Manager ワークフローを使用して、設定可能な条件に基づいて Workfront オブジェクトのステータスを設定してください。
* アセットを Experience Manager パブリッシュ環境または Brand Portal に公開します。

プラットフォームのサポートと[拡張コネクターの前提条件](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience)を参照してください。

>[!IMPORTANT]
>
>* アドビでは、[!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと設定を、認定パートナーまたは [!DNL Adobe Professional Services] を通じてのみ行うことを求めています。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* アドビでは、拡張コネクタバージョン 1.7.4 以降をサポートしています。以前のプレリリースバージョンやカスタムバージョンはサポートされていません。拡張コネクタのバージョンを確認するには、[パッケージマネージャー](/help/sites-administering/package-manager.md)の左側のパネルで使用可能な `digital.hoodoo` グループに移動します。
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、[試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)を参照してください。

## [!DNL Assets] と [!DNL Workfront] の間の異なる統合の比較  {#feature-parity-matrix}

[!DNL Assets] と [!DNL Workfront] の間の様々なタイプの統合を通じて利用できる機能の詳細は、以下のとおりです。

| 機能 | 説明 | [!DNL Workfront] と [!DNL Assets Essentials]：*コネクタが不要（標準）* | [!DNL Workfront for Experience Manager enhanced connector]：*コネクタが必要* | Workfront と [!DNL Experience Manager as a Cloud Service]：*コネクタが不要（標準）* |
|----|----|----|-----|-----|
| デプロイメント方法 | どの [!DNL Assets] の提供に適切か。 | Assets Essentials | Adobe Managed Services、オンプレミス | Cloud Service |
| **一般** |
| [!DNL Workfront] から [!DNL Assets] へのデジタルファイルの送信  | WF ドキュメントの最新バージョンを AEM Assets にアップロードして、ドキュメントの新しいバージョンとしてリンクさせることができます。 | ✓ | ✓ | ✓ |
| AEM フォルダーの Workfront オブジェクトへの手動リンク | 既存の AEM フォルダーは Workfront フォルダーとしてリンクでき、その子アセットは新しい Workfront ドキュメントとしてリンクされます。 | ✓ | ✓ | ✓ |
| [!DNL Assets] を Workfront オブジェクトにリンク | AEM 内の既存のアセットを新しい Workfront ドキュメントにリンクしたり、既存のドキュメントの新しいバージョンとしてリンクしたりできます。 | ✓ | ✓ | ✓ |
| リンクされたフォルダーに追加されたアセットは、AEM に自動的に送信されます | リンクされたフォルダーにドキュメントを追加すると、関連するアセットが新しいアセットとして AEM Assets に自動的にアップロードされます。 | ✓ | ✓ | ✓ |
| Workfront 内からリンクされた AEM Assets をダウンロード | Workfront 内でアセットをリンクすると、ユーザーはアセットのバイトをダウンロードできます。 | ✓ | ✓ | ✓ |
| Workfront 内から AEM Assets を検索 | Workfront の AEM Assets セレクターを使用すると、アセットのフルテキスト検索が可能になります。 | ✓ | ✓ | ✓ |
| Workfront 内から AEM フォルダーを検索 | Workfront の AEM Assets セレクターを使用すると、フォルダーのフルテキスト検索が可能になります。 | ✓ | ✓ | ✓ |
| Workfront 内から AEM フォルダー階層を表示し、階層内を移動する | Workfront の AEM Assets セレクターを使用すると、AEM でユーザーに設定された関連アクセス制御および権限によって制限される AEM Assets 階層を参照できます。 | ✓ | ✓ | ✓ |
| AEM タイムラインでアセットのバージョンを追跡 | Workfront と AEM の間でドキュメントのバージョン履歴を維持します。 | ✓ | ✓ | ✓ |
| Workfront の AEM Assets からアセットのリンクを解除 | AEM の既存のリンクされたアセットのリンクを、関連する Workfront ドキュメントから解除できます。AEM 内の元のアセットは削除されません。 | ✓ | ✓ | ✓ |
| Workfront から AEM Assets に新しくバージョン管理されたアセットを追加 | Workfront のドキュメントに新しく追加されたバージョンが追加された場合、ユーザーは新しいバージョンを AEM に送信して、既存のバージョンに置き換えることができます。 | ✓ | ✓ | ✓ |
| 「ユーザーを AEM に誘導」をクリックしたときに Workfront でリンクされたアセット | ユーザーは、Workfront 内からリンクされたアセットをプレビューするように AEM に誘導されます。 | ✓ | ✓ | 今後提供予定 |
| リンクされた AEM フォルダーを Workfront に自動的に作成 | プロジェクトのステータスを使用して、リンクされた AEM フォルダーを Workfront に自動的に作成します。Workfront のポートフォリオ、プログラムおよびプロジェクトに基づいて、AEM フォルダーを自動的に設定します。 | 不可 | ✓ | なし |
| Workfront から AEM リポジトリに直接移動 | ユーザーが Workfront 内に設定された使用可能な AEM リポジトリに移動できるようになります。 | ✓ | いいえ | ✓ |
| リンクされた AEM フォルダーを Workfront に作成 | 「ドキュメント」タブのオプションを使用して、リンクされた AEM フォルダーを Workfront に作成します。 | ✓ | いいえ | ✓ |
| コメントの同期 | アセットのコメントを [!DNL Workfront] から [!DNL Assets] への自動的に同期 | 不可 | ✓ | なし |
| 単一の AEM 環境に接続する複数の Workfront 環境をサポート | 複数の Workfront 環境のユーザーが単一の AEM 環境に接続できます。 | ✓ | いいえ | ✓ |
| 単一の Workfront 環境に接続する複数の AEM 環境をサポート | 単一の Workfront 環境内のユーザーが、複数の AEM 環境間でアセットを送信またはリンクすることができます。 | ✓ | ✓ | ✓ |
| **メタデータ** |
| Workfront のアセットメタデータの AEM Assets へのマッピング | Workfront オブジェクトおよびカスタムフォームプロパティは、AEM のアセットメタデータプロパティにマッピングできます。値は、最初のアップロード／リンク時にプッシュされます。 | ✓ | ✓ | ✓ |
| Workfront でドキュメントのカスタムフォームを自動的に作成 | AEM ワークフローを使用して、Workfront のドキュメント、タスク、問題にカスタムフォームを添付します。 | 不可 | ✓ | なし |
| AEM Assets と Workfront の間でメタデータを双方向に自動更新 | AEM Assets と Workfront の間でメタデータを自動的に更新します。アセットを最初に Workfront から AEM にプッシュし、双方向のメタデータ更新が適切に機能するように、Workfront アセットメタデータを AEM Assets にマッピングする必要があります。 | 不可 | ✓ | なし |
| AEM にマッピングされたメタデータを Workfront でリアルタイム表示 | Workfront ドキュメントの詳細パネルおよびドキュメントの概要パネル内で、AEM にマッピングされた最新のメタデータを表示します。 | ✓ | いいえ | ✓ |
| 更新された Workfront メタデータの AEM へのリアルタイムプッシュ | アセットや新しいバージョンのアセットを再プッシュすることなく、マッピングされた Workfront メタデータを AEM に自動的に更新します。 | ✓ | いいえ | ✓ |
| Workfront メタデータ を AEM Assets フォルダーへマッピング | Workfront プロジェクトのメタデータを、リンクされた AEM フォルダーと同期します。 | いいえ | ✓ | ✓ |
| 新しいバージョンで AEM メタデータを更新 | AEM の設定を行うことにより、Workfront のアセットのバージョンが新しくなった場合にも、メタデータに加えられた変更をプッシュするかどうかを指定できます。 | いいえ | ✓ | いいえ |
| Workfront のカスタムフォームが変更されると AEM メタデータを自動的に更新 | AEM では、Workfront のドキュメントフォームの更新を購読することができます。その結果、Workfront ドキュメントのカスタムフォームメタデータが更新されると、マッピングされた AEM メタデータフィールドの値が編集されます。 | 不可 | ✓ | いいえ |
| **ワークフロー（標準）** |
| リンクされたアセットに新しい配達確認バージョンを作成 | Workfront でアセットをリンクすると、配達確認を自動的に生成できます。 | 不可 | カスタム | いいえ |
| Workfront オブジェクトのステータスを設定 | AEM ワークフローを使用して、設定可能な条件に基づく Workfront オブジェクトのステータスを設定します。 | いいえ | ✓ | 今後提供予定 |
| AEM パブリッシュ環境または Brand Portal にアセットを公開 | リンクされたアセットを AEM パブリッシュ環境または Brand Portal に自動的に公開するオプションをWorkfront ユーザーに与えます。 | いいえ | ✓ | 今後提供予定 |
