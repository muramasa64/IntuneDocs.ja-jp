---
title: "Intune で iOS デバイスのユーザーをログアウトする"
titleSuffix: Intune on Azure
description: "Intune で iOS デバイスの現在のユーザーをログアウトする方法について説明します。\""
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 07/13/2017
ms.topic: get-started-article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 702bc46c-1a6f-4689-bd53-3b778a447baa
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 1de2069b7b25ee5e5c21a8e4caa7512f13d4ca0e
ms.sourcegitcommit: ee7f69efe9f32a1d6bdeb1fab73d03dbfe1ae58c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2017
---
# <a name="logout-the-current-user-on-intune-managed-ios-devices"></a>Intune で管理される iOS デバイスの現在のユーザーをログアウトする


[!INCLUDE[azure_portal](./includes/azure_portal.md)]


**[現在のユーザーのログアウト]** アクションにより、[iOS 教育プロファイル](education-settings-configure-ios.md)を使用して iOS Classroom アプリを管理するように構成されている共有の iPad デバイスから現在のユーザーがログアウトします。 

## <a name="supported-platforms"></a>サポートされているプラットフォーム

- Windows - サポートされていません
- Windows Phone - サポートされていません
- iOS - iOS 9.3 以降 (共有 iPad デバイスのみ) でサポートされています
- macOS - サポートされていません
- Android - サポートされていません

## <a name="how-to-logout-the-current-user"></a>現在のユーザーをログアウトする方法

1.  Azure ポータルにサインインします。
2.  **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。
3.  **[Intune]** ブレードで、**[デバイス]** を選択します。
4.  **[デバイスとグループ]** ブレードで、**[すべてのデバイス]** を選択します。
5.  管理するデバイスの一覧から iOS デバイスを選択して、**[現在のユーザーのログアウト]** のデバイス リモート アクションを選択します。

## <a name="next-steps"></a>次のステップ

実行したアクションの状態を確認するには、**[デバイスとグループ]** ブレードで **[デバイス アクション]** を選択します。