---
title: データベースの増大を最小にするためのヒント
description: 長期間有効なプロセスは、プロセスデータを AEM Forms データベースに格納します。AEM Forms データベースの増大は、いくつかの簡単なプロセスデザインと製品設定戦略を使用して最小限に抑えることができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ac3766c5-b741-4e65-8053-0c9cfd66a2f9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 93%

---

# データベースの増大を最小にするためのヒント {#tips-for-minimizing-database-growth}

長期間有効なプロセスは、プロセスデータを AEM Forms データベースに格納します。AEM Forms データベースの増大は、いくつかの簡単なプロセスデザインと製品設定戦略を使用して最小限に抑えることができます。

## プロセスデザインのヒント {#process-design-tips}

できる限り、短時間のみ有効なプロセスを使用してください。短時間のみ有効なプロセスは、プロセスデータをデータベースに格納しません。短時間のみ有効なプロセスを使用する場合の短所は、そのステータスと状態が管理コンソールで追跡されず、プロセスの履歴が残らないことです。

タスク割り当て操作（ユーザーサービス）などの一部のサービス操作は、長期間有効なプロセスで使用する必要があります。この場合、可能であれば、プロセスをいくつかのサブプロセスに区分し、それらのサブプロセスを短時間のみ有効にできます。この戦略を使用する場合、短時間のみ有効なサブプロセスで、ドキュメント値などの大きなデータ項目を処理する必要があります。

変数は慎重に使用してください。長期間有効なプロセスを使用する場合、すべてのプロセスインスタンスについて、プロセスの各変数にデータベース上の領域が割り当てられます。変数を計画して適切に使用すると、かなりの領域を節約できます。例えば、プロセスで古い値が不要になった場合は、変数値を上書きできます。また、作成済みで使用していない変数は削除してください。プロセスを検証すると、未使用の変数を見つけることができます。

単純な変数タイプ（string や int など）を使用し、できる限り複雑な変数タイプは使用しないでください。値が含まれていない場合でも、変数にはデータベース領域が割り当てられます。複雑な変数には、通常、単純な変数より多くの領域が必要になります。

## 製品管理のヒント {#product-administration-tips}

グローバルドキュメントストレージ（GDS）を、効率的に使用してください。Forms サーバー上の GDS ディレクトリは、特にプロセス内の AEM Forms に属するサービスに渡されるファイルを格納するために使用されます。パフォーマンス向上のために、小さなドキュメントは代わりにメモリ内に保持され、データベースに格納されます。

メモリ内に保持されデータベースに格納されるドキュメントの最大サイズを設定できるように、管理コンソールには「デフォルトのドキュメント最大インラインサイズ」プロパティがあります（[ 一般的なAEM Forms の設定を参照 ](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)）このプロパティを低い値に設定すると、ほとんどのドキュメントはデータベースではなく GDS ディレクトリに保持されます。 ファイルを GDS ディレクトリに保存した場合の長所は、不要になったときに簡単に削除できることです。
