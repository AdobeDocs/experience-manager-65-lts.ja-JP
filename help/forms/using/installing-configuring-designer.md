---
title: Designer のインストールと設定
description: ワークベンチにバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。スタンドアロン Designerのインストール方法を説明します。
role: Admin, User, Developer
feature: Forms Designer,Designer
solution: Experience Manager, Experience Manager Forms
exl-id: 526bbc59-62c3-4e6d-a938-e368d07fe6b0
source-git-commit: eb6f6b994fdd3b2b01e77700d2deb7bd2830ac8f
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 65%

---

# Designer のインストールと設定{#installing-and-configuring-designer}

## 前提条件 {#pre-requisites}

+++ 64 ビット版 AEM Forms Designer の場合（推奨）

* 64 ビット版の [Visual C++ 2019 再頒布可能パッケージ（x64） &#x200B;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) をインストールします。 インストールを開始する前に、前述の再頒布可能ランタイムパッケージがインストールされていることを確認してください。
* AEM Forms Designer をインストールまたはアンインストールするには、管理者権限を持っている必要があります。

+++

+++ 32 ビット版 AEM Forms Designer の場合

* 32 ビット版の [Visual C++ 2019 再頒布可能パッケージ（x64） &#x200B;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) をインストールします。 インストールを開始する前に、前述の再頒布可能ランタイムパッケージがインストールされていることを確認してください。
* AEM Forms Designer をインストールまたはアンインストールするには、管理者権限を持っている必要があります。

+++

>[!NOTE]
>
>* 64 ビット版のDesignerは、AEM 6.5 Forms サービスパック 19 で導入されました（6.5.19.0）。
>* 32 ビットバージョンのDesignerは、[AEM Forms サービスパック 21 （6.5.21.0） &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) のリリース以降、非推奨（廃止予定）となりました。
> * Forms Designer でサポートされているプラットフォームは、AEM Forms でサポートされているプラットフォームと一致します。Forms Designerでサポートされているプラットフォームについては、[&#x200B; ここをクリック &#x200B;](/help/sites-deploying/technical-requirements.md) してください。

フォーム designer のインストールに関して詳しくは、[よくある質問](#fandq)を参照してください。

## AEM Forms Designer のインストール {#install-designer}

ワークベンチにバンドルされている Designer は、スタンドアロンのインストーラーとして使用することができます。AEM Forms Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。

1. AEM Forms Designer の以前のバージョンが既にインストールされている場合は、そのバージョンをアンインストールします。
1. 要件に応じて、64 ビット版の AEM Forms Designer（推奨）または 32 ビット版の AEM Forms Designer をダウンロードします。

   >[!NOTE]
   > 
   >* 32 ビット版の Forms Designer は、AEM 6.5 Forms Service Pack 20（6.5.20.0）リリースで廃止される予定です。Adobeでは、64 ビット版のForms Designerにアップグレードすることをお勧めします。
   >* 64 ビット版の Forms Designer は、AEM 6.5 Forms Service Pack 19（6.5.19.0）以降のリリースでのみ使用できます。
   >* Adobe Experience Manager 6.5 Forms サービスパック 15（6.5.15.0）以降の Forms Designer バージョンには、サービスパックバージョンも含まれています。例えば、サービスパック 15 の場合、バージョン番号は 6.5.15.20221112.1.0 です。この例では、6.5.15 がサービスパックのバージョンです。

1. setup.exe をダブルクリックして、AEM Forms Designer のインストーラーを起動します。
1. 続行して、「パーソナライズ機能」画面で詳細とシリアル番号を入力します。

   >[!NOTE]
   >
   >* Forms Designer ライセンスキーを [Adobe ライセンス web サイト &#x200B;](https://licensing.adobe.com/) から取得します。

1. 使用許諾契約に同意する場合は、「次へ」をクリックして先に進みます。
1. （オプション）Designer を選択した場所にインストールする場合は、既定のインストールパスを変更します。「次へ」をクリックします。
1. 設定を変更するには、「戻る」をクリックします。Designer をインストールするには、「インストール」をクリックします。
1. インストールが完了したら、「完了」をクリックします。

または、コマンドラインからパッシブモードまたはサイレントモードを使用してAEM Forms Designerをインストールすることもできます。

* パッシブコマンドラインインストール：インストーラーにインストールが進行中であることを示す進行状況バーが表示されますが、プロンプトやエラーメッセージは表示されません。起動後は、インストールをキャンセルできません。

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* サイレントコマンドラインインストール：インストーラーは、ユーザーインターフェイスを表示せずにインストールを実行します。プロンプト、メッセージ、ダイアログボックスは表示されません。起動後は、インストールをキャンセルできません。

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## AEM Forms Designer の更新 {#update-forms-designer}

AEM Forms Designer 6.5.16.0 の最新バージョンの更新する場合、次の 2 つのケースがあります。

* **ケース 1**：ユーザーの AEM Forms Designer バージョンが 6.5.15.0 より前の場合。
* **ケース 2**：ユーザーの AEM Forms Designer のバージョンが 6.5.15.0 の場合。

+++**ユーザーの AEM Forms Designer のバージョンが 6.5.15.0 より前の場合。**

AEM Forms Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。

1. **AEM Forms Designer6.5.16.0** をインストールする前に、以前のバージョンをアンインストールする必要があります。
1. AEM Form のリリースページから [AEM Forms Designer6.5.15.0](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#) をダウンロードしてインストールします。
1. **AEM Forms Designer6.5.15.0** のインストールが完了したら、[AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#)をダウンロードし、ダウンロードしたインストーラーファイルをダブルクリックしてインストールします。

+++

+++**ユーザーの AEM Forms Designer のバージョンが 6.5.15.0 の場合**

AEM Forms Designer でスタンドアロンのインストーラーを使用する場合は、以下の手順を実行します。

1. [&#x200B; ソフトウェア配布ポータル &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#) から最新バージョンのAEM Forms Designerをダウンロードします。
1. ダウンロードしたインストーラーファイルをダブルクリックして、最新バージョンの AEM Forms Designer をインストールします。

+++

## よくある質問 {#fandq}

* **64 ビット Designerを直接アップグレードまたはインストールすることはできますか？**
   * はい。64 ビット Designerを直接アップグレードまたはインストールできます。 アップグレードするには、[SP19](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/Designer-Patch/sp19_x64/aemforms_designer_6_5_0_wwe_win.zip) Designerの完全なインストーラーをインストールし、その後のDesigner パッチリリースを適用します。

     >[!NOTE]
     > 64 ビット版のDesignerにアップグレードする前に、32 ビット版のDesignerが存在する場合は、まずアンインストールします。

* **ユーザーは 32 ビットと 64 ビットの両方をシステムにインストールしたままにすることができますか？**
   * いいえ。32 ビットと 64 ビットのインストールは、同じコンピューターでは動作しません。 32 ビットのDesignerまたは 64 ビットのDesignerを使用できます。

* **ユーザーが 64 ビットのDesignerと 32 ビットのDesignerのどちらにアクセスしているかを確認するにはどうすればよいですか？**
   * Forms Designer のバージョンを確認するには、次の 2 つの方法があります。

      1. Designerを開きます。
      1. **ヘルプ**/**Designerについて** をクリックして、Designerのバージョンとビット数の情報を表示します。
例えば、次の例に示すように、バージョン文字列の末尾は **64 ビット** になります。
         `6.5.21.20240522.1.161 | 64 bit`
      1. Designerを開き、左上に、製品名と 64 ビット情報を含むブランディングアイコンが表示されます。
