---
title: Microsoft Dynamics OData の設定
description: ここでは、フォームデータモデルでオンラインとオンプレミスの Microsoft Dynamics サービスを使用、統合および操作する方法について説明します。
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 6c3c4d7f-fc4c-44ad-886f-f76d0532d91a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 100%

---

# Microsoft Dynamics OData の設定{#microsoft-dynamics-odata-configuration}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/ms-dynamics-odata-configuration.html?lang=ja) |
| AEM 6.5 | この記事 |

![データ統合](assets/data-integeration.png)

Microsoft Dynamics は、顧客関係管理（CRM）およびエンタープライズリソースプランニング（ERP）用のソフトウェアで、顧客のアカウント、連絡先、潜在顧客、顧客機会、顧客事例を作成して管理する企業ソリューションを提供します。[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)の OData クラウドサービス設定を使用して、オンラインおよびオンプレミスの Microsoft Dynamics サーバーの両方に Forms を統合できます。これにより、Microsoft Dynamics サービスで定義されるエンティティ、属性、サービスに基づいて、フォームデータモデルを作成できるようになります。フォームデータモデルを使用して、Microsoft Dynamics サーバーと連携するアダプティブフォームを作成することにより、ビジネスワークフローを使用できるようになります。次に例を示します。

* Microsoft Dynamics サーバーに対してクエリーを実行し、各種のデータや事前に設定されているアダプティブフォームを照会する
* アダプティブフォームの送信時に、データを Microsoft Dynamics に書き込む
* フォームデータモデル内で定義されるカスタムエンティティを使用して、データを Microsoft Dynamics に書き込む（またはその逆の動作）

AEM Forms アドオンパッケージには、Microsoft Dynamics を AEM Forms に素早く統合するのに役立つ参照 OData 設定も含まれます。

パッケージがインストールされると、AEM Forms インスタンス上で、次のエンティティとサービスを使用できるようになります。

* MS Dynamics OData クラウドサービス（OData サービス）
* Microsoft Dynamics の各種エンティティとサービスが事前設定されたフォームデータモデル。

フォームデータモデルで事前構成された Microsoft Dynamics エンティティとサービスは、AEM インスタンスの実行モードが `samplecontent`（デフォルト）に設定されている場合にのみ、AEM Forms インスタンスで使用できます。MS Dynamics OData Cloud Service（OData サービス）は、他の実行モードでも使用できます。AEM インスタンスの実行モードの設定について詳しくは、[実行モード](/help/sites-deploying/configure-runmodes.md)を参照してください。

## 前提条件 {#prerequisites}

Microsoft Dynamics のセットアップおよび設定を開始する前に、次の項目を確認する必要があります。

* [AEM Forms アドオンパッケージ](../../forms/using/installing-configuring-aem-forms-osgi.md)がインストールされている
* Microsoft Dynamics 365 がオンライン環境で設定されているか、次のいずれかの Microsoft Dynamics バージョンのインスタンスがインストールされていること。

   * オンプレミス環境の Microsoft Dynamics 365
   * オンプレミス環境の Microsoft Dynamics 2016

* [Microsoft Dynamics オンラインサービスのアプリケーションを Microsoft Azure Active Directory に登録している](https://docs.microsoft.com/ja-jp/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。登録済みサービスのクライアント ID（アプリケーション ID）とクライアントの秘密鍵の値を書き留めてください。これらの値は [Microsoft Dynamics サービス用にクラウドサービスを設定する](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)ときに使用します。

## 登録された Microsoft Dynamics アプリケーションの応答 URL の設定 {#set-reply-url-for-registered-microsoft-dynamics-application}

次の手順で、登録された Microsoft Dynamics アプリケーションの応答 URL を設定します。

>[!NOTE]
>
>この手順は、AEM Forms をオンラインの Microsoft Dynamics サーバーと統合する場合にのみ使用します。

1. Microsoft Azure Active Directory アカウントに移動し、登録済みアプリケーションの「**応答 URL**」設定に以下のクラウドサービス設定の URL を追加します。

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure ディレクトリ](assets/azure_directory_new.png)

1. 設定を保存します。

## IFD 用の Microsoft Dynamics の設定 {#configure-microsoft-dynamics-for-ifd}

外部のユーザーは、Microsoft Dynamics でクレームベース認証を使用して、Microsoft Dynamics CRM サーバー上のデータにアクセスできます。この機能を有効にするには、次の手順を実行して、インターネット接続デプロイメント（IFD）用に Microsoft Dynamics を設定し、クレーム設定を指定します。

>[!NOTE]
>
>この手順は、AEM Forms をオンプレミスの Microsoft Dynamics サーバーと統合する場合にのみ使用します。

1. 「[Configure IFD for Microsoft Dynamics](https://technet.microsoft.com/ja-jp/library/dn609803.aspx)」の説明に従い、オンプレミス環境の Microsoft Dynamics インスタンスを IFD 用に設定します。
1. Windows PowerShell を使用して以下のコマンドを実行し、IFD が有効になっている Microsoft Dynamics でクレームを設定します。

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   詳しくは、「[CRM オンプレミス（IFD）のアプリ登録](https://msdn.microsoft.com/ja-jp/library/dn531010(v=crm.7).aspx#bkmk_ifd)」を参照してください。

## AD FS マシンで OAuth クライアントを設定する {#configure-oauth-client-on-ad-fs-machine}

OAuth クライアントを Active Directory Federation Services（AD FS）マシンに登録し、AD FS マシンでアクセス権限を設定するには、以下の手順を実行します。

>[!NOTE]
>
>この手順は、AEM Forms をオンプレミスの Microsoft Dynamics サーバーと統合する場合にのみ使用します。

1. 次のコマンドを実行します。

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   各パラメーターの意味は次のとおりです。

   * `Client-ID` は、任意の GUID ジェネレーターを使用して生成できるクライアント ID です。
   * `redirect-uri` は、AEM Forms 上の Microsoft Dynamics OData クラウドサービスに対する URL です。AEM Forms パッケージと共にインストールされるデフォルトのクラウドサービスは、次の URL にデプロイされます。
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 以下のコマンドを実行して、AD FS マシン上でアクセス権を設定します。

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   各パラメーターの意味は次のとおりです。

   * `resource` は、Microsoft Dynamics の組織 URL です。

1. Microsoft Dynamics では、HTTPS プロトコルが使用されます。Forms サーバーから AD FS のエンドポイントを呼び出すには、AEM Forms が稼働しているコンピューターで `keytool` コマンドを使用して、Microsoft Dynamics のサイト証明書を Java の証明書ストアにインストールします。

## Microsoft Dynamics サービス用にクラウドサービスを設定する {#configure-cloud-service-for-your-microsoft-dynamics-service}

**MS Dynamics OData Cloud Service（OData サービス）**&#x200B;の設定は、デフォルトの OData 設定に付属しています。Odata サービスを設定して Microsoft Dynamics サービスに接続するには、以下の手順を実行します。

1. **[!UICONTROL ツール／クラウドサービス／データソース]**&#x200B;に移動し、`global` 設定フォルダーを選択します。
1. **MS Dynamics OData Cloud Service（OData サービス）**&#x200B;の設定を選択して「**[!UICONTROL プロパティ]**」を選択します。クラウドサービスの設定プロパティを表示するダイアログが開きます。

   「**認証設定**」タブで、次のように設定します。

   1. 「**サービスルート**」フィールドの値を入力します。Dynamics インスタンスの「**開発者向けリソース**」に移動し、「サービスルート」フィールドの値を表示します。例えば、https://&lt;tenant-name>/api/data/v9.1/ です。

   1. 「**クライアント ID**」（「**アプリケーション ID**」とも呼ばれます）、「**クライアントの秘密鍵**」、「**OAuth URL**」、「**更新トークン URL**」、「**アクセストークン URL**」、「**リソース**」の各フィールドのデフォルト値を、Microsoft Dynamics サービス設定の値と置き換えます。Microsoft Dynamics をフォームデータモデルで構成するには、「**リソース**」フィールドで Dynamics インスタンスの URL を指定する必要があります。サービスルート URL を使用して、Dynamics インスタンスの URL を取得します。例えば、[https://org.crm.dynamics.com](https://org.crm.dynamics.com/) です。

   1. Microsoft Dynamics の認証プロセス用の「**認証範囲**」フィールドで、「**openid**」を指定します。

   ![認証の設定](assets/dynamics_authentication_settings_new.png)

1. 「**[!UICONTROL OAuth に接続]**」をクリックします。Microsoft Dynamics のログインページにリダイレクトされます。
1. Microsoft Dynamics の資格情報を使用してログインし、クラウドサービス設定を使用して Microsoft Dynamics サービスに接続することに同意します。このサービスとクラウドサービスとの間に接続を確立する操作は 1 回だけ行います。

   クラウドサービス設定のページに切り替わります。このページには、OData の設定が正常に保存されたことを示すメッセージが表示されます。

これで、MS Dynamics OData Cloud Service（OData サービス）がクラウドサービスとして設定され、Dynamics サービスに接続されます。

## フォームデータモデルの作成 {#create-form-data-model}

AEM Forms パッケージをインストールすると、フォームデータモデルの&#x200B;** Microsoft Dynamics FDM** が AEM インスタンスにデプロイされます。デフォルトの場合、MS Dynamics OData Cloud Service（OData サービス）で定義された Microsoft Dynamics サービスが、フォームデータモデルのデータソースとして使用されます。 

初めてフォームデータモデルを開くと、設定済みの Microsoft Dynamics サービスに接続され、Microsoft Dynamics インスタンスからエンティティが取得されます。Microsoft Dynamics から取得される「連絡先」エンティティと「潜在顧客」エンティティは、フォームデータモデル内に既に追加されています。

フォームデータモデルを確認するには、**[!UICONTROL フォーム／データ統合]**&#x200B;に移動します。**Microsoft Dynamics FDM** を選択し、「**編集**」をクリックしてフォームデータモデルを編集モードで開きます。または、次の URL から直接フォームデータモデルを開くこともできます。

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

この後、フォームデータモデルに基づいてアダプティブフォームを作成し、次のようなさまざまな方法でアダプティブフォームを使用できます。

* Microsoft Dynamics のエンティティとサービスに対してクエリーを実行し、取得した情報を使用してアダプティブフォームを事前に設定する
* アダプティブフォームのルールを使用して、フォームデータモデル内で定義された Microsoft Dynamics サーバーの操作を呼び出す
* 送信されたフォームデータを Microsoft Dynamics のエンティティに書き込む

AEM Forms パッケージに付属したフォームデータモデルのコピーを作成し、要件に合わせてデータモデルとサービスを設定することをお勧めします。これにより、今後のパッケージの更新時に、フォームデータモデルが上書きされることがなくなります。

ビジネスワークフローでのフォームデータモデルの作成および使用について詳しくは、[データ統合](../../forms/using/data-integration.md)を参照してください。
