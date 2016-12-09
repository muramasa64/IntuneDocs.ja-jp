---
title: "リソース アクセス用の証明書プロファイル |Microsoft Intune"
description: "各ユーザーのデバイスにインストールされている証明書で、VPN、Wi-Fi、および電子メール アクセスを保護します。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 11/23/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 8cbb8499-611d-4217-a7b4-e9b864785dd0
ms.reviewer: kmyrup
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 35d08100b4332cc63667a401143c17972225a908
ms.openlocfilehash: b64260fd44e5c3fd0fb80e0dab4d75bd5c4eb305


---

# <a name="secure-resource-access-with-certificate-profiles-in-microsoft-intune"></a>Secure resource access with certificate profiles in Microsoft Intune (Microsoft Intune の証明書プロファイルでリソースへのアクセスを保護する)
VPN、Wi-Fi、または電子メール プロファイル経由でユーザーが企業リソースへアクセスできるようにする場合、各ユーザー デバイスにインストールされている証明書を使用してこのアクセスを保護することができます。 そのしくみは次のとおりです。

1. 「[SCEP の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-scep.md)」および「[PFX の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-pfx.md)」の説明に従って、適切な証明書インフラストラクチャを構成します。

2. 各デバイスにルート証明書または中間証明機関 (CA) 証明書をインストールして、デバイスが CA の正当性を認識できるようにします。 これを行うには、**信頼された証明書プロファイル**を作成して展開します。 このプロファイルを展開すると、Intune で管理しているデバイスがルート証明書を要求して受け取ります。 プラットフォームごとに別個のプロファイルを作成する必要があります。 **信頼された証明書プロファイル**は、次のプラットフォーム用に使用できます。
 -  iOS 8.0 以降
 -  Mac OS X 10.9 以降
 -  Android 4.0 以降
 -  Android for Work
 -  Windows 8.1 以降
 -  Windows Phone 8.1 以降

[!INCLUDE[wit_nextref](../includes/afw_rollout_disclaimer.md)]

3. 「[Intune 証明書プロファイルを構成する](configure-intune-certificate-profiles.md)」の説明に従って、デバイスが VPN、Wi-Fi、電子メールによるアクセスの認証に使用する証明書を要求するように、証明書プロファイルを作成します。 次のプラットフォームを実行するデバイスに対しては、**PKCS #12 (.PFX) 証明書プロファイル***または* **SCEP 証明書プロファイル**を作成して展開できます。

  -  iOS 8.0 以降
  -  Android 4.0 以降
  -  Android for Work
  -  Windows 10 (Desktop および Mobile) 以降

  次のプラットフォームを実行するデバイスに対しては、**SCEP 証明書プロファイル**を使用します。
    -   Mac OS X 10.9 以降
    -   Windows Phone 8。1 

プラットフォームごとに別個のプロファイルを作成する必要があります。 プロファイルを作成したら、それを既に作成済みの**信頼されたルート証明書プロファイル**に関連付けます。

> [!NOTE]           
> - エンタープライズ証明機関がない場合は、作成する必要があります。
>- デバイス プラットフォームに基づいて Simplified Certificate Enrollment Protocol (SCEP) プロファイルを使用することにした場合は、ネットワーク デバイス登録サービス (NDES) サーバーも構成する必要があります。
>-  SCEP プロファイルと .PFX プロファイルのどちらを使用する場合でも、Microsoft Intune 証明書コネクタをダウンロードして構成する必要があります。
>-  すべての必須サービスの構成方法については、「[SCEP の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-scep.md)」と「[PFX の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-pfx.md)」を参照してください。

### <a name="next-steps"></a>次のステップ
- [SCEP の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-scep.md)
- [PFX の証明書インフラストラクチャを構成する](configure-certificate-infrastructure-for-pfx.md)
- [Intune 証明書プロファイルを構成する](configure-intune-certificate-profiles.md)



<!--HONumber=Nov16_HO4-->

