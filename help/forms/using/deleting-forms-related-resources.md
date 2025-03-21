---
title: フォームと関連リソースの削除
description: AEM Forms でフォームまたはアセットを削除する方法と、参照先および参照元アセットと XFA フォームに対する影響。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: e9b7e1b1-23a3-4da9-a5b4-c30f70441341
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 100%

---

# フォームと関連リソースの削除 {#deleting-forms-and-related-resources}

フォームとアセットを削除して、これらのアセットをリポジトリから除去できます。削除操作は、すべてのアセットタイプとフォルダーに対して動作します。

オーサーインスタンスからアセットを削除すると、そのアセットはパブリッシュインスタンスからも削除されます。AEM Forms サーバーはオーサーインスタンスとパブリッシュインスタンスからなります。オーサーインスタンスは、フォームのアセットとリソースを作成したり管理したりするためのものです。パブリッシュインスタンスは、発行済みフォームのアセットと関連リソースを含み、これらはエンドユーザーが使用できます。

## フォームの削除方法 {#how-to-delete-a-form}

1. `https://[hostname]:'port'/aem/forms.html.` にアクセスして AEM Forms ユーザーインターフェイスにログインします。
1. 削除するフォームを探して移動します。ツールバーで ![aem6forms_delete2](assets/aem6forms_delete2.png) 削除をクリックし、削除操作を確定します。

   >[!NOTE]
   >
   >一度に削除できるフォームは 1 つだけです。複数のフォームの削除は、1 つずつ個別に削除するか、親フォルダーを削除します。

1. アセットを削除する前に、AEM forms は参照をチェックし、明示的な確認を求めます。関係ステータスとは無関係にアセットを削除する場合は、「削除を強制」をクリックします。

   >[!NOTE]
   >
   >他のアセットによって参照されているアセットを削除すると、機能に問題を起こす可能性があります。

   >[!NOTE]
   >
   >選択したアセットがフォルダーで、その階層にそのようなアセットが含まれている場合は、それ以外のアセットを個別に削除するか、フォルダー全体を削除します。

## 参照先 XFA フォームを削除した場合の影響 {#impact-of-deleting-a-referenced-xfa-form}

AEM Forms では、XFA フォームテンプレートは、アダプティブフォームまたは別の XFA フォームテンプレートによって参照できます。またテンプレートは、リソースまたは別の XFA テンプレートを参照することもできます。

アダプティブフォームによって参照されている XFA フォームを削除すると、アダプティブフォームを破損する可能性があるのでお勧めできません。アダプティブフォームが XFA フォームを参照しているときは、それらのフィールドは連結されています。XFA の削除後に、アダプティブフォームはそのフィールドを XFA のフィールドと同期できず、これらのフィールドに対してエラーメッセージを表示します。参照先 XFA の削除の影響と dirty アダプティブフォームの詳細については、[参照先 XFA フォームの更新](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)を参照してください。

このような XFA フォームを削除するには、アダプティブフォームを更新し、XFA フィールドとの連結を削除します。
