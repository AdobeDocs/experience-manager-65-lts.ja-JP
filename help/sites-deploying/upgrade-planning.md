---
title: アップグレードの計画
description: この記事では、AEM のアップグレードの計画で明確な目標、フェーズ、成果物を定める際に役立つ情報を示します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: ac803ef9ac38380d7ce7fdf4490c428fd0039688
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 61%

---

# アップグレードの計画 {#planning-your-upgrade}

## AEM アップグレードの概要 {#aem-upgrade-overview}

AEM は、何百万人ものユーザーにサービスを提供するような、影響の大きいデプロイメントで使用されることがよくあります。通常、インスタンスにカスタムアプリケーションがデプロイされ、さらに複雑な構成になっています。このようなデプロイメントをアップグレードするときには、入念な計画が必要です。

このガイドでは、アップグレードの計画で明確な目標、フェーズ、成果物を定める際に役立つ情報を示します。アップグレードの全体的な実行とガイドラインに焦点を当てています。 実際のアップグレード手順の概要を示しますが、入手可能な技術リソースを参照するよう指示する場合もあります。このドキュメントで参照されている入手可能な技術リソースを併せて使用してください。

AEM アップグレードプロセスでは、プランニング、分析および実行のフェーズと、各フェーズで定義される主要成果物を慎重に扱う必要があります。

>[!NOTE]
>
>AEM 6.5 LTS へのアップグレードは、最新の 6 つのサービスパックからサポートされています

サポート対象のオペレーティングシステム、Java™ ランタイム、httpd および Dispatcher バージョンを実行していることを確認することが重要です。詳しくは、[AEM 6.5 LTS の技術要件 ](/help/sites-deploying/technical-requirements.md) を参照してください。 これらのコンポーネントのアップグレードは、アップグレード計画で考慮する必要があり、AEMのアップグレード前に行う必要があります。

<!-- Alexandru: drafting for now

## Upgrade Scope and Requirements {#upgrade-scope-requirements}

Below you will find a list of areas that are impacted in a typical AEM Upgrade project:

<table>
 <tbody>
  <tr>
   <td><strong>Component</strong></td>
   <td><strong>Impact</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Operating System</td>
   <td>Uncertain, but subtle effects</td>
   <td>At the time of the AEM upgrade, it may be time to upgrade the operating system as well and this might have some impact.</td>
  </tr>
  <tr>
   <td>Java&trade; Runtime</td>
   <td>Moderate Impact</td>
   <td>AEM 6.3 requires JRE 1.7.x (64 bit) or later. JRE 1.8 is the only version currently supported by Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Moderate Impact</td>
   <td>Online Revision Cleanup requires free<br /> disk space equal to 25% of the repository's size and 15% free heap space<br /> to complete successfully. You may need to upgrade your hardware to<br /> ensure sufficient resources for Online Revision Cleanup to fully<br /> run. Also, if upgrading from a version prior to AEM 6, there<br /> may be additional storage requirements.</td>
  </tr>
  <tr>
   <td>Content Repository (CRX or Oak)</td>
   <td>High Impact</td>
   <td>Starting from version 6.1, AEM does not support CRX2, so a migration to<br /> Oak (CRX3) is required if upgrading from an older version. AEM 6.3 has<br /> implemented a new Segment Node Store that also requires a migration. The<br /> crx2oak tool is used for this purpose.</td>
  </tr>
  <tr>
   <td>AEM Components/Content</td>
   <td>Moderate Impact</td>
   <td><code>/libs</code> and <code>/apps</code> are easily handled through the upgrade, but <code>/etc</code> usually requires some manual reapplication of customizations.</td>
  </tr>
  <tr>
   <td>AEM Services</td>
   <td>Low Impact</td>
   <td>Most AEM core services are tested for upgrade. This is an area of low impact.</td>
  </tr>
  <tr>
   <td>Custom Application Services</td>
   <td>Low to High Impact</td>
   <td>Depending on the application and customization, there may be<br /> dependencies on JVM, operating system versions, and some indexing related<br /> changes, as indexes are not generated automatically in Oak.</td>
  </tr>
  <tr>
   <td>Custom Application Content</td>
   <td>Low to High Impact</td>
   <td>Content that will not be handled through the upgrade can be backed up<br /> before the upgrade takes place and then moved back into the repository.<br /> Most content can be handled through the migration tool.</td>
  </tr>
 </tbody>
</table>

It is important to ensure that you are running a supported operating system, Java&trade; runtime, httpd, and Dispatcher version. For more information, see the [AEM 6.5 Technical Requirements page](/help/sites-deploying/technical-requirements.md). Upgrading these components must be accounted for in your project plan and should take place before upgrading AEM. -->

## アップグレードの段階 {#upgrade-phases}

AEM のアップグレードの計画と実行には、多くの作業が必要になります。このプロセスに含まれる様々な作業を明確にするために、計画と実行に伴う作業を個別のフェーズに分割しました。以下の節では、各フェーズで成果物を作成します。成果物は、アップグレードの将来のフェーズでよく使用されます。

<!-- Alexandru:drafting for now

### Planning for Author Training {#planning-for-author-training}

With any new release, there are potential changes to the UI and user workflows that may be introduced. Also, new releases introduce new features that may be beneficial for the business to use. Adobe recommends reviewing the functional changes that have been introduced and organizing a plan to train your users on using them effectively.

![unu_cropped](assets/unu_cropped.png)

New features in AEM 6.5 can be found in [the AEM section of adobe.com](/help/release-notes/release-notes.md). Make sure to note any changes to UIs or product features that are commonly used in your organization. As you look through the new features, also take note of any that can be of value to your organization. After looking through what has changed in AEM 6.5, develop a training plan for your authors. This could involve using freely available resources like the help feature videos or formal training offered through [Adobe Digital Learning Services](https://learning.adobe.com/). -->

### テスト計画の作成 {#creating-a-test-plan}

顧客の AEM の実装はそれぞれ固有のものであり、ビジネス要件に合うようにカスタマイズされています。そのため、テスト計画に組み込むことができるように、システムに加えられたすべてのカスタマイズを決定することが重要です。

すべてのアプリケーションとカスタムコードが引き続き想定どおりに動作することを確認するには、実稼動環境を正確に複製し、アップグレード後にその環境でテストを実行する必要があります。すべてのカスタマイズを元に戻し、パフォーマンス、負荷およびセキュリティのテストを実行します。テスト計画を立てるときは、日々の運用で使用されている標準の UI およびワークフローに加えて、システムに対して行われたすべてのカスタマイズを対象にします。これには、カスタム OSGI サービスとサーブレット、Adobe Experience Cloud への統合、AEM コネクタによるサードパーティとの統合、サードパーティとのカスタム統合、カスタムコンポーネントとテンプレート、AEM でのカスタム UI オーバーレイ、およびカスタムワークフローが含まれる場合があります。さらに、カスタムクエリをテストして、アップグレード後もインデックスが引き続き効果的に機能していることを確認する必要があります。

### アップグレードの複雑性の評価 {#assessing-upgrade-complexity}

Adobeのお客様がAEM環境に適用するカスタマイズの量と性質には様々な種類があるので、アップグレードで期待される全体的な作業レベルを判断するには、事前にしばらく時間を置くことが重要です。 [AEM 6.5 LTS](/help/sites-deploying/pattern-detector.md) 用AEM アナライザーは、アップグレードの複雑さを評価するのに役立ちます。

AEM 6.5 LTS 用の [AEM アナライザーは ](/help/sites-deploying/pattern-detector.md) ほとんどの場合、アップグレード中に予想される作業について、かなり正確な予測を提供します。 ただし、互換性のない変更点が存在する、より複雑なカスタマイズやデプロイメントの場合は、[ インプレースアップグレードの実行 ](/help/sites-deploying/in-place-upgrade.md) の手順に従い開発インスタンスをAEM 6.5 LTS にアップグレードできます。 完了したら、この環境で全体的なスモークテストを実行します。この演習の目的は、テストケースのインベントリを完全に作成し、欠陥の正式なインベントリを作成することではなく、AEM 6.5 LTS 互換のコードをアップグレードするために必要な作業量の概算を提供することです。 [AEM アナライザー ](/help/sites-deploying/pattern-detector.md) および前の節で決定したアーキテクチャの変更と組み合わせると、アップグレードを計画するプロジェクト管理チームに、大まかな見積もりを提供できます。

### アップグレードおよびロールバックのランブックの作成 {#building-the-upgrade-and-rollback-runbook}

アドビは AEM インスタンスをアップグレードするためのプロセスを文書化していますが、それぞれの顧客のネットワークレイアウト、デプロイメントアーキテクチャおよびカスタマイズに合わせて、このアプローチの調整が必要になります。このため、Adobeでは、提供されているすべてのドキュメントを確認し、環境で実行する特定のアップグレードおよびロールバック手順の概要を説明したアップグレード固有の Runbook を提供するために使用することをお勧めします。

<!--Alexandru:drafting for now

![runbook-diagram](assets/runbook-diagram.png) -->

アップグレードおよびロールバック手順については[アップグレード手順](/help/sites-deploying/upgrade-procedure.md)で、アップグレードを適用するためのステップごとの手順については[インプレースアップグレードの実行](/help/sites-deploying/in-place-upgrade.md)で説明しています。これらの手順を確認し、システムアーキテクチャ、カスタマイズおよびダウンタイム許容度とともに考慮して、アップグレード時に実行する適切な切り替え手順およびロールバック手順を決定する必要があります。カスタマイズした Runbook を作成する際には、アーキテクチャやサーバーのサイズに関する変更を含める必要があります。

### アップグレードプランの作成 {#developing-an-upgrade-plan}

前の演習で得られた結果は、テストや開発作業に必要な予想タイムラインや実際のアップグレードの実行に対応するアップグレード計画の作成に使用できます。

<!--Alexandru: drafting for now

![develop-project-plan](assets/develop-project-plan.png) -->

包括的なプロジェクト計画には、以下が含まれています。

* 開発計画およびテスト計画の確定
* 開発環境および QA 環境のアップグレード
* AEM 6.5 LTS のカスタムコードベースの更新
* QA テストおよび修正サイクル
* ステージング環境のアップグレード
* 統合、パフォーマンスおよび負荷テスト
* 環境認定
* 実稼動

### 開発および QA の実行 {#performing-development-and-qa}

Adobeには、AEM 6.5 LTS との互換性を保つため、[ コードとカスタマイズのアップグレード ](/help/sites-deploying/upgrading-code-and-customizations.md) 手順が用意されています。 この反復プロセスを実行する際は、必要に応じて Runbook を変更する必要があります。

<!--Alexandru: drafting for now

![patru_cropped](assets/patru_cropped.png) -->

通常、開発とテストのプロセスは繰り返されます。アップグレードプロセスの調整が必要な問題が見つかった場合は、それをカスタムアップグレードランブックに追加してください。テストと修正を何回か繰り返すと、コードベースは完全に検証され、ステージング環境へのデプロイメントの準備が整います。

### 最終テスト {#final-testing}

アドビでは、コードベースが組織の QA チームによって認定された後に、最後のテストを実施することをお勧めします。このテストには、ステージング環境でのランブックの検証と、それに続くユーザー受け入れ、パフォーマンスおよびセキュリティのテストが含まれます。

<!--Alexandru: drafting for now

![cinci_cropped](assets/cinci_cropped.png) -->

この手順は、ランブックの手順を実稼動に近い環境で検証できる唯一の機会なので重要です。環境がアップグレードされたら、エンドユーザーがログインし、日常業務でシステムを使用する際のアクティビティを一通り行う時間を設けることが重要です。運用開始前にこれらの領域の問題を見つけて修正すると、コストのかかる実稼動の停止を防ぐのに役立ちます。

### アップグレードの実行 {#performing-the-upgrade}

すべての関係者から最終承認を受けたら、定義されたランブック手順に基づいて実行します。アップグレードおよびロールバックの手順は[アップグレード手順](/help/sites-deploying/upgrade-procedure.md)で、インストール手順は[インプレースアップグレードの実行](/help/sites-deploying/in-place-upgrade.md)を参照してください。

![perform-upgrade](assets/perform-upgrade.png)

アップグレード手順では、環境を検証するためのいくつかの手順が提供されています。これらの手順には、アップグレードログの調査やすべての OSGi バンドルが正しく起動することの確認のような基本的なチェックが含まれていますが、ビジネスプロセスに基づいて独自のテストケースを検証することもお勧めします。また、AEM のオンラインリビジョンクリーンアップおよび関連する定期的な作業のスケジュールをチェックして、それらが処理の少ない時間帯に実行されることを確認することもお勧めします。これらの定期的な作業は、AEM の長期的なパフォーマンスにとって重要です。
