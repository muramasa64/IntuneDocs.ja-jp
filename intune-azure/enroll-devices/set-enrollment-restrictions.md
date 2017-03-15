---
title: "Intune で登録制限を設定する"
titleSuffix: Intune Azure preview
description: "Intune Azure プレビュー: Intune でプラットフォームごとに登録を制限し、デバイス登録の上限数を設定します。 "
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: 153cce3809e24303b8f88a833e2fc7bdd9428a4a
ms.openlocfilehash: 56996592febf0be5ab74b158a70404728fe17a4d
ms.lasthandoff: 02/18/2017

---

# <a name="set-enrollment-restrictions"></a>登録制限を設定する 

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

登録を許可するデバイスの種類と最大数を設定することができます。 [登録の制限] ブレードでは、次のことを設定できます。

- 登録を許可されるプラットフォームと、Android および iOS の個人所有デバイスの登録をブロックするかどうか。

- ユーザーが登録できるデバイスの最大数。

## <a name="set-device-type-restrictions"></a>デバイスの種類の制限を設定する

1. Azure Portal で、**[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。

2. [Intune] ブレードで **[デバイスの登録]** を選択し、**[登録の制限]** を選択します。

3. **[デバイスの種類の制限]** で、**[既定]** を選択します。

4. **[すべてのユーザー]** ブレードで、**[プラットフォーム]** を選択します。

5. Intune で登録できるようにするプラットフォームに対して、**[許可]** を選択します。 登録できないようにするプラットフォームに対しては、**[ブロック]** を選択します。 プラットフォームは規定で **[許可]** に設定されます。 

    >[!NOTE]
    >これらの設定は、Intune ソフトウェア クライアントを使って行われる Windows の登録に適用されたり、登録をブロックしたりすることはありません。 これらの設定は、モバイル デバイス管理を使う登録にのみ影響します。 

6. **[保存]** を選択します。

7. **[プラットフォーム構成]** を選択します。

8. 個人所有の iOS および Android デバイスの登録を **[許可]** するか **[ブロック]** するかを選びます。

9. **[保存]** を選択します。

## <a name="set-device-limit-restrictions"></a>デバイス数の制限を設定する

1. Azure Portal で、**[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。

2. [Intune] ブレードで **[デバイスの登録]** を選択し、**[登録の制限]** を選択します。

3. **[デバイス数の制限]** で、**[既定]** を選択します。

4. **[すべてのユーザー]** ブレードで、**[デバイスの上限数]** を選択します。

5. ユーザーが登録できるデバイスの最大数を選択し、**[保存]** を選択します。
