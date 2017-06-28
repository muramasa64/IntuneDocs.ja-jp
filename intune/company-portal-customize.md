---
title: "ポータル サイトをカスタマイズする"
description: "Intune ポータル サイトでは、ユーザーはデバイスの登録、アプリのインストール、および IT 部署情報の検索など、一般的なタスクを行うことができます。"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 06/07/2017
ms.topic: get-started-article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: eb4a9f01-f857-4563-ab6f-5d0d7dfa659d
ms.reviewer: angerobe
ms.suite: ems
ms.custom: intune-classic
ms.translationtype: Human Translation
ms.sourcegitcommit: df3c42d8b52d1a01ddab82727e707639d5f77c16
ms.openlocfilehash: e54f1a2ab0e62ab3ffcbf6fa1ae6f974c5f18717
ms.contentlocale: ja-jp
ms.lasthandoff: 06/08/2017


---

# <a name="customize-the-company-portal"></a>ポータル サイトをカスタマイズする

[!INCLUDE[both-portals](./includes/note-for-both-portals.md)]

このトピックでは、管理者が Intune ポータル サイト アプリとポータル サイト Web サイトをカスタマイズする方法を説明します。

ユーザーは、Intune ポータル サイトを使用して、会社のデータにアクセスしたり、デバイスの登録、アプリケーションのインストール、IT 部門からのサポート情報の検索などの一般的なタスクを実行したりできます。

Intune ポータル サイトは、ユーザーが会社のデータとアプリにアクセスできるようにします。 ポータル サイトは、次の 2 つの形式で使用できます。

-   **ポータル サイト アプリ**: Intune を使用して管理するデバイスで利用できるアプリケーション。 [Android](/intune-user-help/using-your-android-device-with-intune)、[iOS](/intune-user-help/using-your-iOS-or-macOS-device-with-intune) および [Windows](/intune-user-help/using-your-windows-device-with-intune) 用のポータル サイトの詳細を、それぞれご確認ください。


- **ポータル Web サイト**: エンドユーザーがポータル サイト アプリから実行できるタスクのほとんどを行うことができる Web サイト。 Intune ポータル サイトの URL は [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) です。 この Web サイトの詳細については、「[Intune ポータル サイト Web サイトの使用](/intune-user-help/using-the-intune-company-portal-website)」を参照してください。

> [!TIP]
> ポータル サイトをカスタマイズすると、構成がポータル サイトの Web サイトとポータル サイト アプリの両方に適用されます。

ユーザーは、ポータル サイトで次のようなタスクを実行できます。

-   デバイスの登録
-   デバイスの状態の表示
-   デバイスのリセット
-   パスワードのリセット
-   デバイスのリモートからのロック
-   組織で展開されているソフトウェアのダウンロード
-   サポートの IT 部門への連絡

## <a name="customize-company-portal-settings"></a>ポータル サイト設定をカスタマイズする
ポータル サイトをカスタマイズすることで、エンド ユーザーの利便性を向上させることができます。 テナントまたはサービス管理者として [Microsoft Intune 管理コンソール](https://manage.microsoft.com)にログインし、**[管理者]** &gt; **[ポータル サイト]** の順に選択して、ポータル サイトの設定を構成します。

## <a name="company-contact-information-and-privacy-statement"></a>会社の連絡先情報とプライバシーに関する声明
会社名は、ポータル サイトのタイトルとして表示されます。 連絡先情報と詳細は、ポータル サイトの [IT に連絡] 画面でユーザーに対して表示されます。 プライバシーに関する声明は、ユーザーがプライバシー リンクをクリックすると表示されます。

|フィールド名|最大長|詳細情報|
    |----------|------------------------|----------------|
    |会社名|40|ポータル サイトのタイトルとして表示される名前です。|
    |IT 部門の担当者名|40|**[IT に連絡]** ページに表示される名前です。|
    |IT 部門の電話番号|20|**[IT に連絡]** ページに表示される連絡先の電話番号です。|
    |IT 部門の電子メール アドレス|40|**[IT に連絡]** ページに表示される連絡先の電子メール アドレスです。 **alias@domainname.com** の形式で有効な電子メール アドレスを入力する必要があります。|
    |追加情報|120|**[IT に連絡]** ページに表示されます。|
    |会社のプライバシーに関する声明の URL|79|ポータル サイトでユーザーがプライバシー リンクをクリックすると表示される、各社のプライバシーに関する声明を指定できます。 https://www.contoso.com の形式で URL を入力します。|

## <a name="support-contacts"></a>サポートの連絡先
サポート Web サイトは、ポータル サイトに表示されます。ユーザーは、サポート サイトからオンライン サポートを利用できます。

|フィールド名|最大長|詳細情報|
    |----------|------------------------|----------------|
    |サポート Web サイトの URL|150|ユーザーが使用するサポート Web サイトがある場合、その URL を指定します。 URL は、https://www.contoso.com という形式にする必要があります。 URL を指定しない場合、ポータル サイトの **[IT に連絡]** ページのサポート Web サイトには何も表示されません。|
    |Web サイト名|40|サポート Web サイトの URL に表示されるフレンドリ名です。 サポート Web サイトの URL を指定し、フレンドリ名を指定しない場合、ポータル サイトの **[IT に連絡]** ページに **[IT Web サイトに移動する]** が表示されます。|

## <a name="company-branding-customization"></a>会社のブランドのカスタマイズ
ポータル サイトのロゴや会社名、テーマの色や背景をカスタマイズできます。

|フィールド名|詳細情報|
    |----------|----------------|
    |テーマの色|ポータル サイトに適用するテーマの色を選択します。|
    |会社のロゴを含める|このオプションを有効にすると、ポータル サイトに表示する会社のロゴをアップロードできます。 2 つのロゴをアップロードできます。1 つは、ポータル サイトの背景が白の場合に表示するロゴ、もう 1 つは、選択したテーマの色がポータル サイトの背景に使用されている場合に表示するロゴです。 各ロゴは、.png または .jpg ファイルの種類にし、最大解像度が 400 x 100 ピクセルで、750 KB 以下のサイズにします。|
    |Windows 8 ポータル サイト アプリの背景を選択する|この設定は、Windows 8 ポータル サイト アプリのみの背景に適用されます。|


変更を保存した後で、管理コンソールの **[ポータル サイト]** ページの下部に表示されるリンクを使用して、ポータル サイト Web サイトを表示できます。 これらのリンクは変更できません。 ユーザーがサインインするときに、これらのリンクでポータル サイトが表示されます。
