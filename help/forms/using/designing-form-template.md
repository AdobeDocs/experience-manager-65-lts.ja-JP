---
title: HTML5 フォーム用のフォームテンプレートのデザイン
description: AEM Forms は、XFA フォームテンプレートを HTML5 形式にレンダリングできます。フォームデザイナーは Designer を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 52dc3ecd-339b-4389-b875-4a261d2449e4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 100%

---

# HTML5 フォーム用のフォームテンプレートのデザイン{#designing-form-templates-for-html-forms}

AEM の HTML5 フォームコンポーネントは、XFA フォームテンプレートを HTML5 形式にレンダリングできます。フォームデザイナーは [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。これらのフォームテンプレートはアセットと共に、AEM リポジトリやファイルシステムに配置するか、http で公開することができます。ただし、Forms Manager を使用してフォームを管理する場合には、テンプレートとアセットを AEM リポジトリに置く必要があります。

HTML5 フォームの動作は、その大部分が PDF フォームの動作に一致していますが、両方の形式には他方の形式で適用されない機能がいくつかあります。たとえば、Adobe Reader でバーコードが PDF フォームに適用される方法が Mobile フォームとは異なったり、フォームにデジタル署名を行う方法も各形式で異なります。そのような違いについて詳しくは、[HTML5 フォームと PDF フォームの機能の違い](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)を参照してください。

一般的な XFA 機能の場合、両方の形式で機能するフォームをデザインするために、次のベストプラクティスとガイドラインを参照してください。

## ベストプラクティス {#best-practices}

スキーマバインディングやフォームロジックの記述などの、フォームテンプレートのデザインに関わるほとんどの手順は同じです。ただし、Adobe Reader とブラウザーベースの形式のようなシッククライアントのレンダリングとスクリプティングエンジンに本質的な違いがあるため、いくつかの推奨事項が[ベストプラクティス](/help/forms/using/design-accessible-html5-forms.md)の記事に記載されています。これらのベストプラクティスに従うと、両方の形式で期待通りに機能するようにフォームテンプレートをデザインすることができます。

### AEM Forms Designer の HTML5 フォーム向けの機能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### HTML をプレビューする {#preview-html}

デザインモードに「プレビュー HTML」タブが追加され、フォームデザイナーがデザインプロセス中にフォームを HTML5 形式でプレビューできるようになりました。AEM Forms Designer でこの機能を有効化して設定する方法について詳しくは、[HTML のプレビュー](../../forms/using/preview-xdp-forms-html.md)を参照してください。

#### 手書き署名 {#scribble-signature}

HTML5 フォームの主な対象はタッチデバイスです。そのため、AEM Forms Designer に新しい手書き署名コントロールが追加されました。手書き署名のコントロールは、クリックしてフォームテンプレートにドラッグ＆ドロップすると設定できます。HTML5 レンディションでは手書きフィールドとしてレンダリングされるため、タッチデバイスで署名を手書きするのに使用できます。デスクトップ機器では、手書きフィールドとしてマウスのコントロールで使用できます。この機能の使用方法について詳しくは、[XFA 手書きフィールド](../../forms/using/scribble-signature.md)を参照してください。

![4](assets/4.png)

#### リッチテキスト形式 {#rich-text-format}

テキストフィールドをリッチテキストフィールドに変換できます。テキストフィールドに書式設定オプションのリストを追加します。変換するには、Forms Designer を開き、**[!UICONTROL デザインビュー]**&#x200B;のテキストフィールドを選択します。「**[!UICONTROL フィールド]**」タブで、**[!UICONTROL フィールドの形式]**&#x200B;ドロップダウンリストから「**[!UICONTROL リッチテキスト]**」を選択します。これで、XFA フォームが HTML5 フォームとしてレンダリングされると、そのフィールドはリッチテキストフィールドとしてレンダリングされます。「![最大化](assets/maximize_icon.svg)」を選択して、その他の書式設定オプションを表示します。
