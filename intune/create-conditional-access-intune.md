---
title: Intune によるデバイス ベースの条件付きアクセスの設定
titlesuffix: Microsoft Intune
description: Microsoft Intune デバイスのコンプライアンスとモバイル アプリ管理に基づいて、デバイス ベースの条件付きアクセス ポリシーを作成する方法について説明します。
keywords: ''
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 320ded06b59b583baf27544249393029f7488b2d
ms.sourcegitcommit: 0f19bc5c76b7c0835bfd180459f2bbd128eec1c2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53267717"
---
# <a name="create-a-device-based-conditional-access-policy"></a>デバイス ベースの条件付きアクセス ポリシーを作成する

Intune を利用して、モバイル デバイスのコンプライアンスをアクセス制御に追加することで、Azure Active Directory における条件付きアクセスを拡張できます。 デバイスがコンプライアンスに準拠するように要件を定義した Intune コンプライアンス ポリシーを作成すると、以降はデバイスのコンプライアンス ステータスを使用して、お使いのアプリとサービスへのアクセスを許可または拒否できるようになります。 **[デバイスは準拠としてマーク済みである必要があります]** 設定を使用した条件付きアクセス ポリシーを作成することで、これを実現できます。 

条件付きアクセス ポリシーでは、保護するアプリまたはサービス、そのアプリまたはサービスにアクセスできる条件、およびポリシーが適用されるユーザーを指定します。 条件付きアクセスは、Azure Active Directory 内で構成できる Azure AD のプレミアム機能ですが、Intune ポータル内からこれらと同じポリシーを設定することも可能です。 

> [!IMPORTANT]
> 条件付きアクセスを設定する前に、Intune デバイスのコンプライアンス ポリシーを設定して、特定の要件を満たしているかに基づいてデバイスを評価する必要があります。 「[Intune のデバイス コンプライアンス ポリシーの概要](device-compliance-get-started.md)」をご覧ください。

## <a name="create-conditional-access-policy"></a>条件付きアクセス ポリシーを作成します

1.  Intune ポータルで、**[条件付きアクセス]** > **[ポリシー]** > **[新しいポリシー]** の順に選択します。
   
    ![新しい条件付きアクセス ポリシーを作成する](media/create-conditional-access-intune/create-ca.png)
 
2.  **[割り当て]** で、**[ユーザーとグループ]** を選択します。 
3.  **[含む]** タブで、この条件付きアクセス ポリシーを適用するユーザーまたはグループを特定します。 含める対象を選択した後は、このポリシーから除外する任意のユーザー、ロール、またはグループがある場合、**[除外]** タブを使用できます。  
    - **[すべてのユーザー]**: 内部ユーザーやゲスト ユーザーを含め、すべてのユーザーおよびグループにポリシーを適用するには、このオプションを選びます。
  
    - **[ユーザーとグループを選択する]**: このオプションを選ぶ場合は、次のうち 1 つ以上のオプションを指定します。
  
      」を参照します。 **[すべてのゲスト ユーザー]**: 外部のゲスト ユーザー (たとえば、パートナーや外部のコラボレーターなど) を含めるか、または除外するには、このオプションを選びます。
       
      b. **[ディレクトリ ロール]**: 1 つ以上の Azure AD ロールを選択して、それらのロールに割り当てられたユーザーを含めるか、または除外します。
      
      c. **[ユーザーとグループ]**: 含める/除外する個々のユーザーまたはグループを検索して選択するには、このオプションを選びます。
     
       > [!TIP]  
       > 小規模なユーザーのグループに対してポリシーをテストして、期待どおりに動作することを確認してください。
4.  **[完了]** を選びます。
5.  **[割り当て]** で、**[クラウド アプリ]** を選択します。 
6.  **[含む]** タブで、この条件付きアクセス ポリシーによって保護するアプリおよびサービスを特定します。 その後、このポリシーから除外する任意のアプリやサービスがある場合は、**[除外]** タブを使用できます。
    - **[すべてのクラウド アプリ]**:すべてのアプリにポリシーを適用するには、このオプションを選びます。
      > [!IMPORTANT]  
      > Azure portal にアクセスするための Microsoft Azure 管理アプリは、このリストに含まれます。 必ず、この画面または **[ユーザーとグループ]** オプションのどちらかにある **[除外]** タブを使用して、ご自身 (あるいは、指定したユーザーまたはグループ) が Azure portal に確実にサインインできるようにしてください。 

    - **[アプリを選択]**: このオプションを選ぶ場合は、**[選択]** をクリックしてから、アプリケーションの一覧を使って保護するアプリまたはサービスを検索して選択します。
    
      ![新しい条件付きアクセス ポリシーを作成する](media/create-conditional-access-intune/create-ca-select-apps.png)

7.  **[完了]** を選びます。
8.  **[割り当て]** の下で、**[条件]** を選択します。
    - **[サインイン リスク]**: Azure AD Identity Protection のサインイン リスク検出を使用するために [はい] を選択してから、ポリシーに適用するサインイン リスクのレベルを選択します。
    - **[デバイス プラットフォーム]**: **[含む]** タブで、この条件付きアクセス ポリシーを適用するデバイス プラットフォームを特定します。 このポリシーからプラットフォームを除外するには、**[除外]** タブを使用します。
    - **[場所]**: **[含む]** タブで、任意の場所、IT 部門で制御されている信頼済みネットワークの場所、または特定のネットワークの場所のどれにポリシーを適用するかを指定します。 このポリシーからネットワークの場所を除外するには、**[除外]** タブを使用します。 
    - **[クライアント アプリ]**: **[はい]** を選択して、ブラウザー アプリ、モバイル アプリ、およびデスクトップ クライアントのどれにポリシーを適用するかを指定します。 また、**先進認証クライアント** (iOS 版の Outlook や Android 版の Outlook など) および **Exchange ActiveSync クライアント**を選択することも可能です。
    - **[デバイスの状態]**: [はい] を選択して、[ハイブリッド Azure AD 参加済みのデバイス] または [デバイスは準拠としてマーク済み] のどちらか (または両方) の状態を特に除外していない限り、条件付きアクセス ポリシーがすべてのデバイスの状態に適用されます。
    
      ![新しい条件付きアクセス ポリシーを作成する](media/create-conditional-access-intune/create-ca-device-platforms.png)

      > [!TIP]  
      > **先進認証**クライアントと **Exchange ActiveSync クライアント**の両方を保護する場合、クライアントの種類ごとに 1 つずつ、計 2 つの別個の条件付きアクセス ポリシーを作成します。 Exchange ActiveSync では先進認証をサポートしていますが、Exchange ActiveSync でサポートされる条件はプラットフォームだけです。 多要素認証などのその他の条件は、サポートされていません。 Exchange ActiveSync から Exchange Online へのアクセスを効率よく保護するには、[サポートされているプラットフォームのみにポリシーを適用する] を選択したうえで、クラウド アプリ Office 365 Exchange Online とクラウド アプリ Exchange ActiveSync を指定する条件付きアクセス ポリシーを作成します。

9.  **[完了]** を選びます。
10. **[アクセス制御]** で **[許可]** を選択します。 設定した条件に基づいて、実行される制御を構成します。  次のオプションから選択できます。
    - **[アクセスのブロック]**: 指定済みの条件の下では、このポリシーに指定されたユーザーはアプリへのアクセスが拒否されます。
    - **[アクセスの許可]**: このポリシーに指定されたユーザーはアクセスが許可されますが、ユーザーに対してさらに次のいずれかの操作を要求することが可能です。
      - **[多要素認証が必要]**:ユーザーは、電話呼び出しや文字入力など、追加のセキュリティ要件を完了する必要があります。
      - **[デバイスは準拠としてマーク済みである必要があります]**: デバイスは Intune に準拠している必要があります。 デバイスが準拠していない場合、Intune にデバイスを登録するためのオプションがユーザーに提示されます。 
      - **[ハイブリッド Azure AD 参加済みのデバイスが必要]**: デバイスはハイブリッド Azure AD に参加している必要があります。
      - **[承認されたクライアント アプリが必要です]**: デバイスは承認されたクライアント アプリを使用する必要があります。 
      - **[複数のコントロールの場合]**: デバイスがアプリへのアクセスを試行するときに、上記のすべての要件が適用されるように、**[選択したコントロールすべてが必要]** を選択します。
    
      ![アクセス制御の [許可] 設定](media/create-conditional-access-intune/create-ca-grant-access-settings.png)
 
11. **[ポリシーを有効にする]** で、**[オン]** を選択します。
     
     ![ポリシーの有効化](media/create-conditional-access-intune/enable-policy.png)

12. **[作成]** を選択します。

## <a name="see-also"></a>関連項目
[Intune を使用したアプリ ベースの条件付きアクセス](app-based-conditional-access-intune.md)