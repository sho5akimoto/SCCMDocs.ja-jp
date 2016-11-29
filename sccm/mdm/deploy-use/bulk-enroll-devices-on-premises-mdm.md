---

title: "デバイスの一括登録 | オンプレミス MDM | System Center Configuration Manager"
description: "System Center Configuration Manager のオンプレミス モバイル デバイス管理を使用して、デバイスの一括登録を自動で行います。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
caps.latest.revision: 13
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 92f30335c412fb1ddf790de7218bb4b704562298


---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager オンプレミス モバイル デバイス管理を使ったデバイスの一括登録の方法

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager のオンプレミス モバイル デバイス管理での一括登録は、ユーザー登録 (デバイスを登録するためにユーザーが資格情報を入力する必要がある) と比較して、より自動化されたデバイスの登録手段です。  一括登録では、登録パッケージを使用して、登録時にデバイスを認証します。 パッケージ (.ppkg ファイル) には、証明書プロファイルが含まれています。また、必要に応じて、登録をサポートするためにデバイスでイントラネット接続が必要な場合には Wi-Fi プロファイルも含まれています。  

 > [!NOTE]  
>  Configuration Manager の現在のブランチでは、次のオペレーティング システムを実行しているデバイスをオンプレミス モバイル デバイス管理で登録することができます。  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(Configuration Manager バージョン 1602 以降\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise

次のタスクでは、オンプレミス モバイル デバイス管理の対象となるコンピューターとデバイスを一括登録する方法について説明します。  

-   [証明書プロファイルの作成](#bkmk_createCert)  

-   [Wi-Fi プロファイルの作成](#CreateWifi)  

-   [登録プロファイルの作成](#bkmk_createEnroll)  

-   [登録パッケージ (ppkg) ファイルの作成](#bkmk_createPpkg)  

-   [パッケージを使用するデバイスの一括登録](#bkmk_getPpkg)  

-   [デバイスの登録の確認](#bkmk_verifyEnroll)  

##  <a name="a-namebkmkcreatecerta-create-a-certificate-profile"></a><a name="bkmk_createCert"></a> 証明書プロファイルの作成  
 登録パッケージの主要なコンポーネントは、証明書プロファイルです。これは登録するデバイスに対し、信頼されたルート証明書を自動的にプロビジョニングするのに使われます。  このルート証明書は、デバイスと、オンプレミス モバイル デバイス管理で必要なサイト システムの役割との間で信頼された通信を行うために必要です。 ルート証明書を使用しないと、登録ポイント、登録プロキシ ポイント、配布ポイント、デバイス管理ポイントのサイト システムの役割をホストするサーバーとの間の HTTPS 接続において、デバイスが信頼されないことになります。  

 オンプレミス モバイル デバイス管理のためのシステムの準備の一環として、登録パッケージの証明書プロファイルで使用できるルート証明書をエクスポートします。 信頼されたルート証明書を取得する手順については、「[Web サーバー証明書と同じルートの証明書をエクスポートする](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)」を参照してください。  

 エクスポートされたルート証明書を使用して、証明書プロファイルを作成します。 手順については、「[System Center Configuration Manager で証明書プロファイルを作成する方法](../../protect/deploy-use/create-certificate-profiles.md)」を参照してください。  

##  <a name="a-namecreatewifia-create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Wi-Fi プロファイルの作成  
 一括登録のために使用されるパッケージのもう一方のコンポーネントは、Wi-Fi プロファイルです。 デバイスによっては、ネットワークの設定がプロビジョニングされるまでは、登録をサポートするために必要なネットワーク接続がない場合があります。 登録パッケージに Wi-Fi プロファイルを含めることは、デバイスのネットワーク接続を確立するための手段となります。  

 Configuration Manager で Wi-Fi プロファイルを作成する場合は、「[System Center Configuration Manager で Wi-Fi プロファイルを作成する方法](../../protect/deploy-use/create-wifi-profiles.md)」の手順に従ってください。  

> [!IMPORTANT]  
>一括登録のために Wi-Fi プロファイルを作成する場合は、次の 2 つの点に注意してください。
>
> - Configuration Manager の現在のブランチでは、オンプレミス モバイル デバイス管理について、次の Wi-Fi セキュリティのみがサポートされます。  
>   
>   - セキュリティの種類: **[WPA2 Enterprise]** または **[WPA2 Personal]**  
>   - 暗号化の種類: **[AES]** または **[TKIP]**  
>   - EAP の種類: **[スマート カードまたは他の証明書]** または **[PEAP]**  
>
>
> - Configuration Manager の Wi-Fi プロファイルにはプロキシ サーバー情報の設定がありますが、デバイスの登録時にプロキシは構成されません。 登録済みデバイスでプロキシ サーバーをセットアップする必要がある場合は、デバイスの登録後に構成アイテムを使用して設定を展開するか、Windows イメージングおよび構成デザイナー (ICD) を使用して 2 番目のパッケージを作成し、一括登録パッケージと共に展開することができます。

##  <a name="a-namebkmkcreateenrolla-create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> 登録プロファイルの作成  
 登録プロファイルでは、デバイスの登録に必要な設定を指定できます。これには、信頼されたルート証明書をデバイスに動的にプロビジョニングする証明書プロファイル、および必要な場合には、ネットワークの設定をプロビジョニングする Wi-Fi プロファイルが含まれます。  

 登録プロファイルを作成する前に、証明書プロファイルおよび (必要であれば) Wi-Fi プロファイルを確実に作成しておきます。 詳細については、「 [証明書プロファイルの作成](#bkmk_createCert) 」および「 [Wi-Fi プロファイルの作成](#CreateWifi)」をご覧ください。  

#### <a name="to-create-an-enrollment-profile"></a>登録プロファイルを作成するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** >**[概要]** >**[会社が所有しているすべてのデバイス]** >**[Windows]** >**[登録プロファイル]** の順にクリックします。  

2.  **[登録プロファイル]** を右クリックし、 **[プロファイルの作成]**をクリックします。  

3.  登録プロファイルの作成ウィザードでプロファイルの名前を入力して、 **[管理機関]** には **[オンプレミス]**を選び、 **[次へ]**をクリックします。  

4.  サイト コードを選んで、 **[次へ]**をクリックします。  

5.  **[イントラネットのみ]**を選んで、デバイスが登録プロセスを開始するために使用する登録プロキシ ポイントを選び、 **[次へ]**をクリックします。  

6.  信頼されたルート証明書 (これは、「 [Create a certificate profile](#bkmk_createCert)」で作成したプロファイルです) を含む証明書プロファイルを選び、 **[次へ]**をクリックします。  

7.  デバイスがイントラネットに接続するために必要なネットワーク設定を含んだ W-Fi プロファイル (これは、「 [Create a Wi-Fi profile](#CreateWifi)」で作成したプロファイルです) を選び、 **[次へ]**をクリックします。  

    > [!NOTE]  
    >  登録パッケージで Wi-Fi プロファイルを使用しない場合は、この手順をスキップします。  

8.  登録プロファイルの設定を確認し、**[次へ]** をクリックします。 **[閉じる]** をクリックしてウィザードを終了します。  

##  <a name="a-namebkmkcreateppkga-create-an-enrollment-package-ppkg-file"></a><a name="bkmk_createPpkg"></a> 登録パッケージ (ppkg) ファイルの作成  
 登録パッケージは、オンプレミス モバイル デバイス管理にデバイスを一括登録するために使用するファイルです。  このファイルは Configuration Manager で作成する必要があります。 Windows イメージングおよび構成デザイナー (ICD) を使用して同じようなパッケージを作成できますが、オンプレミス モバイル デバイス管理で登録するデバイスを始めから終わりまで使用できるのは、Configuration Manager で作成したパッケージだけです。 Windows ICD で作成したパッケージは、登録に必要なユーザー プリンシパル名 (UPN) しか提供できず、実際の登録プロセスを実行できません。  

 登録パッケージを作成するプロセスには、Windows 10 用 Windows アセスメント & デプロイメント キット (ADK) が必要です。  Configuration Manager コンソールを実行しているサーバーで、インストールされている Windows ADK のバージョンが 1511 であることを確認します。 詳しくは、「 [Windows 10 向けキットとツールのダウンロード](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)」の ADK セクションをご覧ください。  

> [!TIP]  
>  Configuration Manager コンソールから登録パッケージを削除すると、デバイスを登録する際に使用できなくなります。 パッケージの削除は、デバイスの一括登録に使用する必要がなくなったパッケージを管理する方法として使用できます。  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>登録パッケージ (ppkg) ファイルを作成するには  

1.  「 [登録プロファイルの作成](#bkmk_createEnroll)」で作成したばかりのプロファイルを右クリックし、 **[エクスポート]**をクリックします。  

2.  	**[参照]**をクリックして、.ppkg ファイルを保存する場所を見つけます。次にパッケージの名前を入力し、 **[保存]**をクリックします。  

3.  パッケージをパスワードで保護するには、 **[パッケージの暗号化]**の横にあるチェック ボックスをクリックします。次に、 **[エクスポート]** をクリックし、エクスポートが完了するまで、約 10 秒間待ちます。  

    > [!NOTE]  
    >  パッケージを暗号化した場合、Configuration Manager は復号化パスワードが示されているメッセージを表示します。 デバイスでパッケージをプロビジョニングする際に必要になるため、パスワード情報を必ず保存してください。  

4.  **[OK]**をクリックします。  

##  <a name="a-namebkmkgetppkga-use-the-package-to-bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a> パッケージを使用するデバイスの一括登録  
 パッケージを使用すると、デバイスを OOBE (out-of-box experience) プロセスを介してプロビジョニングする前または後に、デバイスを登録できます。   登録パッケージを、相手先ブランド供給 (OEM) のプロビジョニング パッケージの一部として含めることもできます。  

 パッケージを一括登録に使用するには、これを物理的に配信する必要があります。 ニーズに応じて、以下のさまざまな方法でデバイスに登録パッケージを配信できます。  

-   ファイル システムからのコピー  

-   メールに添付  

-   近距離無線通信 (NFC) 接続を介したコピー  

-   メモリ カードからのコピー  

-   バーコードのスキャン  

-   テザリングされたデバイスからのコピー  

-   OEM プロビジョニング パッケージに含める  

#### <a name="to-bulk-enroll-a-device"></a>デバイスを一括登録するには  

1.  登録されるデバイスで登録パッケージを検索し (エクスプローラーを使用)、.ppkg ファイルをダブルクリックします。  

2.  [ユーザー アカウント制御] メッセージで **[はい]** をクリックします。  

3.  ダイアログでパッケージが信頼できるソースからのものかどうか確認するよう求められたら、**[はい、追加します]** をクリックします。  

     登録プロセスが開始し、5 分程度かかります。  

4.  **[設定]**を開きます。  

5.    **[アカウント]** > **[作業のアクセス]**が必要とするサイト システムの役割との間で信頼された通信を行うために必要です。 登録が正常に行われると、 **[企業のアプリ]**の下にアカウントが表示されます。  

6.  アカウントをクリックし、**[同期]** をクリックすると、Configuration Manager による管理が開始します。  

##  <a name="a-namebkmkverifyenrolla-verify-enrollment-of-device"></a><a name="bkmk_verifyEnroll"></a> デバイスの登録の確認  
 Configuration Manager コンソールで、デバイスが正常に登録されていることを確認できます。  

-   Configuration Manager コンソールを起動します。  

-    **[資産とコンプライアンス]** > **[概要]** > **[デバイス]**が必要とするサイト システムの役割との間で信頼された通信を行うために必要です。 登録されているデバイスが一覧に表示されます。  



<!--HONumber=Nov16_HO1-->

