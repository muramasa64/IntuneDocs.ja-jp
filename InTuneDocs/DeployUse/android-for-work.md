---
title: "Android for Work の概要 | Microsoft Intune"
description: "Intune は Android for Work を管理し、ユーザーが仕事に Android デバイスを使用するときに追加の管理機能とプライバシーを提供します。"
keywords: 
author: nathbarn
manager: angrobe
ms.date: 11/29/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: aa0002d9-f5a0-466e-98ac-3970cb77e3a2
translationtype: Human Translation
ms.sourcegitcommit: 83914246bde673b188ca3f7d9cf50b4d0de2edd4
ms.openlocfilehash: 127db326fc96625c719b8136964bae014a904b3d


---

# <a name="manage-android-for-work-devices-with-intune"></a>Intune で Android for Work デバイスを管理する

Android for Work は、Android デバイスの機能とサービスのセットです。 これらの機能とサービスは、ユーザーが仕事に Android デバイスを使用するときに追加の管理機能とプライバシーを提供します。 Intune を使用すると、アプリと会社のリソースを Android for Work デバイスに展開し、仕事の情報と個人の情報を分けることができます。 展開に成功すると、ユーザーがアクセスするアプリとデータは、デバイス上の Android for Work 環境内にのみ存在します。

[!INCLUDE[wit_nextref](../includes/afw_rollout_disclaimer.md)]

## <a name="supported-devices"></a>サポートされるデバイス

Android for Work を使用するには新しい Android ハードウェアが必要です。これは、多くの管理機能が、新しい Android オペレーティング システムに含まれる機能に依存しているためです。 現在、Android for Work は、Android 5.0 Lollipop 以降を実行し、仕事用プロファイルをサポートしているデバイスでサポートされています。 Android for Work をネイティブでサポートしていないデバイスの場合、従来の Android 管理を使用できます。 詳細については、「[Android for Work requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)」(Android for Work の要件) を参照してください。

## <a name="onboarding"></a>オンボード

Android for Work デバイスを登録する前に、いくつかのオンボード手順を完了する必要があります。 この手順で、Intune テナントと Google Play for Work サービス間に接続を確立します。この接続は、Android for Work アプリの配布と管理プロセスに不可欠な要素です。 詳細については、「[Android for Work デバイスの登録を有効にする](https://docs.microsoft.com/en-us/intune/deploy-use/set-up-android-for-work)」を参照してください。

## <a name="work-profile-management"></a>仕事用プロファイルの管理

Intune で Android for Work デバイスを管理する場合、デバイス全体は管理しません。 管理機能は、登録時に作成された仕事用プロファイルにのみ影響があります。 Intune でデバイスに展開されるすべてのアプリは、仕事用プロファイルに含まれます。 仕事用プロファイルのアプリのアイコンには、オレンジ色のブリーフケースが表示されます。 このマークで、デバイス上の会社のアプリと個人のアプリが区別されます。 デバイスの Android for Work に含まれないすべての Android アプリとデータは個人用であり、エンド ユーザーが管理します。 ユーザーはデバイスの個人用の側に任意のアプリをインストールできます。一方、管理者は仕事用プロファイルの対象となる操作を管理および監視できます。

## <a name="app-publishing-and-distribution"></a>アプリの発行と配布

Google Play for Work サービスは、アプリの配布と管理に不可欠な要素です。 仕事用プロファイルで Android for Work デバイスに展開されるすべてのアプリは、Play for Work から取得されます。 Play ストアでアプリを管理および展開するには、Intune 管理者として Play for Work Web サイトにログインし、Intune テナントのアプリを承認します。 これらのアプリは Intune コンソールと同期されます。Intune コンソールでは、Intune を使用してアプリの展開と管理を行うことができます。 組織が開発した基幹業務 (LOB) アプリは、Google の Android アプリ公開コンソールを使用して Play for Work に公開する必要があります。 基幹業務アプリは、Android アプリ公開コンソールで組織にアクセスを限定するように構成する必要があります。

アプリは、ユーザー操作なしでインストールされます。また、ユーザーが**不明なソースからのインストール**を許可する必要もありません。 オプションまたは使用可能なアプリを参照およびインストールするには、デバイスで仕事用の印が付いた Play ストア アプリを使用します。 詳細については、「[Intune を使用してアプリを Android for Work デバイスを展開する方法](https://docs.microsoft.com/en-us/intune/deploy-use/android-for-work-apps)」を参照してください。

## <a name="app-configuration"></a>アプリの構成

Android for Work には、アプリの構成値を、そのアプリをサポートするアプリに展開するインフラストラクチャがあります。 仕事用アプリの構成値を指定することで、ユーザーが初めてそのアプリを起動するときに構成値を正しく設定することができます。 アプリ構成をサポートするには、管理されている構成値をサポートする Android アプリをアプリ開発者が作成する必要があります。 そうすると、Intune を使用して、構成設定を指定および適用できるようになります。 詳細については、「[Android for Work app configuration settings](afw-app-configuration-policy.md)」(Android for Work アプリの構成設定) を参照してください。

## <a name="email-configuration"></a>電子メールの構成

Android for Work には、iOS で提供されているような既定の電子メール アプリまたはネイティブの電子メール プロファイル オブジェクトはありません。 その代わり、サポートする電子メール アプリにアプリ構成設定を適用することで、電子メール構成を設定できます。 Play ストアにある Gmail と Nine Work は、Android for Work アプリ構成による構成をサポートする 2 つの Exchange ActiveSync (EAS) クライアント アプリです。

Intune には、Gmail アプリと Nine Work アプリ用の構成テンプレートがあります。 アプリ構成プロファイルをサポートするその他の電子メール アプリは、モバイル アプリ構成ポリシーを使用して構成することができます。

Android for Work デバイスで EAS の条件付きアクセスを使用している場合、Gmail または Nine Work 電子メール アプリを使用する必要があります。 Android アプリ用 Microsoft Outlook、または ADAL 経由の新しい認証方法を使用する他の電子メール アプリもサポートされます。 詳細については、「[Microsoft Intune で電子メール プロファイルを使用して会社の電子メールへのアクセスを構成にする](configure-access-to-corporate-email-using-email-profiles-with-microsoft-intune.md)」を参照してください。

## <a name="mobile-app-management-policies"></a>モバイル アプリ管理ポリシー

モバイル アプリケーション管理 (MAM) に対応するアプリに適用される制限ポリシーは、仕事用プロファイルと個人用プロファイルで完全にサポートされます。 Android アプリ公開コンソール (https://play.google.com/apps/publish) で基幹業務アプリを公開できます。 このコンソールには、アプリを組織にのみ制限するオプションもあります。 詳細については、[コンプライアンス ポリシーの設定](afw-compliance-policy-settings-in-microsoft-intune.md)に関するページを参照してください。 詳細については、[モバイル アプリの管理ポリシー](protect-app-data-using-mobile-app-management-policies-with-microsoft-intune.md)に関するページを参照してください。

## <a name="vpn-profiles"></a>VPN プロファイル

VPN のサポートは、Android VPN プロファイルに似ています。 同じ VPN プロバイダーと基本的な構成オプションを使用できます。 主に 2 つの違いがあります。

1.  **仕事用プロファイル対象の VPN** - VPN 接続は、仕事用プロファイルに展開されるアプリのみが対象です。 Android for Work で管理されるアプリのみが VPN 接続を使用できます。 デバイス上の個人用のアプリは、管理対象の VPN 接続を使用できません。

2.  **アプリ固有の VPN** - VPN プロバイダーがアプリ固有の VPN の構成をサポートし、Android for Work アプリ構成プロファイルを介してアプリごとの VPN を構成する互換性がある場合、Intune でアプリ固有の VPN を構成できます。 この機能をサポートしているかどうかについては、VPN プロバイダーに問い合わせてください。 詳細については、[VPN 接続プロファイル](vpn-connections-in-microsoft-intune.md)に関するページを参照してください。

## <a name="certificate-profiles"></a>証明書プロファイル

従来の Android 管理で使用できるものと同じ証明書プロファイルの構成オプションが、Android for Work デバイスで使用できます。 Android for Work には、強化された証明書管理 API があります。 強化された証明書管理には、次の機能があります。

1.  ユーザーにとって、証明書の展開が自動的かつシームレスに実行されます。

2.  デバイスが Intune のインベントリから削除され、仕事用プロファイルが削除されるときに、展開された証明書が完全に削除されます。

3.  IT 部門が管理サービスを介して証明書を展開し、構成したことをユーザーに伝えるメッセージ処理が改善されます。

詳細については、「[Microsoft Intune の証明書プロファイルでリソースへのアクセスを保護する](secure-resource-access-with-certificate-profiles.md)」を参照してください。

## <a name="wi-fi-profiles"></a>Wi-Fi プロファイル

デバイスが Intune のインベントリから削除され、仕事用プロファイルが削除されると、Android for Work が管理する Wi-Fi プロファイルは確実に削除されます。 詳細については、「[デバイスを構成すると、会社の Wi-Fi ネットワークに接続できます](wi-fi-connections-in-microsoft-intune.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
[Android for Work デバイスの登録を有効にする](https://docs.microsoft.com/en-us/intune/deploy-use/set-up-android-for-work)
[Intune を使用してアプリを Android for Work デバイスを展開する方法](https://docs.microsoft.com/en-us/intune/deploy-use/android-for-work-apps)



<!--HONumber=Nov16_HO5-->

