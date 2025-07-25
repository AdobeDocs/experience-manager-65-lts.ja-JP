---
title: Google Chrome、Firefox、Microsoft&reg; Edge、Microsoft&reg; Internet Explorer、または Apple Safari で XFA ベースの PDF フォームを開けない
description: Google Chrome、Firefox、Microsoft&reg; Edge、Microsoft&reg; Internet Explorer、または Apple Safari で XFA ベースの PDF フォームを開けない
feature: Adaptive Forms,Document Services
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: a28b084e-ec74-4c05-a90c-d447792faa41
source-git-commit: 9421c7d0b5cf80a0f2d2d82034091ffe4f875af6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Google Chrome、Firefox、Microsoft® Edge、Microsoft® Internet Explorer、Apple Safari で XFA ベースの PDF フォームを開けない{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

最近の多くのブラウザーバージョンには、XFA ベースの PDF フォームに対する独自の制限付きサポートが含まれています。これらのブラウザーで XFA ベースの PDF フォームを開くことはできますが、提供される機能は限られています。最新のブラウザーで XFA ベースの PDF フォームを開いたり送信したりできない場合は、次のいずれかの方法を使用します。

* XFA ベースの PDF フォームを開いて送信するには、[Adobe® Acrobat®](https://www.adobe.com/jp/acrobat.html) または [Adobe® Adobe® Reader®](https://get.adobe.com/jp/reader/) のバージョン 8 以降を使用します。
* Acrobat と Reader は、Microsoft® Windows® 上では、PDF を保護ビューモードで開くように設定することができます。これにより、XFA ベースの PDF フォームを開けなくなります。Acrobat または Reader の保護ビューモードが無効になっていることを確認します。 詳しくは、[保護されたビュー（Windows のみ）](https://helpx.adobe.com/jp/reader/using/protected-mode-windows.html)を参照してください。
* （フォーム開発者向け）Adobe Experience Manager Forms は次の機能もサポートしています。

   * [XFA ベースのフォームを HTML5 フォームにレンダリング](/help/forms/using/introduction.md#key-capabilities-of-html-forms-br)して、iPad のようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができるようにします。フォームの HTML5 レンディションは、フォームデザインのレイアウトを保持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。
   * [XFA ベースのフォームをモバイルレスポンシブなアダプティブフォームに変換](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)します。これらのフォームは、レスポンシブレイアウトやパーソナライズ機能を提供し、フィールドやセクションを必要に応じて追加または削除することで、ユーザーの応答に動的に適応します。また、様々なデータソース、レコードのドキュメント機能、パフォーマンス評価のための Adobe Analytics への簡単な接続を利用するためにすぐに使用できるコネクタも用意されています。詳細情報は、[主な特長と機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=ja)を参照してください。
これにより、XFA フォームに対するテクノロジー投資が保護され、エンドユーザーに最適なエクスペリエンスを継続的に提供することができます。詳しくは、[Adobe Experience Manager Forms 製品ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=ja)を参照してください。
