---
title: PDF Generator の操作の概要
description: 様々な形式のファイルを PDF に変換する方法について説明します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: cc0a3d56-3adc-4d6e-87a3-9a8587bbe3f2
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 100%

---

# PDF Generator の操作の概要 {#introduction-to-working-with-pdf-generator}

PDF Generator では、様々な形式のファイルを PDF に変換できます。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。サポートされるファイル形式のリストについては、「[PDF Generator のソフトウェアサポート](/help/sites-deploying/technical-requirements.md)」を参照してください。

**ファイルを処理するために PDF Generator に送信**

ファイル処理のために、ファイルは PDF Generator に 3 種類の方法で送信できます。

* 管理者は、管理コンソールで PDFG ページにアクセスできます（[PDF Generator を使用したファイルの変換](/help/forms/using/admin-help/converting-files-using-pdf-generator.md)を参照）。
* ユーザーは、`http(s)://'[server]:[port]'/pdfgui.` にログインすると、PDFG エンドユーザーページにアクセスできます。そこから、PDFG ネットワークプリンター、PDFの作成、HTML から PDF、PDF のエクスポート、PDF の最適化などの各ページにアクセスできます。
* これらのサービスのエンドポイントを設定できます参照先 <!--Fix broken link to Managing Endpoints --> [Generate PDF サービスのレコメンデーション](configuring-watched-folder-endpoints.md#generate-pdf-service-recommendations).
