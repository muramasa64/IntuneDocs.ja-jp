---
title: Microsoft Intune にサインアップまたはサインインする
description: Microsoft Intune サブスクリプションにサインアップする方法、またはサブスクリプションを使用してサインインする方法。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 0f3ce07a-b718-42a9-bace-f99a8b8abd94
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 97a1ab3327f8d76f1623d51fe80289a8f15d7ff1
ms.sourcegitcommit: cb93613bef7f6015a4c4095e875cb12dd76f002e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2019
ms.locfileid: "57235227"
---
# <a name="sign-up-or-sign-in-to-microsoft-intune"></a>Microsoft Intune にサインアップまたはサインインする

[!INCLUDE [both-portals](./includes/note-for-both-portals.md)]

このトピックでは、システム管理者が Intune アカウントにサインアップする方法を説明します。

Intune にサインアップする前に、Microsoft Online Services アカウント、Enterprise Agreement、または同等のボリューム ライセンス契約が既にあるかどうかを確認してください。 Microsoft ボリューム ライセンス契約や、Office 365 などの他の Microsoft クラウド サービス サブスクリプションには、通常、職場または学校アカウントが含まれます。

既に職場または学校アカウントがある場合は、そのアカウントで**サインイン**し、Intune をサブスクリプションに追加します。 それ以外の場合は、新しいアカウントに**サインアップ**して、組織で Intune を使うことができます。

>[!WARNING]
>新しいアカウントにサインアップした後で、既存の職場または学校アカウントを組み合わせることはできません。

## <a name="how-to-sign-up-or-sign-in-to-intune"></a>Intune にサインアップまたはサインインする方法

1. [Intune のサインアップ ページ](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)にアクセスします。

   ![Microsoft Intune 試用版アカウントのサインアップ Web ページのスクリーンショット](./media/account-sign-up-site.png)

2. サインアップ ページで、Intune の新しいサブスクリプションを管理するために、サインアップまたはサインインします。

## <a name="post-sign-up-considerations"></a>サインアップ後の考慮事項
新しいサブスクリプションにサインアップした後、アカウント情報の記載されたメール メッセージが、サインアップ過程で登録したメール アドレスに送信されます。 このメールで、サブスクリプションがアクティブになったことが確認されます。

サインアップ プロセスが完了すると、ユーザーの追加とライセンスの割り当てに使われる Office 365 管理センターが表示されます。 既定の onmicrosoft.com ドメイン名を使ったクラウドベースのアカウントだけがある場合は、この時点でユーザーを追加し、ライセンスを割り当てることができます。 一方、組織の[カスタム ドメイン名](custom-domain-name-configure.md)を使う場合や、オンプレミスの Active Directory から[ユーザー アカウント情報を同期する](users-add.md#sync-active-directory-and-add-users-to-intune)場合は、そのブラウザー ウィンドウを閉じてかまいません。
