---
title: Microsoft Intune とは
description: Microsoft Intune が Enterprise Mobility + Security ソリューションのモバイル デバイス管理 (MDM) とモバイル アプリ管理 (MAM) コンポーネントとしてどのように機能するか、およびそれが会社のデータを保護するしくみについて説明します。
keywords: Intune の概要
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 02/26/2019
ms.topic: overview
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b4e778d-ac13-4c23-974f-5122f74626bc
ms.reviewer: pmay
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 511e672193ec609f817c10572c99ac73831c54ae
ms.sourcegitcommit: 25e6aa3bfce58ce8d9f8c054bc338cc3dff4a78b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57460582"
---
# <a name="what-is-microsoft-intune"></a>Microsoft Intune とは

[!INCLUDE [both-portals](./includes/note-for-both-portals.md)]

Microsoft Intune はエンタープライズ モビリティ管理 (EMM) スペースのクラウドベース サービスであり、会社のデータを守りながら、社員に生産的に働いてもらうことができます。 他の Azure サービスと同様に、Microsoft Intune は Azure Portal で使用できます。 Intune では次のことができます。
* 社員が会社のデータにアクセスするために利用するモバイル デバイスと PC を管理します。
* 社員が利用するモバイル アプリを管理します。
* 社員が会社の情報にアクセスし、共有する方法を制御し、会社の情報を保護します。
* デバイスやアプリが会社のセキュリティ要件に準拠するように管理します。

## <a name="common-business-problems-that-intune-helps-solve"></a>Intune が解決に役立つ一般的なビジネス問題

* [モバイル デバイスでアクセスできるようにオンプレミスの電子メールとデータを保護する](common-scenarios.md#protecting-your-on-premises-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices)
* [モバイル デバイスで安全にアクセスできるように Office 365 の電子メールとデータを保護する](common-scenarios.md#protecting-your-office-365-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices)
* [社員向けに企業所有の携帯電話を用意する](common-scenarios.md#issue-corporate-owned-phones-to-your-employees)
* [すべての従業員に "Bring your own device" (BYOD) プログラムという個人デバイス プログラムを提供する](common-scenarios.md#offer-a-bring-your-own-device-program-to-all-employees)
* [公共の場所から Office 365 に安全にアクセスできるようにする](common-scenarios.md#enable-your-employees-to-securely-access-office-365-from-an-unmanaged-public-kiosk)
* [タスク ワーカー向けに制限付きの共有タブレットを用意する](common-scenarios.md#issue-limited-use-shared-tablets-to-your-employees)


## <a name="how-does-intune-work"></a>Intune のしくみ
Microsoft Intune は Enterprise Mobility + Security (EMS) スイートに含まれ、モバイル デバイスとモバイル アプリを管理します。 ID とアクセス制御のために Azure Active Directory (Azure AD) のような他の EMS コンポーネントと、データ保護のために Azure Information Protection と密接に統合されます。 Office 365 との連携で、社員はあらゆるデバイスを生産的に活用し、同時に会社の情報を保護することができます。

![Intune アーキテクチャのイメージ](./media/intunearch_sm.png)

[ここ](./media/intunearchitecture.svg)をクリックすると、Intune アーキテクチャ ダイアグラムが大きな画像で表示されます。

Intune のデバイス/アプリ管理機能と EMS データ保護の利用方法は、[解決しようとしているビジネス上の問題](#common-business-problems-that-intune-helps-solve)によって異なります。 次に例を示します。
* 小売店の交代勤務従業員に共有させる一時使用デバイスのプールを作成する場合、デバイス管理をかなり利用することになります。
* 個人のデバイスで企業データにアクセスすること (BYOD) を社員に許可する場合、アプリ管理とデータ保護に頼ります。  
* 情報作業者に会社の電話を与える場合、この技術のすべてに依存します。

## <a name="intune-device-management-explained"></a>Intune デバイス管理の説明
Intune デバイス管理は、モバイル オペレーティング システムで利用できるプロトコルまたは API を利用して動作します。 含まれるタスク:
* デバイスを登録して管理し、企業サービスにアクセスしているデバイスの目録を IT 部署に与える
* 会社のセキュリティ/健全性基準を満たすようにデバイスを構成する
* 企業サービスにアクセスするための証明書と Wi-Fi/VPN プロファイルを提供する
* 企業基準に対するデバイスの準拠状況を測定し、報告する
* マネージド デバイスから会社のデータを削除する  

**企業データのアクセス制御**はデバイス管理機能であると考える人がいます。 Microsoft の考え方は違います。それはモバイル オペレーティング システムが提供する機能ではないからです。 それはむしろ、ID プロバイダーが提供するサービスです。 この場合、ID プロバイダーは、Microsoft の ID/アクセス管理システムである、Azure Active Directory (Azure AD) です。  

Intune は Azure AD と連携し、さまざまなアクセス制御シナリオを可能にします。 たとえば、Exchange のような企業サービスにデバイスでアクセスするには、モバイル デバイスが企業基準に準拠する必要があるように Intune に設定できます。 同様に、特定のモバイル アプリに企業サービスを制限できます。 たとえば、Exchange Online へのアクセスを Outlook または Outlook Mobile だけに制限できます。

## <a name="intune-app-management-explained"></a>Intune アプリ管理の説明
アプリの管理とは、次のようにまとめられます。
* モバイル アプリを従業員に割り当てる
* アプリ実行時に利用される標準設定でアプリを構成する
* モバイル アプリによる企業データの使用と共有を制御する
* モバイル アプリから会社のデータを削除する   
* アプリを更新する
* モバイル アプリ インベントリについて報告する
* モバイル アプリの使用状況を追跡する

モバイル アプリ管理 (MAM) という用語は、上記のいずれかを表す言葉として、または特定の組み合わせを表す言葉として使用されています。 特に、アプリ構成の概念とモバイル アプリ内の企業データのセキュリティ保護の概念が一般的に混同されます。 一部のモバイル アプリで、データ セキュリティ機能の構成を許可する設定が露出するためです。

アプリ構成や Intune について話すとき、具体的には、[iOS の管理対象アプリ構成](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html)などの技術について言及します。

EMS の他のサービスと共に Intune を使用すると、モバイルオペレーティング システムとモバイル アプリ自体がアプリ構成を介して提供するセキュリティに加え、組織のモバイル アプリ セキュリティを提供できます。 EMS で管理されるアプリには、次のようなさまざまなモバイル アプリへのアクセス機能とデータ保護機能が与えられます。

* [シングル サインオン](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)  
*   [多要素認証](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication)
* [アプリの条件付きアクセス (モバイル アプリに企業データが含まれる場合、アクセスを許可する)](app-based-conditional-access-intune.md)
* [同じアプリ内で企業データと個人データを分離する](app-protection-policy.md)
* [アプリの保護ポリシー (PIN、暗号化、名前を付けて保存、クリップボードなど)](app-protection-policies.md)
* [モバイル アプリから企業データを消去する](apps-selective-wipe.md)
* [Rights Management の保護](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

![アプリ管理データ セキュリティのレベルを示す画像](./media/managing-mobile-apps.png)

### <a name="intune-app-security"></a>Intune アプリ セキュリティ
アプリ セキュリティの提供はアプリ管理の一部です。Intune では、モバイル アプリ セキュリティは次のような意味になります。
* 企業の IT 認識と個人情報を分離すること
* コピー、切り取り/貼り付け、保存、表示など、企業情報に対してユーザーが行う操作を制限すること
* モバイル アプリから企業データを削除すること (選択的なワイプや企業ワイプとも呼ばれています)

Intune がモバイル アプリにセキュリティを提供する方法の 1 つには、**アプリの保護ポリシー**機能があります。 アプリの保護ポリシーでは、Azure AD ID を利用し、個人データと企業データが分離されます。 企業の資格情報を利用してアクセスされるデータには、企業の保護が追加されます。

たとえば、ユーザーが会社の自分の資格情報でデバイスにログオンすると、そのユーザーの企業 ID により、自分の個人 ID では拒否されるデータにアクセスできます。 その企業データが使用されるため、アプリ保護ポリシーにより保存方法と共有方法が制御されます。 ユーザーが自分のデバイスに自分の個人 ID でログオンしたときにアクセスできるデータには同じ保護機能は適用されません。 このように、IT 部署が企業データを管理し、エンド ユーザーが自分自身のデータを管理しプライバシーを保護します。

## <a name="emm-with-and-without-device-enrollment"></a>デバイス登録あり/なしの EMM
ほとんどの企業向けモバイル管理ソリューションで、基本的なモバイル デバイス技術とモバイル アプリ技術に対応しています。 そのようなソリューションは、通常、組織のモバイル デバイス管理 (MDM) ソリューションに登録されているデバイスに関連します。 Intune はこれらのシナリオをサポートし、さらに、多くの “登録なし” シナリオに対応しています。  

組織が “登録なし” シナリオを採用する程度はさまざまです。 それを標準とする組織もあります。 個人のタブレットなど、コンパニオン デバイスでそれを許可する組織もあります。 まったくサポートしない組織もあります。 まったくサポートせず、従業員のすべてのデバイスに MDM 登録が要求される場合でも、通常、コントラクター、ベンダー、特定の例外があるその他のデバイスには、"登録なし" シナリオがサポートされます。

登録済みデバイスでも Intune の “登録なし” 技術を利用できます。 たとえば、MDM に登録されているデバイスには、モバイル オペレーティング システムにより "オープンイン" 保護が与えられていることがあります。 (オープンイン保護とは、両アプリが同じ MDM プロバイダーによって管理されている場合を除き、Outlook などのアプリから Word などの別のアプリでドキュメントを開くことを制限する Apple の iOS の機能です。) さらに、IT 部署がアプリの保護ポリシーを EMS で管理されるモバイル アプリにも適用し、名前を付けて保存を制御したり、多要素認証を提供したりすることがあります。

組織がモバイル デバイスやモバイル アプリを登録する場合でも登録しない場合でも、Intune は、EMS の一部として、社員の生産性を強化し、同時に企業データを保護するためのツールを提供します。

## <a name="microsoft-intune-in-the-azure-portal"></a>Azure Portal の Microsoft Intune

[Azure Portal](https://portal.azure.com) は、Microsoft Intune サービスのある場所です。

Azure Portal での Microsoft Intune のエクスペリエンスの概要を以下に示します。

- すべての Enterprise Mobility + Security (EMS) コンポーネント用の統合コンソール
- Web 標準に基づく HTML ベースのコンソール
- 多数のアクションを自動化するために Microsoft Graph API をサポート
- Azure Active Directory (AD) グループによってすべての Azure アプリケーション間での互換性を提供
- 最新の Web ブラウザーの大部分に対応

ポータルのエクスペリエンスをカスタマイズするクイック ガイドについては、「[Azure Portal で Intune を始める](get-started-azure.md)」を参照してください。

> [!NOTE]
> 以前のバージョンの Microsoft Intune を使用している場合は、次の情報が役立ちます。
> * [Azure での Intune の機能の移動先](ui-changes.md)は、Azure への移行で変更された特定のワークフローと UI を示すリファレンスです。
> * [Azure Portal での Intune クラシック グループ](groups-get-started.md)は、グループを管理するための Azure Active Directory セキュリティ グループへの切り替えの影響について説明します。

### <a name="before-you-start"></a>開始する前に

Azure Portal で Intune を使用するには、Intune の管理者およびテナント アカウントが必要です。 まだお持ちでない場合は、[アカウントにサインアップ](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)してください。

### <a name="supported-web-browsers-for-the-azure-portal"></a>Azure Portal でサポートされている Web ブラウザー

Azure Portal は、ほとんどの最新 PC、Mac、タブレットで動作します。 携帯電話はサポート対象外です。
現時点では、以下のブラウザーがサポートされています。

- Microsoft Edge (最新バージョン)
- Microsoft Internet Explorer 11
- Safari (最新バージョン、Mac のみ)
- Chrome (最新バージョン)
- Firefox (最新バージョン)

サポート対象のブラウザーに関する最新情報については、[Azure Portal に関するページ](https://docs.microsoft.com/azure/azure-preview-portal-supported-browsers-devices)を参照してください。

## <a name="next-steps"></a>次の手順
* [Intune の一般的な使用方法](common-scenarios.md)を読む
* [Intune の 30 日間の評価版](free-trial-sign-up.md)を使用して製品の理解を深める
* Intune の[技術的要件と機能](supported-devices-browsers.md)を調べる
