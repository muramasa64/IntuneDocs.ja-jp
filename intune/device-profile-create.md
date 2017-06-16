---
title: "Intune デバイス構成プロファイルを作成する | Intune Azure プレビュー"
titleSuffix: Intune Azure preview
description: "Intune Azure プレビュー: Intune デバイス構成プロファイルを作成する方法について説明します。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: a719b3f53076a55f1e888a9ddf8e98c7074dd25f
ms.contentlocale: ja-jp
ms.lasthandoff: 05/23/2017


---

# <a name="how-to-create-device-configuration-profiles-in-microsoft-intune"></a>Microsoft Intune でデバイス構成プロファイルを作成する方法

[!INCLUDE[azure_preview](./includes/azure_preview.md)]


1. Azure ポータルにサインインします。
2. **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[デバイスの構成]** を選択します。
2. **[デバイス構成]** ブレードで、**[管理]** > **[プロファイル]** の順に選択します。
2. プロファイルの一覧が表示されているブレードで、**[プロファイルを作成します]** を選択します。
3. **[プロファイルを作成します]** ブレードで、次を指定します。
    - **[名前]** - 新しいプロファイルのわかりやすい名前を入力します。
    - **[説明]** - プロファイルの説明を入力します (省略可能)。
    - **[プラットフォーム]** - 作成するプロファイルのプラットフォームの種類を選択します。
    - **[プロファイルの種類]** - 作成するプロファイルの種類を選択します。 選択可能な種類の一覧は、選択したプラットフォームによって異なります。
    - **[設定]** - プロファイルの種類ごとの設定に関する情報については、次のトピックを参照してください。
        -  [デバイス機能設定](device-features-configure.md)
        -  [デバイスの制限設定](device-restrictions-configure.md)
        -  [電子メールの設定](email-settings-configure.md)
        -  [VPN 設定](vpn-settings-configure.md)
        -  [Wi-Fi 設定](wi-fi-settings-configure.md)
        -  [Windows 10 エディションのアップグレード設定](edition-upgrade-configure-windows-10.md)
        -  [証明書の設定](certificates-configure.md)
        -  [Windows 情報保護の設定](windows-information-protection-configure.md)
        -  [教育設定](education-settings-configure.md)
        -  [カスタム設定](custom-settings-configure.md)

    ![デバイス プロファイルの作成](./media/create-device-profile.png)
4. 設定の構成が完了したら、**[プロファイルを作成します]** ブレードで、**[作成]** を選択します。

プロファイルが作成され、プロファイルの一覧ブレードに表示されます。
このプロファイルをグループに割り当てる場合は、[デバイス プロファイルを割り当てる方法](device-profile-assign.md)に関する記事を参照してください。


### <a name="next-steps"></a>次のステップ
デバイス プロファイルを割り当てる方法については、[Microsoft Intune でデバイス プロファイルを割り当てる方法](device-profile-assign.md)に関する記事を参照してください。
