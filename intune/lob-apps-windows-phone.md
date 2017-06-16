---
title: "Windows Phone の基幹業務アプリを Intune に追加する方法 | Microsoft Docs"
titleSuffix: Intune Azure preview
description: "Intune Azure プレビュー: Windows Phone の基幹業務アプリを Intune に追加する方法について説明します。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 04/12/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: a097b7b2-d01d-454b-954c-da4f3cd0ae86
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 4d9adb9a5120c83023bb25199f666f1352752562
ms.contentlocale: ja-jp
ms.lasthandoff: 05/23/2017

---

# <a name="how-to-add-windows-phone-line-of-business-lob-apps-to-microsoft-intune"></a>Windows Phone の基幹業務 (LOB) アプリを Microsoft Intune に追加する方法

[!INCLUDE[azure_preview](./includes/azure_preview.md)]


## <a name="step-1---specify-the-software-setup-file"></a>手順 1 - ソフトウェアのセットアップ ファイルを指定する

1. Azure ポータルにサインインします。
2. **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[アプリの管理]** を選択します。
4. **[モバイル アプリ]** ワークロードで、**[管理]** > **[アプリ]** の順に選択します。
5. アプリの一覧の上にある **[追加]** を選択します。
6. **[アプリの追加]** ブレードで、**[基幹業務アプリ]** を選択します。

## <a name="step-2---configure-the-app-package-file"></a>手順 2 - アプリのパッケージ ファイルを構成する

1. **[アプリの追加]** ブレードで、**[アプリのパッケージ** ファイル] を選択します。
2. **[アプリのパッケージ ファイル]** ブレードで、参照ボタンを選択し、拡張子 **.xap** が付いた Windows Phone インストール ファイルを選択します。
3. 終了したら **[OK]** を選択します。


## <a name="step-3---configure-app-information"></a>手順 3 - アプリ情報を構成する

1. **[アプリの追加]** ブレードで、**[アプリのパッケージ** ファイル] を選択します。
2. **[アプリ情報]** ブレードで、以下の情報を構成します。 選択したアプリによっては、このブレード内の一部の値が自動的に入力されている場合があります。
    - **名前** - アプリの名前を入力します。この名前は会社のポータルに表示されます。 使用するアプリ名はすべて一意にします。 同じアプリ名が 2 つ存在する場合、会社のポータルではそのいずれかのみがユーザーに表示されます。
    - **説明** - アプリの説明を入力します。 これは会社のポータルでユーザーに表示されます。
    - **発行元** - アプリの発行元の名前を入力します。
    - **[カテゴリ]** - 1 つまたは複数の組み込みアプリ カテゴリ、または作成したカテゴリを選択します。 会社のポータルを閲覧するとき、ユーザーにとってアプリを探すのが簡単になります。
    - **[会社のポータルでおすすめアプリとして表示します]** - ユーザーがアプリを探す際に、会社のポータルのメイン ページでアプリを目立つように表示します。
    - **[情報 URL]** - 必要に応じて、このアプリに関する情報が含まれる Web サイトの URL を入力します。 この URL は会社のポータルでユーザーに表示されます。
    - **[プライバシー URL]** - 必要に応じて、このアプリのプライバシー情報が含まれる Web サイトの URL を入力します。 この URL は会社のポータルでユーザーに表示されます。
    - **[開発者]** - 必要に応じて、アプリ開発者の名前を入力します。
    - **[所有者]** - 必要に応じて、このアプリの所有者の名前 ("**人事部**" など) を入力します。
    - **[メモ]** - このアプリに関連付けるメモを入力します。
    - **[ロゴ]** - アプリに関連付けるアイコンをアップロードします。 ユーザーが会社のポータルを参照するとき、アプリにこのアイコンが表示されます。
3. 終了したら **[OK]** を選択します。

## <a name="step-4---finish-up"></a>手順 4. - 完了

1. **[アプリの追加]** ブレードで、構成した情報が正しいことを確認します。
2. **[追加]** を選択して、アプリを Intune にアップロードします。

作成したアプリはアプリの一覧に表示され、選択したグループに割り当てることができるようになります。 詳細については、[アプリをグループに割り当てる方法](apps-deploy.md)に関するページを参照してください。
