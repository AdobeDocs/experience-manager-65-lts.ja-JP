---
title: AEM 6.5 Formsでの hCaptcha&reg；の使用方法
description: hCaptcha® サービスでフォームのセキュリティを容易に強化できます。ステップバイステップガイドをご用意しております。
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: da0f8fc5-732e-41de-b73c-0355ec723d26
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 27%

---

# AEM Forms環境と hCaptcha の接続® {#connect-your-forms-environment-with-hcaptcha-service}


<span class="preview"> この機能はデフォルトでは有効になっていません。 公式アドレスからaem-forms-ea@adobe.comに書き込んで、機能へのアクセスをリクエストできます。</span>

CAPTCHA（コンピュータと人間を区別する完全に自動化された公開チューリングテスト）は、人間と自動化されたプログラム／ボットを区別するために、オンライントランザクションで一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のある目的を防止することで、オンライントランザクションの安全性を高めます。

AEM Forms 6.5 では、hCaptcha® に加えて、次の CAPTCHA ソリューションもサポートしています。

* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)

## AEM Forms環境と hCaptcha の統合®

hCaptcha® サービスは、ボット、スパム、自動化された不正使用からフォームを保護します。チェックボックスウィジェットテストを行ってユーザーの反応を評価し、フォームを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットによるスパムの投稿や悪意のあるアクティビティを防止することで、オンライントランザクションの安全性を高めます。

AEM 6.5 アダプティブ Formsは、hCaptcha&amp;reg をサポートします。 これを使用して、フォーム送信時にチェックボックスウィジェットの課題を表示できます。

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### AEM Forms環境と hCaptcha を統合するための前提条件® {#prerequisite}

AEM Formsで hCaptcha® を設定するには、hCaptcha® web サイトから [hCaptcha® サイトキーと秘密鍵 ](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) を取得する必要があります。

### hCaptcha の設定® {#steps-to-configure-hcaptcha}

AEM Formsを hCaptcha® サービスと統合するには、次の手順を実行します。

1. AEM Forms環境に設定コンテナを作成します。このコンテナには、AEMを外部サービスに接続するために使用するクラウド設定が格納されます。 設定コンテナを作成するには：
   1. AEM Formsを開きます。
   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   1. 設定ブラウザーで、既存のフォルダーを選択したり、新しいフォルダーを作成したりできます。
      * 新しいフォルダーを作成し、クラウド設定を有効にするには：
         1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
         1. 設定を作成ダイアログで、名前とタイトルを指定し、「**[!UICONTROL クラウド設定]**」をオンにします。
         1. 「**[!UICONTROL 作成]**」をクリックします。
      * 既存のフォルダーに対してクラウド設定を有効にするには：
         1. 設定ブラウザーで、フォルダーを選択して「**[!UICONTROL プロパティ]**」を選択します。
         1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
         1. 「**[!UICONTROL 保存して閉じる]**」をクリックして設定を保存し、ダイアログを閉じます。

1. クラウドサービスの設定：
   1. AEM オーサーインスタンスで、![tools-1](assets/tools-1.png)/**[!UICONTROL Cloud Services]** に移動し、**[!UICONTROL hCaptcha®]** をクリックします。

      ![hCaptcha® の ui](assets/hcaptcha-in-ui.png)
   1. 前の節で説明したように、作成または更新された設定コンテナを選択します。 「**[!UICONTROL 作成]**」を選択します。

      ![ 設定 hCaptcha®](assets/config-hcaptcha.png)
   1. **[!UICONTROL タイトル]**, <!--**[!UICONTROL Name]**--> を指定 **[!UICONTROL サイトキー]**、および hCaptcha® サービスの **[!UICONTROL 秘密鍵]**&#x200B;[ 前提条件で取得 ](#prerequisite)。
   1. 「**[!UICONTROL 作成]**」をクリックします。

      ![AEM Forms環境を hCaptcha と接続するようにCloud Serviceを設定する®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > [ クライアントサイドのJavaScript検証 URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) および [ サーバーサイドの検証 URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side) は、hCaptcha® 検証用に既に入力されているので、変更する必要はありません。

   hCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。

## アダプティブフォームでの hCaptcha® の使用 {#using-hCaptcha-in-aem-6.5}

1. AEM Formsを開きます。
1. **[!UICONTROL Forms]**／**[!UICONTROL フォームとドキュメント]**&#x200B;に移動します。
1. アダプティブフォームを選択し、**[!UICONTROL プロパティ]** をクリックします。
1. **[!UICONTROL 設定コンテナ]** で、AEM Formsと hCaptcha を接続するクラウド設定を含む設定コンテナを選択します。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   Hcaptcha 用の Configuration Container がない場合、Configuration Container の作成方法については、[AEM Forms環境と hCaptcha の接続®](#configure-hcaptcha-steps-to-configure-hcaptcha) の節を参照してください。

   ![設定コンテナの選択](/help/forms/using/assets/captcha-properties.png)

1. アダプティブフォームを選択し、**[!UICONTROL 編集]** をクリックして、フォームをエディターで開きます。
1. コンポーネントブラウザーから **[!UICONTROL Captcha]** コンポーネントを、アダプティブフォームにドラッグ＆ドロップします。
1. **[!UICONTROL Captcha]** コンポーネントを選択し、プロパティ ![ プロパティアイコン ](assets/configure-icon.svg) をクリックして、プロパティダイアログを開きます。 次のプロパティを指定します。

   ![hCaptcha® v1](assets/config-hcaptcha-v1-img.png)

   * **[!UICONTROL タイトル &#x200B;]:** Captcha コンポーネントのタイトルを指定します。
   * **[!UICONTROL 検証メッセージ &#x200B;]:** フォーム送信時またはユーザーアクション時に Captcha 検証の検証メッセージを提供します。
   * **[!UICONTROL Captcha サービス &#x200B;]:** フォーム送信用の CAPTCHA サービスを選択します。ここでは、「hCaptcha®」を選択します。
   * **[!UICONTROL 設定 &#x200B;]:** hCaptcha® 用に設定したクラウド設定を選択します。

     >[!NOTE]
     >同様の目的のために、環境内に複数のクラウド設定を持つことができます。 そのため、サービスは慎重に選択してください。サービスがリストに表示されない場合は、[AEM Forms環境と hCaptcha® の接続 ](#connect-your-forms-environment-with-hcaptcha-service) を参照して、AEM Forms環境と hCaptcha® サービスを接続するCloud Serviceの作成方法を確認してください。

   * **[!UICONTROL エラーメッセージ &#x200B;]:** Captcha 送信が失敗した場合にユーザーに表示するエラーメッセージを指定します。
   * **[!UICONTROL Captcha サイズ &#x200B;]:** hCaptcha® チャレンジダイアログの表示サイズを選択できます。 **[!UICONTROL コンパクト]** オプションを使用すると小さいサイズを表示でき、**[!UICONTROL 標準]** を使用すると比較的大きいサイズの hCaptcha® チャレンジダイアログを表示できます。**[!UICONTROL 非表示]** を使用すると hCaptcha® を検証でき、ユーザーインターフェイスでチェックボックスウィジェットを明示的にレンダリングする必要はありません。

1. 「**[!UICONTROL 完了]**」を選択します。


現在は、フォームの入力者が hCaptcha® サービスによって発生する課題を正常にクリアした正当なフォームのみがフォーム送信で許可されています。

**hCaptcha® は、Intuition Machines, Inc. の登録商標です。**


## よくある質問

* **Q:1 つのアダプティブフォームで複数の Captcha コンポーネントを使用できますか？**
* **A:** アダプティブフォームでの複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込みのためにマークされたフラグメントまたはパネルで Captcha コンポーネントを使用することはお勧めしません。

## 関連トピック {#see-also}

* [アダプティブフォームの CAPTCHA の使用](/help/forms/using/captcha-adaptive-forms.md)
* [アダプティブフォームで Turnstile Captcha を使用する](/help/forms/using/integrate-adaptive-forms-turnstile.md)
