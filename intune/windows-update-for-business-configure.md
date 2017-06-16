---
title: "ビジネス設定向けの Windows Update の構成 - Intune | Intune Azure プレビュー | Microsoft Docs"
description: "Intune Azure プレビュー: Intune でビジネス設定向けの Windows Update を構成して、Windows 10 デバイスの更新を制御します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/10/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 08f659cf-715e-4e10-9ab2-1bac3c6f2366
ms.reviewer: coryfe
ms.suite: ems
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: b0bc3e557f303cd80c780634ba47b24405c327e1
ms.contentlocale: ja-jp
ms.lasthandoff: 05/23/2017


---

# <a name="how-to-configure-windows-update-for-business-settings-with-microsoft-intune"></a>Microsoft Intune でビジネス設定向けの Windows Update を構成する方法

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

## <a name="introduction"></a>概要
サービスとしての Windows は、Windows 10 の更新プログラムを提供するための新しい方法です。 Windows 10 以降、すべての新しい機能更新プログラムと品質更新プログラムには、以前の更新プログラムすべての内容が含まれます。 つまり、最新の更新プログラムをインストールしている限り、Windows 10 デバイスが完全に最新の状態であることを把握できます。 以前のバージョンの Windows とは異なり、更新プログラムの一部ではなく全体をインストールすることが必要になります。

Windows Update for Business を使用することで、デバイスのグループに対して個々の更新プログラムを承認する必要がなくなるため、更新プログラム管理エクスペリエンスを簡略化できます。 更新プログラムの展開戦略を構成することで環境内のリスクを引き続き管理でき、さらに Windows Update により更新プログラムが適切なタイミングでインストールされるようになります。 Microsoft Intune では、デバイスでの更新プログラムの設定を構成でき、また更新プログラムのインストールを遅らせることができます。 Intune では更新プログラムは格納されず、更新プログラムのポリシー割り当てのみが格納されます。 デバイスは更新プログラムのため Windows Update に直接アクセスします。**Windows 10 更新プログラム リング**を構成し管理するには Intune を使用します。 更新プログラム リングには、Windows 10 更新プログラムがインストールされるタイミングと方法を構成する設定のグループが含まれています。 たとえば、以下を構成できます。

- **Windows 10 Servicing Branch**: デバイスのグループで Current Branch または Current Branch for Business から更新プログラムを受信するかどうかを指定します。  
- **遅延設定**: デバイスのグループに対して更新プログラムのインストールを遅らせるように更新遅延設定を構成します。 更新プログラムが段階的に展開されるため、その過程を確認できます。
- **一時停止**: 更新プログラムのロールアウト中に問題を検出した場合に、更新プログラムのインストールを延期します。
- **メンテナンス期間**: 更新プログラムをインストールできる時間を構成します。
- **更新プログラムの種類**: インストールされる更新プログラムの種類を選択します  (品質更新プログラム、機能更新プログラム、ドライバーなど)。
- **インストールの動作**: 更新プログラムがインストールされる方法を構成します  (インストール後にデバイスを自動的に再起動するかなど)。
- **ピアのダウンロード**: ピアのダウンロードを構成するかどうかを指定できます。 構成した場合、デバイスで更新プログラムのダウンロードが完了すると、他のデバイスがそのデバイスからの更新プログラムをダウンロードできるようになります。 これにより、ダウンロード処理を高速化できます。

更新プログラム リングを作成したら、これらをデバイスのグループに割り当てます。 更新プログラム リングを使用すると、自社のビジネス ニーズを反映した更新プログラム戦略を立てることができます。 詳しくは、「[Windows Update for Business を使った更新プログラムの管理](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)」をご覧ください。

## <a name="before-you-start"></a>開始する前に

- Windows 10 PC を更新するには、Windows Anniversary Update 付き Windows 10 Pro 以降を実行している必要があります。

- Windows Update では、次の Windows 10 バージョンがサポートされています。
    - Windows 10
    - Windows 10 Team (Surface Hub デバイス向け)

 Windows 10 Mobile および Windows 10 Holographic を実行するデバイスはサポートされていません。

- Windows デバイスで、**[フィードバックと診断]**  >  **[診断と使用状況データ]** が**基本**以上に設定されている必要があります。

    ![診断と使用状況データの Windows 設定](./media/telemetry-basic.png)

    この設定は手動で構成できます。または Windows 10 以降向けの Intune デバイスの制限プロファイルを使用することもできます。 これを行うには、設定 **[全般]**  >  **[診断データの送信]** を**基本**以上に設定します。 デバイスのプロファイルについて詳しくは、「[Microsoft Intune でデバイスの制限設定を構成する方法](device-restrictions-configure.md)」をご覧ください。

- 従来の Intune 管理コンソールには、ソフトウェア更新プログラムの動作を制御する 4 つの設定があります。 これらの設定は、Windows 10 Desktop および Mobile デバイスの全般的な構成ポリシーの一部です。
    - **自動更新を直ちにインストールすることを許可する**
    - **プレリリース機能を有効にする**
    - **インストールを実行する日**
    - **インストールを実行する時間**

  また、従来のコンソールでは、デバイスの構成プロファイルのその他の Windows 10 更新プログラムの数に制限があります。 Azure ポータルへの移行時に、従来の Intune 管理コンソールでこれらのいずれかの設定を構成している場合は、次の操作を実行することを強くお勧めします。

1. 必要な設定を使用して、Azure ポータルで Windows 10 更新プログラム リングを作成します。 Azure ポータルでは **[プレリリース機能を許可する]** 設定はサポートされていません。これは、最新の Windows 10 ビルドに適用できなくなったためです。 更新プログラム リングを作成するとき、他の 3 つの設定と他の Windows 10 更新プログラムの設定を構成できます。

  > [!NOTE]
  > 従来のコンソールで作成した Windows 10 更新プログラム設定は、移行後、Azure ポータルに表示されません。 ただし、これらの設定は引き続き適用されます。 これらのいずれかの設定を移行し、Azure ポータルから移行されたポリシーを編集した場合、これらの設定はポリシーから削除されます。

2. 従来のコンソールで更新プログラムの設定を削除します。 Azure ポータルに移行し、同じ設定を更新プログラム リングに追加した後、従来のポータルの設定を削除して潜在的なポリシーの競合を回避する必要があります。 たとえば、異なる値で同じ設定が構成され、競合が発生した場合、これを簡単に把握することができません。なぜなら、従来のコンソールで構成した設定が Azure ポータルに表示されないためです。

## <a name="how-to-create-and-assign-update-rings"></a>更新プログラム リングを作成して割り当てる方法

1. Azure ポータルにサインインします。
2. **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[ソフトウェア更新プログラム]** を選択します。
4. **[ソフトウェア更新プログラム]** ブレードで、**[管理]**  >  **[Windows 10 Update Rings (Windows 10 更新プログラム リング)]** を選択します。
5. 更新プログラム リングの一覧が表示されたブレードで、**[作成]** を選択します。
6. **[Create Update Ring (更新プログラム リングの作成)]** ブレードで、更新プログラム リングの名前と説明 (省略可能) を指定して、**[設定]** を選択します。
7. **[設定]** ブレードで、以下の情報を構成します。
    - **サービス ブランチ**: デバイスで Windows 更新プログラムを受け取るブランチを設定します (Current Branch または Current Branch for Business)。
    - **Microsoft 更新プログラム**: Microsoft Update のアプリの更新プログラムをスキャンするかどうかを選択します。
    - **Windows ドライバー**: 更新プログラムから Windows Update ドライバーを除外するかどうかを選択します。
    - **自動更新の動作**: 自動更新の動作をどのように管理して更新プログラムをスキャン、ダウンロード、およびインストールするかを選択します。 詳しくは、「[Update/AllowAutoUpdate](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#update-allowautoupdate)」をご覧ください。
    - **品質更新プログラムの遅延期間 (日数)** - 品質更新プログラムを遅延させる日数を指定します。 これらの品質更新プログラムの受信を、リリースから最大 30 日間延期できます。  

      品質更新プログラムは通常、既存の Windows 機能の修正プログラムや機能強化で、(マイクロソフトでは随時リリースできますが) 月の最初の火曜日に公開されるのが一般的です。 入手可能になってから品質更新プログラムの受信を延期するか、またどのくらい延期するかを定義できます。
    - **機能更新プログラムの遅延期間 (日数)** - 機能更新プログラムを遅延させる日数を指定します。 これらの機能更新プログラムの受信を、リリースから最大 180 日間延期できます。

    機能更新プログラムは一般的に Windows の新しい機能です。 **サービス ブランチ**の設定 (**CB** または **CBB**) を構成したら、Windows Update でマイクロソフトから入手可能になってから機能更新プログラムの受信を延期するか、またどのくらい延期するかを定義できます。

    例:  
    **サービス ブランチが CB に設定され、遅延期間が 30 日の場合**: 機能更新プログラム X が Windows Update で 1 月に CB として公開されるとします。 デバイスは 2 月になるまで (30 日後まで) 更新プログラムを受信しません。

    **サービス ブランチが CBB に設定され、遅延期間が 30 日の場合**: 機能更新プログラム X が Windows Update で 1 月に CB として公開されるとします。 4 か月後の 4 月に、機能更新プログラム X が CBB にリリースされたとします。 デバイスは、この CBB リリースの 30 日後に機能更新プログラムを受信し、5 月に更新されます。

    - **配信の最適化** - デバイスが Windows 更新プログラムをダウンロードする方法を選択します。 詳細については、「[DeliveryOptimization/DODownloadMode](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#deliveryoptimization-dodownloadmode)」を参照してください。
8. 完了したら、**[OK]** をクリックして、**[Create Update Ring (更新プログラム リングの作成)]** ブレードで **[作成]** をクリックします。

新しい更新プログラム リングが、更新プログラム リングの一覧に表示されます。

1. リングを割り当てるには、更新プログラム リングの一覧でリングを選択し、[<*リング名*>] タブで **[割り当て]** を選択します。
2. [次へ] タブで **[グループの選択]** を選び、このリングを割り当てるグループを選択します。
3. 選択が完了したら、**[選択]** を選んで割り当てを完了します。



## <a name="update-compliance-reporting"></a>更新プログラムのコンプライアンス対応レポート
Windows 10 更新プログラム ロールアウトを監視するには、更新プログラムのコンプライアンス対応と呼ばれる Operations Management Suite (OMS) の無料のソリューションを使用します。 詳しくは、「[Monitor Windows Updates with Update Compliance (更新プログラムのコンプライアンス対応を使用した Windows Update の監視)](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor)」をご覧ください。 このソリューションを使用すると、更新プログラムのコンプライアンス対応を報告する Intune の対象管理の任意の Windows 10 デバイスに商用 ID を展開できます。

Intune コンソールで、カスタム ポリシーの OMA-URI 設定を使用して商用 ID を構成できます。 詳しくは、「[Microsoft Intune での Windows 10 デバイス向けの Intune ポリシー設定](https://docs.microsoft.com/intune-classic/deploy-use/windows-10-policy-settings-in-microsoft-intune)」を参照してください。   

商用 ID を構成するための OMA-URI (大文字と小文字を区別する) パスは次のとおりです。./Vendor/MSFT/DMClient/Provider/ProviderID/CommercialID

たとえば、**[OMA-URI 設定の追加または編集]** で次の値を使用できます。

- **設定名**: Windows Analytics の商用 ID
- **設定の説明**: Windows Analytics ソリューションの商用 ID を構成
- **データ型**: 文字列
- **OMA-URI** (大文字と小文字を区別): ./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID
- **値**: <*OMS ワークスペースの Windows 利用統計情報に示された GUID を使用*>>

![診断と使用状況データの Windows 設定](./media/commID.png)

<!--
1. Sign into the Azure portal.
2. Choose **More Services** > **Monitoring + Management** > **Intune**.
3. On the **Intune** blade, choose **Software Updates**.
4. On the **Software Updates** blade, choose **Overview**. From here you can see general information about the status of any update rings you assigned.
4. On the **Windows 10 Updates** blade, choose **Monitor** > **Update ring deployment for devices**, **Update ring deployment for users**, or **Per-setting deployment state** to view more detailed information about update ring assignments.
-->





## <a name="how-to-pause-updates"></a>更新プログラムを一時停止する方法
更新プログラムを一時停止したときから最大 35 日間、機能更新プログラムまたは品質更新プログラムのデバイスでの受け取りを一時停止することができます。 最大日数が経過すると、一時停止機能の有効期限が自動的に切れ、デバイスによる Windows Update の該当する更新プログラムのスキャンが開始されます。 このスキャン後に、もう一度更新プログラムを一時停止することもできます。
1. Azure ポータルにサインインします。
2. **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[ソフトウェア更新プログラム]** を選択します。
4. **[ソフトウェア更新プログラム]** ブレードで、**[管理]**  >  **[Windows 10 Update Rings (Windows 10 更新プログラム リング)]** を選択します。
5. 更新プログラム リングの一覧が表示されたブレードで、一時停止するリングを選択し、一時停止する更新プログラムの種類に応じて、**[...]**  >  **[品質更新プログラムの一時停止]** または **[機能更新プログラムの一時停止]** を選択します。

> [!IMPORTANT]
> 一時停止コマンドを発行した場合、デバイスは、次にサービスにチェックインしたときにこのコマンドを受信します。 チェックインする前に、スケジュールされた更新プログラムをインストールする可能性もあります。
> また、一時停止コマンドを発行したときに対象のデバイスが無効になっていると、有効にしたときに、デバイスは Intune でチェックインする前に、スケジュールされた更新プログラムをダウンロードしインストールする場合があります。
