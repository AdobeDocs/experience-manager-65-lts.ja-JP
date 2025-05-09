---
title: 3D アセットのプレビュー
description: Experience Manager で 3D アセットをプレビューする方法を学習します。
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 88dc81aa-f8b2-403e-bd87-ea224ac2d0c2
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 100%

---

# Adobe Experience Manager での 3D アセットのプレビュー {#previewing-3d-assets-aem}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=ja) |
| AEM 6.5 | この記事 |

Adobe Experience Manager では、オーサリングプロセスの一環として、3D アセットのアップロード、配信、インタラクティブプレビューをサポートしています。

Experience Manager のアセットの詳細ページから、インタラクティブ 3D ビューアを使用できます。このビューアには、3D アセットをオービット、ズームおよびパンできるインタラクティブなカメラコントロールのコレクションが含まれます。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Experience Manager でサポートされる 3D プレビューの形式  {#supported-3d-previewing-assets}

インタラクティブ 3D プレビューでは、次のファイル形式をサポートしています。

| 3D ファイル拡張子 | ファイル形式 | MIME タイプ | 備考 |
|---|---|---|---|
| GLB | バイナリ GL 伝送 | model/gltf-binary | |
| GLTF | GL 伝送形式 | model/gltf+json | 下記の&#x200B;**備考**&#x200B;を参照。 |
| OBJ | WaveFront 3D オブジェクトファイル | application/x-tgif | |
| STL | ステレオリソグラフィ | application/vnd.ms-pki.stl | |
| DN | Adobe Dimension | model/x-adobe-dn | 取り込みのみサポート。プレビューは使用できません。 |
| USDZ | 汎用シーン記述 Zip アーカイブ | model/vnd.usdz+zip | 取り込みのみサポート。プレビューは使用できません。 |

>[!NOTE]
>
>gLTF モデルのプレビューでマテリアルがレンダリングされない場合は、次のように、マテリアルに適切に名前を付け、モデルと同じルートフォルダー内の `textures` フォルダーにマテリアルを格納してください。

    Asset（フォルダー）
    model.gltf
    model.bin
    textures（フォルダー）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Experience Manager で 3D アセットをプレビューする際のパフォーマンスに関する考慮事項{#performance-3d-previewing-assets}

アセットの詳細表示ページで 3D アセットを開くときにかかる時間は、帯域幅、画像の複雑さ、サーバーの待ち時間など、いくつかの要因によって異なります。

さらに、カメラをインタラクティブに操作する際に、ワークステーション、ノート型コンピューター、モバイルタッチデバイスなどのクライアントコンピューターの性能を考慮することも重要です。グラフィック性能に優れ、ある程度パワフルなシステムなら、インタラクティブな 3D 表示をよりスムーズで満足なものにすることができます。

**Experience Manager で 3D アセットをプレビューするには：**

1. 3D アセットが Experience Manager にアップロードされていることを確認します。詳しくは、[3D プレビューでサポートされるファイル形式](#supported-3d-previewing-assets)と[アセットのアップロード](/help/assets/manage-assets.md#uploading-assets)を参照してください。
1. Experience Manager の&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで&#x200B;**[!UICONTROL アセット]**／**[!UICONTROL ファイル]**&#x200B;を選択します。

   ![ナビゲーションページ](/help/assets/assets-dm/navigation-assets.png)

1. ページの右上隅付近にある「表示」ドロップダウンリストで「**[!UICONTROL カード表示]**」を選択し、プレビューする 3D アセットに移動します。

   ![3D カードの選択](/help/assets/assets-dm/3d-card-select.png)
   _カード表示で、プレビューする 3D アセットのカードを選択_

1. 3D アセットのカードを選択します。

   ![インタラクティブ 3D プレビュー](/help/assets/assets-dm/3d-preview.png)
   _アセット詳細表示ページでの 3D アセットのインタラクティブプレビュー_
1. 3D アセットのアセット詳細表示ページで、次のいずれかの操作を行います。

   | 表示 | 説明 | マウス操作 | タッチスクリーン操作 |
   | --- | --- | --- | --- |
   | **カメラを回転** | 3D シーンとオブジェクトの周囲でビューを周回させます。 | 左クリックしながらドラッグします。 | 1 本指で押しながらドラッグします。 |
   | **カメラをパン** | ビューを左、右、上、下にパンします。 | 右クリックしながらドラッグします。 | 2 本指で押しながらドラッグします。 |
   | **カメラをズーム** | 3D シーンの領域の内外に移動します。 | ホイールをスクロールします。 | 2 本指でピンチします。 |
   | **カメラを中心に戻す** | カメラを中心の位置に戻し、3D シーンのオブジェクトに合わせます。 | ダブルクリックします。 | ダブルクリックします。 |
   | **リセット** | ページの右下隅付近にあるリセットアイコンを選択して、視野のターゲットポイントを 3D アセットの中心に戻します。リセットを使用しても、アセット全体を表示したり、適切な表示サイズで表示するために、カメラを近づけたり遠ざけたりできます。 |   |   |
   | **全画面表示モード** | フルスクリーンモードに入るには、ページの右下隅にあるフルスクリーンアイコンを選択します。 |   |   |

1. 作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 閉じる]**」を選択します。
