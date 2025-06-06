---
title: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識
description: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f7402f0d-7c19-4a56-8630-208faa197f94
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 100%

---

# PDF ドキュメントでの有効な証明書と期限切れ証明書の認識 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Reader Extensions によって使用権限が適用される PDF ドキュメントを Adobe Reader で開くと、PDF ドキュメントで有効になっている特定の使用権限についての説明がステータスバーに表示されます。

PDF ドキュメントに対する使用権限を指定する電子証明書の有効期限が切れてから、PDF ドキュメントを Adobe Reader で開くと、PDF ドキュメントには使用権限があり、その権限が無効になっていることをユーザーに伝えるダイアログボックスが表示されます。メッセージでは PDF ドキュメントが変更または改ざんされたことが通知されますが、必ずしもそうであるとは限りません。証明書の期限が切れるか、またはドキュメントが修正されると、Adobe Reader にこのメッセージが表示されます。Adobe Reader 7.0.x 以降では、どちらの問題が現在発生しているのかは判断できません。

ダイアログボックスを閉じると、Adobe Reader で PDF ドキュメントが開かれます。Acrobat Reader DC Extensions を使用して適用されていた使用権限は、有効期限が切れているので使用できません。PDF ドキュメントがインタラクティブフォームである場合、フォームフィールドはロックされて、フォームデータを変更できません。
