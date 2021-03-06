---
title: ユーザー - Intune データ ウェアハウス
titleSuffix: Microsoft Intune
description: Intune データ ウェアハウス API のエンティティ コレクションのユーザー カテゴリに関するリファレンス トピック。
keywords: Intune データ ウェアハウス
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/09/2019
ms.topic: reference
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: C29A6EEA-72B7-427E-9601-E05B408F3BB0
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e650f8cb713d76c44d3f3399612ee5fd6d02426
ms.sourcegitcommit: 601327125ac8ae912d8159422de8aac7dbdc25f6
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2019
ms.locfileid: "59429146"
---
# <a name="reference-for-user-entity"></a>ユーザー エンティティのリファレンス

**ユーザー** カテゴリには、データ モデルのユーザーのプロパティを定義する **User** エンティティが含まれています。

## <a name="user"></a>User

**User** エンティティには、社内のすべての Azure Active Directory (Azure AD) ユーザーと割り当てられているライセンスが表示されます。

**User** エンティティ コレクションにはユーザー データが含まれています。 これらのレコードには、ユーザーが削除されている場合でも、データ コレクション期間中のユーザーの状態が含まれます。 たとえば、ユーザーが Intune に追加され、過去 1 か月の過程で削除されたとします。 このユーザーがレポートの時点では存在しない一方で、ユーザーと状態は先月のデータに存在します。 データ内のユーザーの履歴における存在の期間を示すレポートを作成できます。

|          プロパティ          |                                                                                                           説明                                                                                                          |                例               |
|:--------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------:|
| UserKey                    | データ ウェアハウス内のユーザーを示す一意識別子 - 代理キー。                                                                                                                                                         | 123                                  |
| UserId                     | ユーザーを示す一意識別子 - UserKey と似ていますが、ナチュラル キーです。                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| UserEmail                  | ユーザーの電子メール アドレス。                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | ユーザーのユーザー プリンシパル名。                                                                                                                                                                                               | John@constoso.com                    |
| DisplayName                 | ユーザーの表示名。                                                                                                                                                                                                      | John                                 |
| IntuneLicensed             | ユーザーに Intune のライセンスがあるかどうかを示します。                                                                                                                                                                              | 真/偽                           |
| IsDeleted                  | そのユーザーのすべてのライセンスの期限が切れているかどうか、および、そのユーザーがそのため Intune から削除されたかどうかを示します。 1 つのレコードでは、このフラグは変更されません。 代わりに、新しいユーザー状態用の新しいレコードが作成されます。 | 真/偽                           |
| RowLastModifiedDateTimeUTC | レコードがデータ ウェアハウスで最後に変更されたときの UTC 日時                                                                                                                                                 | 11/23/2016 0:00                      |


## <a name="next-steps"></a>次の手順
 - **現在のユーザー** エンティティ コレクションを使用して、現在アクティブなユーザーにユーザー データを制限することができます。 詳細については、「[現在のユーザー エンティティのリファレンス](reports-ref-current-user.md)」をご覧ください。
 - データ ウェアハウスが Intune のユーザーの有効期間を追跡する方法の詳細については、「[Intune データ ウェアハウスのユーザー有効期間の表記](reports-ref-user-timeline.md)」をご覧ください。
