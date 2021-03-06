---
title: iOS アプリ保護ポリシー設定 | Microsoft Intune
titlesuffix: Microsoft Intune
description: このトピックでは、iOS デバイスのアプリ保護ポリシー設定について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/28/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 0f8b08f2-504c-4b38-bea2-b8a4ef0526b8
ms.reviewer: andcerat
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 73bc1a3bc03b5136c849fecbbe2a482f242b062f
ms.sourcegitcommit: 93de3423d2d8f0019e676a63784edeb3daf47cb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2019
ms.locfileid: "56325522"
---
#  <a name="ios-app-protection-policy-settings"></a>iOS アプリ保護ポリシー設定
[!INCLUDE [azure_portal](./includes/azure_portal.md)]

この記事では、iOS デバイスのアプリ保護ポリシーの設定について説明します。 新しいポリシーを作成する場合、説明されているポリシーの設定は、Azure portal の **[設定]** ブレード上でアプリ保護ポリシー用に[構成](app-protection-policies.md)することができます。

ポリシー設定にはカテゴリが 3 つあります。*データ再配置*、*アクセス要件*、および*条件付き起動*です。 この記事の "***ポリシーで管理されているアプリ***" という用語は、アプリ保護ポリシーで構成されるアプリを示します。

##  <a name="data-protection"></a>データの保護

### <a name="data-transfer"></a>データ転送
| Setting | 使用する方法 | 既定値 |
|------|----------|-------|
| **iTunes と iCloud のバックアップに組織データをバックアップ** | このアプリで職場や学校のデータが iTunes および iCloud にバックアップされないようにするには、**[ブロック]** を選択します。 このアプリで職場や学校のデータを iTunes および iCloud にバックアップできるようにするには、**[許可]** を選択します。 | **許可**  |
| **組織のデータを他のアプリに送信** | このアプリからデータを受け取ることができるアプリを指定します。 <ul><li>**すべてのアプリ**:すべてのアプリへの転送を許可します。</li><li>**[なし]**:他のポリシーで管理されているアプリを含め、アプリへのデータ転送を許可しません。</li><li> **ポリシーで管理されているアプリ**:他のポリシーで管理されているアプリへの転送のみを許可します。</li><li>**Policy managed apps with OS sharing\(ポリシーで管理されているアプリと OS の共有\)**:他のポリシーで管理されているアプリへのデータ転送、および登録されたデバイス上の他の MDM で管理されているアプリへのファイル転送のみを許可します。<p><p>**注:** _値 **[Policy managed apps with OS sharing]\(ポリシーで管理されているアプリと OS の共有\)** は、MDM に登録されているデバイスのみに適用されます。登録されていないデバイスを使用するユーザーをこの設定の対象にした場合、値 **[ポリシーで管理されているアプリ]** の動作が適用されます。_<p><p></li><li>**Policy managed apps with Open-In/Share filtering (ポリシーで管理されているアプリとオープンイン/共有フィルター)**:他のポリシーで管理されているアプリへの転送のみを許可し、[OS Open-in/Share]\(OS オープンイン/共有\) ダイアログをポリシーで管理されているアプリだけが表示されるようにフィルター処理します。<p><p>**注:**  _**[Open-In/Share]\(オープンイン/共有\)** ダイアログのフィルタリングを構成するには、ファイル/ドキュメント ソースとして機能するアプリと、このファイル/ドキュメントを開き、Intune SDK for iOS バージョン 8.1.1 以降をインストールできるアプリの両方が必要です。_ <p><p></li></ul><br>さらに、**[ポリシーで管理されているアプリ]** または **[なし]** に設定すると、Spotlight 検索を使用してアプリ内のデータを検索できる iOS 9 の機能がブロックされます。 <p><p>このポリシーは、iOS ユニバーサル リンクにも該当する場合があります。  一般的な Web リンクは、**[Intune Managed Browser でアプリ リンクを開く]** ポリシー設定によって管理されます。 <p> Intune でデータ転送先として既定で許可される可能性のある除外対象アプリとサービスがいくつかあります。 さらに、Intune アプリをサポートしていないアプリへのデータ転送を許可する必要がある場合、独自の例外を作成できます。 詳細については、「[データ転送の除外対象](#data-transfer-exemptions)」を参照してください。  | **すべてのアプリ**   |
| <ul><ui> **除外するアプリを選択します** | このオプションは、上記のオプションで *[ポリシーで管理されているアプリ]* を選択した場合に使用できます。   |   |
| **他のアプリからデータを受信** | このアプリにデータを転送できるアプリを以下のように指定します。 <ul><li>**すべてのアプリ**:すべてのアプリからのデータ転送を許可します。</li><li>**[なし]**:他のポリシーで管理されているアプリを含め、アプリからのデータ転送を許可しません。</li><li>**ポリシーで管理されているアプリ**:他のポリシーで管理されているアプリからの転送のみを許可します。</li><li>**受信した組織のデータを持つすべてのアプリ**:すべてのアプリからのデータ転送を許可します。 ユーザー ID が設定されていないすべての受信データを、自分の組織からのデータとして扱います。 データは、`IntuneMAMUPN` の設定で定義されている MDM 登録ユーザーの ID でマークされます。<p><p>**注:** _値 **[受信した組織のデータを持つすべてのアプリ]** は、MDM に登録されているデバイスのみに適用されます。登録されていないデバイスを使用するユーザーをこの設定の対象にした場合、値 **[Any apps]\(任意のアプリ\)** の動作が適用されます。_</li></ul> 一部の除外対象アプリとサービスは、Intune でデータ転送元として許可される可能性があります。 アプリとサービスの完全な一覧については、「[データ転送の除外対象](#data-transfer-exemptions)」をご覧ください。 登録されていない iOS デバイス上にある、複数 ID の MAM 対応のアプリケーションでは、このポリシーは無視され、すべての受信データが許可されます。<br><br> | **すべてのアプリ**    |
| **組織データのコピーを保存** | このアプリで *[名前を付けて保存]* オプションの使用を無効にするには、**[ブロック]** を選択します。 *[名前を付けて保存]* の使用を許可する場合は、**[許可]** を選択します。 <br><br>**注:** *この設定は、Microsoft Excel、OneNote、Outlook、PowerPoint、および Word でサポートされています。サード パーティ アプリと LOB アプリでもサポートされている場合があります*。 <br><br> *[ブロック]* に設定した場合、*[選択したサービスにユーザーがコピーを保存することを許可]* の設定を構成できます。   | <br><br> **許可**   |
| <ul><ui> **選択したサービスにユーザーがコピーを保存することを許可** | ユーザーは、選択したサービス (OneDrive for Business、SharePoint、ローカル ストレージ) に保存できます。 他のすべてのサービスはブロックされます。| **選択済み 0**  |
| **他のアプリとの間で切り取り、コピー、貼り付けを制限する** | このアプリで切り取り、コピー、および貼り付け操作をいつ使用できるようにするかを指定します。 次の中から選択します。 <ul><li>**ブロック**:このアプリと他のアプリの間で、切り取り、コピー、および貼り付け操作を許可しません。</li><li>**ポリシーで管理されているアプリ**:このアプリと他のポリシーで管理されているアプリ間で、切り取り、コピー、および貼り付け操作を許可します。</li><li>**貼り付けを使用する、ポリシーで管理されているアプリ**:このアプリと他のポリシーで管理されているアプリ間で切り取りまたはコピーを許可します。 任意のアプリからこのアプリへのデータの貼り付けを許可します。</li><li>**任意のアプリ**:このアプリに対する切り取り、コピー、貼り付けに制限はありません。</ul> | **任意のアプリ**   |



### <a name="encryption"></a>暗号化
| Setting | 使用する方法 | 既定値 |
|------|----------|-------|
| **組織データを暗号化** | [必要] を選択すると、このアプリ内の職場や学校のデータに対する暗号化が有効になります。  デバイスのロック中にアプリ データを保護するために、Intune では iOS デバイスの暗号化が強制されます。  アプリケーションでは、必要に応じて、Intune アプリ SDK の暗号化を使ってアプリ データを暗号化できます。  Intune アプリ SDK では iOS の暗号化方法が使われ、アプリ データに 128 ビット AES 暗号化が適用されます。 <br><br> この設定を有効にする場合、状況によっては、ユーザーが自分のデバイスにアクセスするために PIN をセットアップして使用する必要があります。 デバイスの PIN がなく、暗号化が必要な場合、"組織により、このアプリケーションにアクセスするには、最初にデバイス PIN を有効にする必要があります" というメッセージと共に、ユーザーは PIN を設定するよう求められます。 <br><br> FIPS 140-2 認定済みまたは FIPS 140-2 認定保留中の iOS 暗号化モジュールについては、[Apple の公式ドキュメント](https://support.apple.com/en-us/HT202739)をご覧ください。 | **必要**  |


### <a name="functionality"></a>機能
| Setting | 使用する方法 | 既定値 |
|------|----------|-------|
| **アプリとネイティブ連絡先アプリを同期** |  **[無効にする]** を選択すると、アプリでデバイス上のネイティブ連絡先アプリにデータを保存できなくなります。 **[有効にする]** を選択した場合は、アプリでデバイス上のネイティブ連絡先アプリにデータを保存できます。 <br><br>選択的ワイプを実行し、アプリから職場または学校のデータを削除すると、アプリからネイティブ連絡先アプリに直接同期されている連絡先が削除されます。 ネイティブ アドレス帳から別の外部ソースに同期された連絡先はワイプできません。 現在、これは Microsoft Outlook アプリにのみ適用されます。   | **有効化**  |
| **組織データを出力する** | **[無効にする]** を選択すると、アプリで職場または学校のデータを印刷できなくなります。   | **有効化**  |
| **ポリシーで管理されているブラウザーで Web コンテンツを共有する** | ポリシーで管理されているアプリケーションから Web コンテンツ (http/https リンク) をどのように開くか指定します。 次の中から選択します。 <ul><li>**ポリシーで管理されているブラウザー**:ポリシーで管理されているブラウザーでのみ Web コンテンツを開くことを許可します。</li><li>**任意のアプリ**:任意のアプリで Web リンクを許可します </li></ul> デバイスの管理に Intune を使用している場合は、「[Managed Browser のポリシーを使用したインターネット アクセスを Microsoft Intune で管理する](app-configuration-managed-browser.md)」を参照してください。<br><br>**ポリシーで管理されているブラウザー**<br>ポリシーで管理されているブラウザーを複数デプロイした場合、1 つのみが起動されます。  まず Intune Managed Browser、次いで Microsoft Edge が起動されます。<p>ポリシーで管理されているブラウザーが必要であるにもかかわらず、インストールされていない場合、エンド ユーザーには Intune Managed Browser のインストールが求められます。<p>ポリシーで管理されているブラウザーが必要な場合、iOS ユニバーサル リンクは **[アプリで他のアプリへのデータ転送を許可する]** ポリシー設定で管理されます。 <p>**Intune デバイスの登録**<br>デバイスの管理に Intune を使用している場合は、「Microsoft Intune のポリシーで保護されたブラウザーを使用してインターネット アクセスを管理する」をご参照ください。 <p>**ポリシーで管理されている Microsoft Edge**<br>モバイル デバイス (iOS と Android) 向けの Microsoft Edge ブラウザーが、Intune アプリ保護ポリシーをサポートします。 企業の Azure AD アカウントで Microsoft Edge ブラウザー アプリケーションにサインインしたユーザーは、Intune によって保護されます。 Microsoft Edge ブラウザーは Intune SDK を統合し、そのデータ保護ポリシーをすべてサポートしています。ただし、例外として次が禁止されます。<br><ul><li>**名前を付けて保存**:Microsoft Edge ブラウザーでは、クラウド ストレージ プロバイダー (OneDrive など) にアプリ内で直接接続を追加することをユーザーに許可していません。</li><li>**連絡先の同期**:Microsoft Edge ブラウザーは、ネイティブの連絡先一覧に保存しません。</li></ul><br>**注**:<br>Intune SDK では、ターゲット アプリがブラウザーであるかどうかは判別できません。 iOS デバイスでは、その他の管理されているブラウザー アプリは許可されていません。    | **未構成**  |
| **サード パーティのキーボード** | **[無効にする]** を選択すると、マネージド アプリケーションではサードパーティ製のキーボードが使えなくなります。 <br><br>この設定が有効になっていると、1 回限りのメッセージがユーザーの元に届き、サードパーティ製キーボードの使用が禁止されていることが伝えられます。 このメッセージは、キーボードの使用を要求する組織データをユーザーが初めて操作したときに表示されます。 マネージド アプリケーションの使用時は標準の iOS キーボードのみ利用できます。その他のキーボード オプションはすべて無効になります。 アンマネージド アプリケーションでサードパーティ製キーボードを使用する場合、この設定は適用されません。 | **有効化** |



> [!NOTE]  
> データ保護の設定では、iOS デバイスの Apple Managed Open In 機能は制御されません。 Apple Managed Open In を使うには、「[Microsoft Intune を使用して iOS アプリ間のデータ転送を管理する](data-transfer-between-apps-manage-ios.md)」をご覧ください。

## <a name="data-transfer-exemptions"></a>データ転送の除外対象

特定のシナリオにおいて Intune アプリ保護ポリシーによってデータ転送が許可される可能性のある除外対象のアプリとプラットフォーム サービスがいくつかあります。 このリストは、セキュリティで保護された生産性向上に役立つと考えられるサービスとアプリを表しており、変更される可能性があります。

| アプリ/サービス名 | 説明 |
| ---- | --- |
|<code>tel; telprompt</code> | ネイティブの電話アプリ |
| <code>skype</code> | Skype |
| <code>app-settings</code> | デバイスの設定 |
| <code>itms; itmss; itms-apps; itms-appss; itms-services</code> | アプリ ストア |
| <code>calshow</code> | ネイティブのカレンダー |


## <a name="access-requirements"></a>アクセス要件

| Setting | 使用する方法 | 既定値 |
|------|----------|-------|
| **アクセスに PIN を使用** | **[必要]** を選択すると、このアプリを使用する際に PIN が要求されます。 ユーザーは、職場または学校のコンテキストでアプリを初めて実行するときに、この PIN のセットアップを求められます。 PIN は、オンラインまたはオフラインで作業しているときに適用されます。    <br><br> PIN 強度について、次の設定を構成します。   | **必要** |
| <ul><ui> **PIN の種類** | アプリ保護ポリシーが適用されているアプリにアクセスする前に、数値またはパスコードのどちらの種類の PIN を入力する必要があるかを設定します。 数値の場合は数字だけですが、パスコードの場合は少なくとも 1 つのアルファベット**または**少なくとも 1 つの特殊文字で定義できます。  <br><br> **注:** *パスコードの種類を構成するには、アプリに Intune SDK バージョン 7.1.12 以降が必要です。数値型には、Intune SDK バージョンの制限はありません。許可されている特殊文字には、iOS 英語キーボードの特殊文字と記号が含まれます*。  | **[数字]**  |
| <ul><ui> **単純な PIN** | **[許可]** を選択すると、ユーザーは 1234、1111、abcd、aaaa などの単純な PIN シーケンスを使えるようになります。 **[ブロック]** を選択すると、単純なシーケンスは使用できなくなります。 <br><br>**注**:*パスコードの種類として PIN が構成され、[単純な PIN を許可する] が [はい] に設定されている場合、少なくとも 1 つの文字 **または** 少なくとも 1 つの特殊文字を PIN に使用する必要があります。パスコードの種類として PIN が構成され、[単純な PIN を許可する] が [いいえ] に設定されている場合、少なくとも 1 つの数字 **および** 1 つの文字、 **さらに** 少なくとも 1 つの特殊文字を PIN に使用する必要があります。*    |**許可**  |
| <ul><ui> **PIN の最小長を選択** | PIN シーケンスの最小桁数を指定します。  | **4**  |
|  <ul><ui> **アクセスに PIN ではなく Touch ID を使用 (iOS 8 以降)** | **[許可]** を選択すると、アプリへのアクセスに、PIN の代わりに [Touch ID](https://support.apple.com/HT201371) を使用できるようになります。    | **許可**  |
|  <ul><ui> <ul><ui> **タイムアウト後は PIN で Touch ID をオーバーライドする** |  この設定を使用するには、**[必要]** を選択し、非アクティブ タイムアウトを構成します。  |**必要**  |
|  <ul><ui> <ul><ui> **タイムアウト (非アクティブ分数)** | 時間を分単位で指定します。この時間を過ぎると、指紋の代わりに PIN が使用されます。  |**30**  |
|  <ul><ui> **アクセスに PIN ではなく Face ID を使用 (iOS 11 以降)** | **[許可]** を選択すると、iOS デバイスで顔認証技術を使用したユーザー認証ができるようになります。 許可すると、Face ID 対応デバイスでは Face ID を使用してアプリにアクセスする必要があります。    | **許可**  |
|  <ul><ui>**PIN をリセットするまでの日数** | **[はい]** を選択すると、ユーザーは設定された期間の経過後にアプリの PIN を変更する必要があります。  <br><br>*[はい]* に設定した場合は、PIN のリセットが要求されるまでの日数を構成します。 |**いいえ**  |  
|  <ul><ui> <ul><ui> **日数** | PIN のリセットが要求されるまでの日数を構成します。  |**0**  |
|  <ul><ui>**デバイスの PIN が設定されている場合のアプリ PIN** | ポータル サイトが構成されている登録済みデバイスでデバイス ロックが検出された場合にアプリの PIN を無効にするには、**[無効にする]** を選択します。<br><br> **注:** *アプリに Intune SDK バージョン 7.0.1 以降が必要です*。  <br><br>iOS デバイスでは、ユーザーが PIN の代わりに [Touch ID](https://support.apple.com/HT201371) または [Face ID](https://support.apple.com/HT208109) を使って身元を証明できるようにすることができます。 Intune は、[LocalAuthentication](https://developer.apple.com/documentation/localauthentication/) API を使って、Touch ID と Face ID によりユーザーを認証します。 Touch ID と Face ID については、「[iOS Security Guide](https://www.apple.com/business/docs/iOS_Security_Guide.pdf)」(iOS セキュリティ ガイド) をご覧ください。  <br><br> ユーザーが職場または学校のアカウントでこのアプリを使用しようとすると、PIN を入力する代わりに指紋識別と顔識別を求められます。 この設定を有効にすると、会社または学校のアカウントの使用中には、使用中のアプリ一覧のプレビュー画像はぼやけます。  |  **有効化** |  
| **アクセスに職場または学校アカウントの資格情報を使用** | **[必要]** を選択すると、ユーザーは、アプリへのアクセスに、PIN を入力する代わりに職場または学校のアカウントでのサインインが求められます。 これを **[必要]** に設定し、PIN または生体認証プロンプトが有効になっている場合は、会社の資格情報と、PIN または生体認証プロンプトの両方が表示されます。  | **必要なし** |
| **(非アクティブ分数) 後にアクセス要件を再確認する** | アプリのユーザーがもう一度アクセス要件を指定するように要求されるまでに経過する必要がある、非アクティブな時間を表す分数を構成します。 <br><br> たとえば、管理者がポリシーで PIN をオンにしてルート化されたデバイスをブロックする、ユーザーが Intune で管理されているアプリを開く、PIN を入力しなければならない、およびルート化されていないデバイスでアプリを使用していなければならないなどです。 この設定を使用する場合、ユーザーはすべての Intune で管理されているアプリで、構成されている値と同じ期間、PIN を入力したり、別のルート検出チェックを行ったりする必要はありません。  <br><br>**注:** *iOS では、 **同じ公開元** のすべての Intune 管理対象アプリで PIN が共有されます。デバイスで、アプリがフォアグラウンドを離れると、特定の PIN の PIN タイマーがリセットされます。この設定で定義されているタイムアウトの間、PIN を共有する Intune 管理対象アプリで、PIN を入力する必要はありません。このポリシー設定の形式では、正の整数がサポートされます*。     | **30** |

| Setting | 使用方法 |  
|------|------| 
| **[アクセスのために PIN を要求する]** | **[はい]** を選択すると、このアプリを使用する際に PIN が要求されます。 ユーザーは、職場または学校のコンテキストでアプリを初めて実行するときに、この PIN のセットアップを求められます。 PIN は、オンラインまたはオフラインで作業しているときに適用されます。  <br><br> 既定値 = **はい**。 <br><br> PIN 強度について、次の設定を構成します。 <br><br> <ul><li>**種類の選択**:アプリ保護ポリシーが適用されているアプリにアクセスする前に、数値またはパスコードのどちらの種類の PIN を入力する必要があるかを設定します。 数値の場合は数字だけですが、パスコードの場合は少なくとも 1 つのアルファベット**または**少なくとも 1 つの特殊文字で定義できます。  <br><br> _**注:** パスコードの種類を構成するには、アプリに Intune SDK バージョン 7.1.12 以降が必要です。数値型には、Intune SDK バージョンの制限はありません。許可されている特殊文字には、iOS 英語キーボードの特殊文字と記号が含まれます。_  <br><br> 既定値は **[数値]** です。  </li></ul> <br> <ul><li>**単純な PIN を許可する**:**[はい]** を選ぶと、ユーザーは 1234、1111、abcd、aaaa などの単純な PIN シーケンスを使えるようになります。 **[いいえ]** を選択すると、単純なシーケンスは使用できなくなります。 <br><br>**注**:_パスコードの種類として PIN が構成され、[単純な PIN を許可する] が [はい] に設定されている場合、少なくとも 1 つの文字 **または** 少なくとも 1 つの特殊文字を PIN に使用する必要があります。パスコードの種類として PIN が構成され、[単純な PIN を許可する] が [いいえ] に設定されている場合、少なくとも 1 つの数字 **および** 1 つの文字、 **さらに** 少なくとも 1 つの特殊文字を PIN に使用する必要があります。_   <br><br> 既定値 = **はい**。  </li></ul> <br> <ul><li>**PIN の長さ**:PIN シーケンスの最小桁数を指定します。 <br><br>既定値 = **4**。</li></ul> </li></ul> <br> <ul><li>**PIN の代わりに指紋を許可する (iOS 8.0 以降):** **[はい]** を選択すると、アプリへのアクセスに、PIN の代わりに [Touch ID](https://support.apple.com/HT201371) を使用できるようになります。  <br><br> 既定値 = **はい**。 <br><br><ul><li>**[タイムアウト後は PIN で Touch ID をオーバーライドする]**:この設定を使用するには、**[はい]** を選択し、非アクティブ タイムアウトを構成します。 <br><br>既定値 = **いいえ**。 </li></ul> <br> <ul><li>**[タイムアウト (非アクティブ分数)]**:時間を分単位で指定します。この時間を過ぎると、指紋の代わりにパスコード、数値のいずれかの PIN (構成のとおり) が使用されます。 </li></ul></li></ul> <br> <ul><li> **PIN の代わりに顔認識を許可する (iOS 11+)**:**[はい]** を選択すると、アプリへのアクセスに、PIN の代わりに [Face ID](https://support.apple.com/HT208109) を使用できるようになります。     <br><br>_**注:** 顔認識を構成するには、アプリに Intune SDK バージョン 7.1.19 以上が必要です。_ <br><br>既定値 = **はい**。 ユーザーは、職場アカウントを使ってアプリにアクセスするときに、顔の識別情報を提供するように求められます。</li></ul>  </li></ul> <br> <ul><li>**デバイス PIN が管理されている場合にアプリ PIN を無効にする**:ポータル サイトが構成されている登録済みデバイスでデバイス ロックが検出された場合にアプリの PIN を無効にするには、**[はい]** を選択します。<br><br> _**注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。_  <br><br> 既定値 = **いいえ**。 </li></ul> <br> iOS デバイスでは、ユーザーが PIN の代わりに [Touch ID](https://support.apple.com/HT201371) または [Face ID](https://support.apple.com/HT208109) を使って身元を証明できるようにすることができます。 Intune は、[LocalAuthentication](https://developer.apple.com/documentation/localauthentication/) API を使って、Touch ID と Face ID によりユーザーを認証します。 Touch ID と Face ID については、「[iOS Security Guide](https://www.apple.com/business/docs/iOS_Security_Guide.pdf)」(iOS セキュリティ ガイド) をご覧ください。  <br><br> ユーザーが職場または学校のアカウントでこのアプリを使用しようとすると、PIN を入力する代わりに指紋識別と顔識別を求められます。 この設定を有効にすると、会社または学校のアカウントの使用中には、使用中のアプリ一覧のプレビュー画像はぼやけます。  |  
| **[アクセスには会社の資格情報が必要]** | **[はい]** を選択すると、ユーザーは、アプリへのアクセスに、PIN を入力する代わりに職場または学校のアカウントでのサインインが求められます。 これを **[はい]** に設定し、PIN または生体認証プロンプトが有効になっている場合は、会社の資格情報と、PIN または生体認証プロンプトの両方が表示されます。 <br><br> 既定値 = **いいえ**。 |
| **[(分数) 後に、アクセス要件を再確認する]** | 次の設定を構成します。 <br><br><ul><li>**タイムアウト**:(ポリシーで前に定義した) アクセス要件が再確認されるまでの時間 (分)。 たとえば、管理者がポリシーで PIN をオンにしてルート化されたデバイスをブロックする、ユーザーが Intune で管理されているアプリを開く、PIN を入力しなければならない、およびルート化されていないデバイスでアプリを使用していなければならないなどです。 この設定を使用する場合、ユーザーはすべての Intune で管理されているアプリで、構成されている値と同じ期間、PIN を入力したり、別のルート検出チェックを行ったりする必要はありません。  <br><br> 既定値 = **30 分**  <br><br>_**注:** iOS では、**同じ公開元**のすべての Intune 管理対象アプリで PIN が共有されます。デバイスで、アプリがフォアグラウンドを離れると、特定の PIN の PIN タイマーがリセットされます。この設定で定義されているタイムアウトの間、PIN を共有する Intune 管理対象アプリで、PIN を入力する必要はありません。このポリシー設定の形式では、正の整数がサポートされます。_    <br><br></li>

> [!NOTE]
> [アクセス] セクションで同じアプリとユーザーの組み合わせに対して構成された複数の Intune アプリ保護設定が iOS 上でどのように動作するかについては、[Intune MAM についてよく寄せられる質問](https://docs.microsoft.com/intune/mam-faq#app-experience-on-ios)に関するページおよび「[Intune でアプリ保護ポリシーのアクセス アクションを利用し、データを選択的にワイプする](app-protection-policies-access-actions.md)」を参照してください。

## <a name="conditional-launch"></a>条件付き起動
条件付き起動設定を構成し、アクセス保護ポリシーのサインイン セキュリティ要件を設定します。 

既定では、値とアクションが事前構成された設定がいくつか提供されます。 *[OS の最小バージョン]* など、一部の設定を削除できます。 **[1 つ選んでください]** ドロップダウンから追加の設定を選択することもできます。 

| Setting | 使用方法 |  
|---------|------------| 
| **OS の最小バージョン** | このアプリを使用するための最小 iOS オペレーティング システムを指定します。 *"アクション"* に含まれている項目: <br><ul><li>**[警告]** - デバイスの iOS バージョンが要件を満たさない場合、通知が表示されます。 この通知は閉じることができます。 <br><br> </li></ul> <ul><li>**[アクセスのブロック]** - デバイスの iOS バージョンがこの要件を満たさない場合、アクセスがブロックされます。</li></ul> <ul><li>**[データのワイプ]** - アプリケーションに関連付けられているユーザー アカウントがデバイスからワイプされます。  </li></ul> </li></ul> _**注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。_ |
| **PIN の最大試行回数** | PIN の入力試行回数を指定します。成功せずにこの回数を超えると、構成されているアクションが実行されます。 このポリシー設定の形式は、正の整数をサポートします。 *"アクション"* に含まれている項目: <br><ul><li>**[PIN のリセット]** - ユーザーは自分の PIN をリセットする必要があります。</li></ul> <ul><li>**[データのワイプ]** - アプリケーションに関連付けられているユーザー アカウントがデバイスからワイプされます。  </li></ul></li></ul> 既定値 = **5** |
| **オフラインの猶予期間** | MAM アプリをオフラインで実行できる時間 (分)。 アプリのアクセス要件を再確認するまでの時間 (分) を指定します。 *"アクション"* に含まれている項目: <br><ul><li>**[アクセスのブロック (分)]**: MAM アプリをオフラインで実行できる時間 (分)。 アプリのアクセス要件を再確認するまでの時間 (分) を指定します。 構成された期間が過ぎると、ネットワーク アクセスが利用可能になるまで、職場や学校のデータへのアクセスがアプリによってブロックされます。 このポリシー設定の形式は、正の整数をサポートします。<br><br>既定値 = **720** 分 (12 時間) </li></ul> <ul><li>**[データをワイプ (日)]** - オフラインでの実行期間がこの日数 (管理者が定義) を超えると、アプリはユーザーに対してネットワークへの接続と再認証を要求します。 ユーザーが正常に認証された場合、引き続きデータにアクセスでき、オフライン間隔がリセットされます。  ユーザーの認証が失敗した場合、アプリはユーザーのアカウントとデータの選択的ワイプを実行します。  選択的ワイプで削除されるデータの詳細については、「[Intune で管理されているアプリから会社のデータをワイプする方法](https://docs.microsoft.com/intune/apps-selective-wipe)」を参照してください。 このポリシー設定の形式は、正の整数をサポートします。 <br><br> 既定値 = **90 日** </li></ul>  このエントリは複数回表示できます。インスタンスごとに異なるアクションがサポートされます。 |
| **脱獄またはルート化されたデバイス** | この設定に設定する値はありません。 *"アクション"* に含まれている項目: <br><ul><li>**[アクセスのブロック]** - このアプリが脱獄またはルート化されたデバイスで実行されないようにします。 ユーザーは引き続き個人のタスクにこのアプリを使用できますが、このアプリの職場または学校のデータにアクセスする場合は別のデバイスを使用する必要があります。</li></ul> <ul><li>**[データのワイプ]** - アプリケーションに関連付けられているユーザー アカウントがデバイスからワイプされます。 </li></ul> |
| **アプリの最小バージョン** | 最小オペレーティング システムの値を指定します。 *"アクション"* に含まれている項目: <br><ul><li>**[警告]** - デバイス上のアプリ バージョンが要件を満たさない場合、通知が表示されます。 この通知は閉じることができます。</li></ul> <ul><li>**[アクセスのブロック]** - デバイスのアプリ バージョンが要件を満たさない場合、アクセスがブロックされます。 </li></ul> <ul><li>**[データのワイプ]** - アプリケーションに関連付けられているユーザー アカウントがデバイスからワイプされます。 </li></ul> </li></ul>   多くの場合、アプリには個別のバージョン管理スキームがあるため、1 つのアプリを対象とした、1 つのアプリの最小バージョンでポリシー (*Outlook バージョン ポリシー*など) を作成します。<br><br> このエントリは複数回表示できます。インスタンスごとに異なるアクションがサポートされます。<br><br> このポリシー設定では、major.minor、major.minor.build、major.minor.build.revision のいずれの形式もサポートされます。||
| **SDK の最小バージョン** | Intune SDK のバージョンの最小値を指定します。 *"アクション"* に含まれている項目: <br><ul><li>**[アクセスのブロック]** - アプリの Intune アプリ保護ポリシー SDK バージョンが要件を満たさない場合、アクセスがブロックされます。 <br> <br> Intune アプリ保護ポリシー SDK に関する詳細については、「[Intune App SDK の概要](app-sdk.md)」をご覧ください。</li></ul> <ul><li>**[データのワイプ]** - アプリケーションに関連付けられているユーザー アカウントがデバイスからワイプされます。 </li></ul>  </li></ul> 多くの場合、アプリには個別のバージョン管理スキームがあるため、1 つのアプリを対象とした、1 つのアプリの最小バージョンでポリシー (*Outlook バージョン ポリシー*など) を作成します。 <br><br> このエントリは複数回表示できます。インスタンスごとに異なるアクションがサポートされます。|
| **デバイス モデル** | このアプリを使用するために必要なデバイスのモデルを指定します。 *"アクション"* に含まれている項目: <br><ul><li>**[指定されたものを許可します (未指定のものはブロック)]** - 指定のデバイス モデルに一致するデバイスのみでアプリを使用できます。 他のデバイス モデルはすべてブロックされます。 </li></ul> <ul><li>**[指定されたものを許可します (未指定のものはワイプ)]** - アプリケーションに関連付けられているユーザー アカウントがデバイスからワイプされます。</li></ul> |



##  <a name="add-ins-for-outlook-app"></a>Outlook アプリ用のアドイン

最近、よく使用されているアプリを電子メール クライアントと統合できるアドインが Outlook for iOS に追加されました。 Outlook 用のアドインは、Web、Windows、Mac、および Outlook for iOS で利用できます。 Intune SDK と Intune アプリ保護ポリシーには、Outlook 用のアドインを管理するためのサポートは含まれていませんが、別の方法でその使用を制限できます。 アドインは Microsoft Exchange を介して管理されるため、Exchange でユーザーに対してアドインがオフになっていない限り、ユーザーは Outlook と管理対象外のアドイン アプリケーションの間でデータとメッセージを共有できます。

エンド ユーザーによる Outlook アドインのアクセスとインストールを禁止する場合は (これは Outlook のすべてのクライアントに影響します)、Exchange 管理センターで役割に対して次の変更を行っていることを確認してください。

- ユーザーが Office ストアのアドインをインストールできないようにするには、ユーザーからマイ マーケットプレース役割を削除します。
- ユーザーがアドインをサイド ローディングできないようにするには、ユーザーからマイ カスタム アプリ役割を削除します。
- ユーザーがすべてのアドインをインストールできないようにするには、ユーザーからマイ カスタム アプリ役割とマイ マーケットプレース役割の両方を削除します。

次の手順は、Office 365、Exchange 2016、Exchange 2013 に適用され、Web、Windows、Mac、およびモバイルの Outlook が対象になります。

- Outlook 用アドインの詳細については、[こちら](https://technet.microsoft.com/library/jj943753(v=exchg.150).aspx)を参照してください。
- Outlook アプリ用のアドインをインストールおよび管理できる管理者とユーザーを指定する方法の詳細については、[こちら](https://technet.microsoft.com/library/jj943754(v=exchg.150).aspx)を参照してください。

##  <a name="linkedin-account-connections-for-microsoft-apps"></a>Microsoft アプリの LinkedIn アカウントの接続

LinkedIn アカウントの接続では、ユーザーは特定の Microsoft アプリ内の LinkedIn パブリック プロファイル情報を表示することができます。 既定で、ユーザーは LinkedIn と Microsoft の職場または学校アカウントを接続して、追加の LinkedIn プロファイル情報を表示するよう選択できます。 

> [!NOTE]
> LinkedIn 統合は現在、米国政府機関の顧客、およびオーストラリア、カナダ、中国、フランス、ドイツ、インド、韓国、イギリス、日本、南アフリカでホストされている Exchange Online メールボックスを使用する組織では利用できません。

Intune SDK と Intune アプリ保護ポリシーには、LinkedIn アカウントの接続を管理するためのサポートは含まれていませんが、別の方法でそれらを管理できます。 組織全体に対して LinkedIn アカウントの接続を無効にすることも、組織内の選択したユーザー グループに対して LinkedIn アカウントの接続を有効にすることもできます。 これらの設定は、すべてのプラットフォーム (Web、モバイル、デスクトップ) 上の Office 365 アプリ間の LinkedIn 接続に影響します。 次の操作を行います。

- Azure portal で、テナントに対する LinkedIn アカウントの接続を有効または無効にします。 
- グループ ポリシーを使用して、組織の Office 2016 アプリに対する LinkedIn アカウントの接続を有効または無効にします。

テナントに対して LinkedIn 統合が有効になっている場合、組織内のユーザーが LinkedIn および Microsoft の職場または学校アカウントを接続したときに、次の 2 つのオプションを使用できます。 

- 両方のアカウント間でデータを共有するためのアクセス許可を付与することができます。 これは、LinkedIn アカウントに Microsoft の職場または学校アカウントとデータを共有するためのアクセス許可を与え、Microsoft の職場または学校アカウントに LinkedIn アカウントとデータを共有するためのアクセス許可を与えることを意味します。 LinkedIn と共有されるデータは、オンライン サービスを離れます。 
- LinkedIn アカウントからのみデータを共有するためのアクセス許可を、Microsoft の職場または学校アカウントに付与することができます

ユーザーがアカウント間でデータを共有することに同意した場合、Office アドインの場合と同様に、LinkedIn 統合では既存の Microsoft Graph API を使用します。 LinkedIn 統合では Office アドインで利用可能な API のサブセットのみを使用し、さまざまな除外をサポートします。


|Microsoft Graph に対するアクセス許可  |説明  |
|---------|---------|
|[人](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#people-permissions)に対する読み取りアクセス許可     |アプリがサインインしたユーザーに関連する人のスコア付きリストを読み取ることを許可します。 このリストには、ローカルの連絡先、ソーシャル ネットワーキングまたは組織のディレクトリからの連絡先、最近 (メールや Skype などで) 連絡した人が含まれる場合があります。         |
|[予定表](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#calendars-permissions)に対する読み取りアクセス許可     |アプリがユーザーの予定表内のイベントを読み取ることを許可します。 サインインしたユーザーの予定表の会議、その時間、場所、および出席者が含まれます。         |
|[ユーザー プロファイル](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#user-permissions)に対する読み取りアクセス許可     |ユーザーがアプリにサインインすることと、アプリがサインインしたユーザーのプロファイルを読み取ることを許可します。 アプリがサインインしたユーザーの基本的な会社情報を読み取ることも許可します。         |
|Subscriptions     |このスコープは利用できず、まだ使用されていません。 Office 365 などの Microsoft アプリとサービスに対する、ユーザーの組織によって提供されるサブスクリプションが含まれます。         |
|インサイト     |このスコープは利用できず、まだ使用されていません。 Microsoft サービスの使用に基づき、サインインしたユーザーのアカウントに関連付けられている関心が含まれます。         |

### <a name="learn-more"></a>詳細情報

- [Microsoft アプリの LinkedIn の情報と機能](https://go.microsoft.com/fwlink/?linkid=850740)について学習します。
- [Office 365 ロードマップ ページ](https://products.office.com/en-US/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc)に示されている LinkedIn アカウント接続のリリースについて学習します。 
- [LinkedIn アカウント接続の構成](https://docs.microsoft.com/azure/active-directory/linkedin-integration)について学習します。
- ユーザーの LinkedIn および Microsoft の職場または学校アカウント間で共有されるデータの詳細については、[職場または学校の Microsoft アプリケーションの LinkedIn](https://www.linkedin.com/help/linkedin/answer/84077) に関するページを参照してください。

