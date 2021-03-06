---
title: チュートリアル - アンマネージド デバイス上で Exchange Online の電子メールを保護する
titleSuffix: Microsoft Intune
description: Intune アプリの保護ポリシーと Azure AD 条件付きアクセスを利用して Office 365 Exchange Online をセキュリティ保護する方法について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/26/2019
ms.topic: tutorial
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6224a0dae7c0aa3d80d4e64331a668953220f65
ms.sourcegitcommit: 143dade9125e7b5173ca2a3a902bcd6f4b14067f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61515782"
---
# <a name="tutorial-protect-exchange-online-email-on-unmanaged-devices"></a>チュートリアル: アンマネージド デバイス上で Exchange Online の電子メールを保護する

Intune などのデバイス管理ソリューションにデバイスが登録されていない場合でも、条件付きアクセスを利用したアプリの保護ポリシーを使って Exchange Online を保護する方法について確認します。 このチュートリアルでは、次の方法について説明します。 

> [!div class="checklist"]
> * Outlook アプリ用の Intune アプリ保護ポリシーを作成する。 "名前を付けて保存" を防止することで、ユーザーができるアプリ データの操作を限定すると共に、切り取り、コピー、および貼り付けのアクションを制限します。 
> * Outlook アプリのみに Exchange Online の会社の電子メールへのアクセスを許可する Azure Active Directory (Azure AD) 条件付きアクセス ポリシーを作成する。 また、iOS 版や Android 版の Outlook など、先進認証クライアントには多要素認証 (MFA) も要求します。

## <a name="prerequisites"></a>必要条件
  - このチュートリアルでは、次のサブスクリプションのあるテスト テナントが必要です。
    - Azure Active Directory Premium ([無料試用版](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
    - Intune サブスクリプション ([無料試用版](free-trial-sign-up.md))
    - Exchange を含む Office 365 Business サブスクリプション ([無料試用版](https://go.microsoft.com/fwlink/p/?LinkID=510938))

## <a name="sign-in-to-intune"></a>Intune にサインインする

グローバル管理者または Intune サービス管理者として [Intune](https://aka.ms/intuneportal) にサインインします。 Intune には、Azure portal で **[すべてのサービス]** > **[Intune]** を選択してアクセスします。

## <a name="create-the-app-protection-policy"></a>アプリ保護ポリシーを作成する
このチュートリアルでは、Outlook アプリにおいてアプリ レベルで適切に保護を配置するための Intune アプリ保護ポリシーを設定します。 仕事上では、アプリを開くために PIN を要求します。 また、アプリ間でのデータ共有を制限して、会社のデータが個人用の場所に保存されることを防ぎます。

1.  Intune で、**[クライアント アプリ]** > **[アプリ保護ポリシー]** > **[ポリシーの追加]** の順に選択します。
2.  **[名前]** に、「**Outlook app policy test**」(Outlook アプリのポリシー テスト) と入力します。
3.  **[説明]** に、「**Outlook app policy test**」(Outlook アプリのポリシー テスト) と入力します。
4.  **[アプリ]** を選択します。 アプリの一覧で **[Outlook]** を選択してから、**[選択]** をクリックします。
5.  **[設定]** を選択します。 
6.  **[データ再配置]** の下で、このチュートリアルのために次の設定を選択します。

    - **[アプリで他のアプリへのデータ転送を許可する]** で、**[なし]** を選択します。
    - **[アプリで他のアプリからのデータの受信を許可する]** で、**[なし]** を選択します。
    - **[[名前を付けて保存] を禁止する]** で、**[はい]** を選択します。
    - **[他のアプリとの間で切り取り、コピー、貼り付けを制限する]** で、**[禁止]** を選択します。
   
     ![Outlook アプリ保護ポリシー データの再配置の設定を選択する](media/tutorial-protect-email-on-unmanaged-devices/outlook-app-data-relocation.png)
    
7.  **[アクセス アクション]** の下で、このチュートリアルのために次の設定を選択します。

    - **[アクセスのために PIN を要求する]** で、**[はい]** を選択します。
    - **[アクセスには会社の資格情報が必要]** で、**[はい]** を選択します。
    - その他の設定はすべて、既定値のままにします。
 
     ![Outlook アプリ保護ポリシー アクセスのアクションを選択する](media/tutorial-protect-email-on-unmanaged-devices/outlook-app-access-actions.png)

9.  **[OK]** を選択します。
10. **[作成]** を選択します。

Outlook 用のアプリ保護ポリシーが作成されます。 これで、Outlook アプリを使用するデバイスに要求する条件付きアクセスを設定できるようになりました。

## <a name="create-conditional-access-policies"></a>条件付きアクセス ポリシーを作成する
次に、すべてのデバイス プラットフォームに対応する 2 つの条件付きアクセス ポリシーを作成します。 最初のポリシーでは、iOS 版 Outlook や Android 版 Outlook などの先進認証クライアントに、承認済みの Outlook アプリと MFA を使用するように要求します。 2 番目のポリシーでは、Exchange ActiveSync クライアントに、承認済みの Outlook アプリを使用するように要求します  (現時点では、Exchange Active Sync ではデバイス プラットフォーム以外の条件をサポートしていません)。 Azure AD ポータルまたは Intune ポータルのいずれかで、条件付きアクセス ポリシーを構成できます。 既に Intune ポータルにいるので、ここでポリシーを作成します。
### <a name="create-an-mfa-policy-for-modern-authentication-clients"></a>先進認証クライアント用の MFA ポリシーを作成する
1.  Intune で、**[条件付きアクセス]** > **[ポリシー]** > **[新しいポリシー]** の順に選択します。
1.  **[名前]** に「**Test policy for modern auth clients**」(先進認証クライアント用のテスト ポリシー) と入力します。 
3.  **[割り当て]** で、**[ユーザーとグループ]** を選択します。 **[含む]** タブで **[すべてのユーザー]** を選択して、**[完了]** を選択します。

4.  **[割り当て]** で、**[クラウド アプリ]** を選択します。 Office 365 Exchange Online のメールを保護するので、次の手順で選択します。
     
    1. **[含む]** タブで、**[アプリを選択]** を選択します。
    2. **[選択]** を選択します。 
    3. アプリケーションの一覧で **Office 365 Exchange Online** を選択し、**[選択]** を選択します。 
    4. **[完了]** を選びます。
  
    ![Office 365 Exchange Online アプリを選択する](media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-cloud-apps.png)

5.  **[割り当て]** で、**[条件]** > **[デバイス プラットフォーム]** を選択します。
     
    1. **[構成]** で、**[はい]** を選択します。
    2. **[含む]** タブで、**[任意のデバイス]** を選択します。
    1. **[完了]** を選びます。
   
6.  **[条件]** ウィンドウで、**[クライアント アプリ]** を選択します。
     
    1. **[構成]** で、**[はい]** を選択します。
    2. **[モバイル アプリとデスクトップ クライアント]** および **[先進認証クライアント]** を選択します。
    3. それ以外のチェック ボックスをオフにします。
    4. **[完了]** を選択し、**[完了]** をもう一度選択します。
    
    ![Office 365 Exchange Online アプリを選択する](media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png)

7.  **[アクセス制御]** で **[許可]** を選択します。 
     
    1. **[許可]** ウィンドウで、**[アクセス権の付与]** を選択します。
    2. **[多要素認証が必要]** を選択します。
    4. **[承認されたクライアント アプリが必要です]** を選択します。
    5. **[複数のコントロールの場合]** で、**[選択したコントロールすべてが必要]** を選択します。 この設定により、デバイスがメールへのアクセスを試みるときに、選択した両方の要件が適用されます。
    6. **[選択]** を選択します。
     
    ![Office 365 Exchange Online アプリを選択する](media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png)

8.  **[ポリシーを有効にする]** で、**[オン]** を選択します。
     
    ![Office 365 Exchange Online アプリを選択する](media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png)

9.  **[作成]** を選択します。

先進認証クライアント用の条件付きアクセス ポリシーが作成されます。 これで、次は Exchange Active Sync クライアント用のポリシーを作成できます。

### <a name="create-a-policy-for-exchange-active-sync-clients"></a>Exchange Active Sync クライアント用のポリシーを作成する
1.  Intune で、**[条件付きアクセス]** > **[ポリシー]** > **[新しいポリシー]** の順に選択します。
2.  **[名前]** に「**Test policy for EAS clients**」(EAS クライアント用のテスト ポリシー) と入力します。 
3.  **[割り当て]** で、**[ユーザーとグループ]** を選択します。 **[含む]** タブで **[すべてのユーザー]** を選択して、**[完了]** を選択します。

4.  **[割り当て]** で、**[クラウド アプリ]** を選択します。 次の手順を使用して、Office 365 Exchange Online 電子メールを選択します。
     
    1. **[含む]** タブで、**[アプリを選択]** を選択します。
    2. **[選択]** を選択します。 
    3. アプリケーションの一覧で **Office 365 Exchange Online** を選択し、**[選択]** を選択します。 
    4. **[完了]** を選びます。

5.  **[割り当て]** で、**[条件]** > **[デバイス プラットフォーム]** を選択します。
     
    1. **[構成]** で、**[はい]** を選択します。
    2. **[含む]** タブで **[任意のデバイス]** を選択してから、**[完了]** を選択します。 
    3. **[完了]** をもう一度選択します。

6.  **[条件]** ウィンドウで、**[クライアント アプリ]** を選択します。
     
    1. **[構成]** で、**[はい]** を選択します。
    2. **[モバイル アプリとデスクトップ クライアント]** を選択します。
    3. **[Exchange ActiveSync クライアント]** および **[サポートされているプラットフォームのみにポリシーを適用する]** を選択します。 
    4. 他のチェック ボックスはすべてオフにします。
    5. **[完了]** を選択し、**[完了]** をもう一度選択します。
    
    ![Office 365 Exchange Online アプリを選択する](media/tutorial-protect-email-on-unmanaged-devices/eas-client-apps.png)

7.  **[アクセス制御]** で **[許可]** を選択します。 
     
    1. **[許可]** ウィンドウで、**[アクセス権の付与]** を選択します。
    4. **[承認されたクライアント アプリが必要です]** を選択します。 他のチェック ボックスはすべてオフにします。
    6. **[選択]** を選択します。
     
    ![Office 365 Exchange Online アプリを選択する](media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png)

8.  **[ポリシーを有効にする]** で、**[オン]** を選択します。

9.  **[作成]** を選択します。

アプリ保護ポリシーと条件付きアクセスが配置され、テストの準備が整いました。 

## <a name="try-it-out"></a>試してみましょう
作成したポリシーを使用する場合、デバイスが Intune に登録され、Outlook モバイル アプリを使用して Office 365 電子メールにアクセスしている必要があります。 iOS デバイスでこのシナリオをテストするには、テスト テナントのユーザーの資格情報を使用して、Exchange Online へのサインインを試みます。
1. iPhone でテストするには、**[Settings]\(設定\)** > **[Passwords & Accounts]\(パスワードとアカウント\)** > **[Add Account]\(アカウントの追加\)** > **[Exchange]** に移動します。
2. テスト テナント内のユーザーのメール アドレスを入力し、**[次へ]** を選択します。
3. **[サインイン]** を選択します。
4. テスト ユーザーのパスワードを入力して、**[サインイン]** を選択します。
5. **[More information is required]** \(詳細情報が必要です\) というメッセージが表示され、MFA の設定が求められます。 手順を進めて、詳細な検証方法を設定します。
6. 次に、IT 部門では承認されていないアプリを使ってこのリソースを開こうとしていることを示すメッセージが表示されます。 これは、ネイティブな電子メール アプリの使用がブロックされていることを意味します。 サインインをキャンセルします。
7.  Outlook アプリを開き、**[設定]** > **[アカウントの追加]** > **[電子メール アカウントの追加]** の順に選択します。
8. テスト テナント内のユーザーのメール アドレスを入力し、**[次へ]** を選択します。
9. **[Sign in with Office 365]**/(Office 365 を使ってサインインする/) をクリックします。 追加認証と登録を求めるメッセージが表示されます。 サインインした後は、切り取り、コピー、貼り付けなどのアクションと "名前を付けて保存" をテストできます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする
テスト ポリシーが必要なくなった場合は削除できます。
1. グローバル管理者または Intune サービス管理者として [Intune](https://aka.ms/intuneportal) にサインインします。
2. **[デバイスのポリシー準拠]** > **[ポリシー]** の順に選択します。
3. **[ポリシー名]** ボックスの一覧で、お使いのテスト ポリシーのコンテキスト メニュー **[...]** を選択し、**[削除]** を選択します。 **[OK]** を選択して確定します。
4. **[条件付きアクセス]** > **[ポリシー]** の順に選択します。
5. **[ポリシー名]** 一覧で、お使いの各テスト ポリシーのコンテキスト メニュー **[...]** を選択し、**[削除]** を選択します。 **[はい]** をクリックして操作を確定します。

 ## <a name="next-steps"></a>次の手順 
このチュートリアルでは、アプリ保護ポリシーを作成して、Outlook アプリにおいてユーザーができる操作を制限しました。また、Outlook アプリの要求と、先進認証クライアントに対しては MFA の要求を行う条件付きアクセス ポリシーを作成しました。 他のアプリやサービスを保護するために条件付きアクセスと共に Intune を使用する方法については、「[条件付きアクセスの設定](conditional-access.md)」をご覧ください。
