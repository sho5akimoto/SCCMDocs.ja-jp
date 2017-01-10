---
title: "セットアップ ウィザード | System Center Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ffcdf4285d5f182e8d625200989f65c748bc2067
ms.openlocfilehash: 9552ac1b77acfce6a398ec6e74f1be3686ee15a4

---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>セットアップ ウィザードを使用した System Center Configuration Manager サイトのインストール

*適用対象: System Center Configuration Manager (Current Branch)*


ガイド付きユーザー インターフェイスを使用して新しい System Center Configuration Manager サイトをインストールするには、Configuration Manager セットアップ ウィザード (setup.exe) を使用します。 このウィザードは、プライマリ サイトまたは中央管理サイトのインストールをサポートしています。 Configuration Manager の評価版インストールをフル機能のライセンス版インストールに[アップグレード](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md)するときにも、このウィザードを使用します。  ウィザードを使用しない場合は、代わりに[インストール スクリプト](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)を使用して、コマンド ラインからの無人インストールを実行できます。

セカンダリ サイトをインストールするには、Configuration Manager コンソール内からサイトをインストールする必要があります。  セカンダリ サイトは、スクリプトを使用してコマンド ラインからインストールすることはできません。

## <a name="a-namebkmkprimarya-install-a-central-administration-site-or-primary-site"></a><a name="bkmk_primary"></a>  中央管理サイトまたはプライマリ サイトをインストールする
中央管理サイトまたはプライマリ サイトをインストールする場合や、評価版サイトをフル機能のライセンス版 Configuration Manager サイトにアップグレードする場合は、次の手順に従います。   

サイトのインストールを開始する前に、次の記事で詳細を確認してください。
 -  [サイトのインストールの準備](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [サイトをインストールするための前提条件](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

この手順をサイト展開シナリオの一部として実行する場合は、次の手順を使用する前に、このトピックの「[スタンドアロン プライマリ サイトを拡張する](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)」セクションを確認してください。

### <a name="a-namebkmkinstallpria-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a>   プライマリ サイトまたは中央管理サイトをインストールするには

1.  サイトをインストールするコンピューターで、**&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** を実行して **System Center Configuration Manager セットアップ ウィザード**を開始します。  

    > [!NOTE]  
    >  中央管理サイトをスタンドアロン プライマリ サイトにインストールして拡張する場合、または新しい子プライマリ サイトを既存の階層にインストールする場合は、既存のサイトのバージョンに対応するインストール メディア (ソース ファイル) を使用する必要があります。  コンソール内の更新プログラムをインストールした結果、以前にインストールしたサイトのバージョンが変更された場合は、更新したサイトの元のインストール メディアを使用するのではなく、[CD.Latest フォルダー](../../../../core/servers/manage/the-cd.latest-folder.md)にあるソース ファイルを使用してください。  Configuration Manager では、新しいサイトが接続する既存のサイトのバージョンに対応したソース ファイルを使用する必要があります。  

2.  [ **開始する前に** ] ページで [ **次へ**] をクリックします。  

3.  **[はじめに]** ページで、インストールするサイトの種類を選択します。  

     **中央管理サイト** – 新しい階層の最初のサイトとして、またはスタンドアロン プライマリ サイトを拡張するとき。  

    -   選択: **[Configuration Manager 中央管理サイトをインストールする]**  

         この手順の後のステップで、新しい階層の最初のサイトとして中央管理サイトをインストールするか、スタンドアロン プライマリ サイトに中央管理サイトをインストールして拡張するかを選べます。  

     **プライマリ サイト** - 新しい階層の最初のサイトであるスタンドアロン プライマリ サイトとして、または子プライマリとして。  

    -   選択: **[Configuration Manager プライマリ サイトをインストールする]**  

        > [!TIP]  
        >  通常、 **[標準インストール オプションを使用して、スタンドアロンのプライマリ サイトをインストールする]** オプションは、テスト環境にスタンドアロンのプライマリ サイトをインストールする場合にだけ選びます。 このオプションを選んだ場合:  
        >   
        > -   セットアップがサイトをスタンドアロン プライマリ サイトとして自動的に構成する  
        > -   既定のインストール パスを使用する  
        > -   サイト データベースに SQL Server の既定のインスタンスのローカル インストールを使用する  
        > -   サイト サーバー コンピューターに管理ポイントと配布ポイントをインストールする  
        > -   プライマリ サイト サーバーのオペレーティング システムの表示言語が Configuration Manager でサポートされている言語である場合は、英語とその言語でサイトを構成する  

4.  **[プロダクト キー]** ページでの操作:
    - [プロダクト キー] ページで、Configuration Manager を評価版としてインストールするか、製品版としてインストールするかを選びます。  

      -   製品版を選んだ場合は、プロダクト キーを入力し、 **[次へ]**をクリックします。  

      -   評価版を選んだ場合は、 **[次へ]**をクリックします (評価版インストールは、後で完全インストールにアップグレードできます)。  
    - System Center Configuration Manager については、2016 年 10 月リリースのバージョン 1606 基準メディア以降、ソフトウェア アシュアランス契約の有効期限の日付を指定できます。 このページでは、ライセンス契約の**ソフトウェア アシュアランスの有効期限**を通知する便利なアラームとして、この日付を指定できます。 セットアップ時に入力しなかった場合は、後で Configuration Manager コンソール内から指定できます。

      >  [!NOTE]   
      >  Microsoft では、お客様が入力した有効期限の日付を確認していません。また、ライセンスを検証する場合もこの日付を使用しません。  お客様は有効期限を通知するアラームとして、この日付を使用することができます。 Configuration Manager ではオンラインで新しいソフトウェア更新プログラムが提供されていないか定期的に確認します。このような追加の更新プログラムを取得するためにはソフトウェア アシュアランス ライセンスが最新の状態になっている必要があります。このため有効期限を通知するアラーム機能は便利です。    

      詳細については、「[System Center Configuration Manager のライセンスとブランチ](/sccm/core/understand/learn-more-editions)」を参照してください。

5.  **[マイクロソフト ソフトウェア ライセンス条項]** ページで、ライセンス条項を読んで同意します。  

6.  **[必須ライセンス]** ページで、必須ソフトウェアのライセンス条項を読んで同意します。  ソフトウェアがダウンロードされ、必要に応じて、サイト システムまたはクライアントに自動的にインストールされます。 次のページに進む前に、すべてのチェック ボックスをオンにする必要があります。  

7.  **[必須ファイルのダウンロード]** ページで、前提条件の最新の再配布可能ファイルをインターネットからダウンロードするか、以前にダウンロードしたファイルを使用するかを指定します。  

    -   この時点でファイルをダウンロードする場合は、 **[必須ファイルをダウンロードする]** を選び、ファイルを保存する場所を指定します。  

    -   [セットアップ ダウンローダー](../../../../core/servers/deploy/install/setup-downloader.md)を使用して既にファイルをダウンロードしている場合は、**[ダウンロード済みのファイルを使用する]** を選択して、ダウンロード先フォルダーを指定します。  

        > [!TIP]  
        >  前にダウンロードしたファイルを使用する場合は、ダウンロード先フォルダーのパスに、最新バージョンのファイルが含まれていることをご確認ください。  

8.  **[サーバーの言語の選択]** ページで、Configuration Manager コンソールとレポートで使用できるようにする言語を選びます (既定では英語が選ばれています。選択を解除することはできません)。  

9. **[クライアント言語の選択]** ページで、クライアント コンピューターで使用できるようにする言語を選び、すべてのクライアント言語をモバイル デバイス クライアントで有効にするかどうかを指定します (既定では英語が選ばれています。選択を解除することはできません)。  

    > [!IMPORTANT]  
    > 中央管理サイトを使用する場合は、中央管理サイトに構成するクライアント言語に、個々の子プライマリ サイトに構成するすべてのクライアント言語を含めてください。 そのようにする必要がある理由は、配布ポイントからインストールしたクライアントは最上階層のサイトからクライアント言語にアクセスしますが、管理ポイントからインストールしたクライアントは、割り当てられたプライマリ サイトからクライアント言語にアクセスするためです。  

10. **[サイトとインストールの設定]** ページで、インストールする新しいサイトの次の値を指定します。  

    -   **サイト コード:**[階層内の各サイト コードは、一意](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes)であり、3 つの英数字 (A から Z および 0 から 9) で構成されている必要があります。 サイト コードはフォルダー名に使用されるため、Windows で予約されている名前を含め、次のようなコードをサイトに使用しないでください。    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        >  セットアップ時に、指定したサイト コードがまだ使用されていないかどうかや、予約されている名前かどうかは検証されません。  

    -   **サイト名:** 各サイトには、サイトを識別するのに役立つこのフレンドリ名が必要です。  

    -   **インストール先フォルダー:** これは Configuration Manager のインストール フォルダーのパスです。 サイトのインストール後に場所を変更することはできません。また、パスに Unicode 文字を使用することや、パスの末尾にスペースを含めることはできません。  

11. **[サイトのインストール]** ページで、シナリオに一致する次のオプションを使用します。  

    -   **中央管理サイトをインストールする:**  

         **[中央管理サイトのインストール]** ページで、 **[新しい階層に最初のサイトとしてインストールする]**を選び、 **[次へ]** をクリックして続けます。  

    -   **スタンドアロン プライマリ サイトを中央管理サイトがある階層に拡張する:**  

         **[中央管理サイトのインストール]** ページで、 **[既存のスタンドアロン プライマリを 1 つの階層に展開する]**を選び、スタンドアロン プライマリ サイト サーバーの FQDN を指定して、 **[次へ]** をクリックして続けます。  

         新しい中央管理サイトのインストールに使用するメディアが、プライマリ サイトのバージョンに一致する必要があります。  

    -   **スタンドアロン プライマリ サイトをインストールする:**  

         **[プライマリ サイトのインストール]** ページで、**[プライマリ サイトをスタンドアロン サイトとしてインストールする]**を選び、 **[次へ]**をクリックします。  

    -   **子プライマリ サイトをインストールする:**  

         [ **プライマリ サイトのインストール** ] ページで [ **プライマリ サイトを既存の階層に含める**] を選択し、中央管理サイトの FQDN を指定して [ **次へ**] をクリックします。  

12. [データベース情報] ページで、次の情報を指定します。  

    -   **SQL Server 名 (FQDN):** 既定では、これはサイト サーバー コンピューターに設定されます。  

    -   **インスタンス名:** 既定では、これは空白になり、サイト サーバー コンピューターの SQL の既定のインスタンスが使用されます。  

    -   **データベース名:** 既定では、これは CM_&lt;Sitecode\> に設定されます。 別の名前を自由に指定して使用できます。  

    -   **Service Broker ポート:** 既定では、これは既定の SQL Server Service Broker (SSB) ポートである 4022 を使用するように設定されます。このポートは、SQL が他のサイトのサイト データベースと直接通信するために使用されます。  

13. 2 番目の **[データベース情報]** で、サイト データベースの SQL Server データ ファイルと SQL Server ログ ファイルに既定以外の場所を指定できます。  

    -   SQL Server の既定のファイルの場所が指定されます  

    -   既定以外のファイルの場所を指定するオプションは、SQL Server クラスターを使用する場合は使用できません  

    -   前提条件チェッカーでは、既定以外のファイルの場所の空きディスク領域については、チェックは実行されません  

14. **[SMS プロバイダーの設定]** ページで、SMS プロバイダーをインストールするサーバーの FQDN を指定します。  

    -   既定では、サイト サーバーが指定されます。  

    -   サイトのインストールが終わった後で、他の SMS プロバイダーを追加して構成できます  

15. **[クライアント コンピューターの通信設定]** ページで、すべてのサイト システムがクライアントからの HTTPS 通信だけを受け入れるようにするか、サイト システムの役割ごとに通信方法を構成するかを選びます。  

    -   **[すべてのサイト システムの役割でクライアントからの HTTPS 通信のみ受け付ける]**を選んだ場合は、クライアント コンピューターで、クライアント認証用の正しい PKI 証明書が必要になります。 証明書の要件の詳細については、「Configuration Manager での PKI 証明書の要件」を参照してください。  

    > [!NOTE]  
    >  この手順は、プライマリ サイトをインストールする場合にのみ適用されます。 中央管理サイトをインストールする場合は、この手順をスキップします。  

16. [ **サイト システムの役割** ] ページで、管理ポイントまたは配布ポイントをインストールするかどうかを選択します。 セットアップでインストールするように選んだ役割ごとに:  

    -   役割をホストするコンピューターの **FQDN** を入力し、サーバーでサポートするクライアントの接続方法 (HTTP または HTTPS) を選ぶ必要があります。  

    -   前のページで [ **すべてのサイト システム ロールでクライアントからの HTTPS 通信のみ受け付ける** ] を選択した場合は、クライアント接続設定が自動的に HTTPS に構成されています。前のページに戻らないと、この設定を変更することはできません。  

    > [!NOTE]  
    >  この手順は、プライマリ サイトをインストールする場合にのみ適用されます。 中央管理サイトをインストールする場合は、この手順をスキップします。  

    > [!NOTE]  
    >  サイト システムの役割をインストールするために、セットアップでは **[サイト システムのインストール アカウント]**を使用します。 既定では、プライマリ サイトのコンピューター アカウントが使用されます。  このアカウントは、サイト システムの役割をインストールするリモート コンピューターのローカル管理者である必要があります。 このアカウントに必要な権限がない場合は、サイト システムの役割のチェック ボックスをオフにし、サイト システムのインストール アカウントとして使用する他のアカウントを構成した後で Configuration Manager コンソール内からサイト システムの役割をインストールします。  

17. **[使用状況データ]** ページで、Microsoft が収集するデータに関する情報を確認してから、 **[次へ]**をクリックします。  

18. 親プライマリ サイトの **[サービス接続ポイントのセットアップ]** ページは、次の場合にのみセットアップ時に使用できます。  

    -   スタンドアロン プライマリ サイトをインストールする  

    -   中央管理サイトをインストールする  

    > [!NOTE]  
    >  子プライマリ サイトをインストールする場合は、この手順をスキップします (このページは使用できません)。  

     サイト展開シナリオの一部として中央管理サイトをインストールするとき、この役割が既にスタンドアロン プライマリ サイトにインストールされている場合は、スタンドアロン プライマリ サイトからこの役割をアンインストールする必要があります。 この役割のインスタンスは、階層内で 1 つだけ許可されており、階層の最上位サイトでのみ許可されます。  

     **[サービス接続ポイント]** の構成を選んだら、**[次へ]** をクリックします。 (セットアップの完了後、Configuration Manager コンソール内からこの構成を変更できます。)  

19. **[設定の概要]** ページで、選んだ設定を確認し、準備ができたら、 **[次へ]** をクリックして、前提条件チェッカーを起動します。  

20. **[インストールの前提条件チェック]** ページに、特定できた問題が一覧表示されます。  

    -   一覧に問題が表示されている場合は、その問題をクリックして解決方法を確認します。  

    -   サイトのインストールを続ける前に、ステータスが **[失敗]** の各項目を解決する必要があります。 ステータスが **[警告]** の項目は解決することをお勧めしますが、サイトのインストールがブロックされることはありません。  

    -   問題を解決したら、 **[前提条件チェックの実行]** をクリックして、前提条件チェッカーを再実行します。  

     前提条件チェッカーを実行し、ステータスが **[失敗]** の項目がなければ、 **[インストールの開始]** をクリックして、サイトのインストールを開始します。  

    > [!TIP]  
    >  ウィザードで提供されるフィードバックのほかに、インストール先のコンピューターのシステム ドライブのルートにある **ConfigMgrPrereq.log** ファイルを確認すると、前提条件に関する問題についての補足情報を見つけることができます。  インストールの前提条件となる規則のリストと説明については、「[List of Prerequisite Checks for System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)」(System Center Configuration Manager の前提条件チェックのリスト) を参照してください。  

21. **[インストール]** ページに、インストールのステータスが表示されます。 コア サイト サーバーのインストールが完了したら、インストール ウィザードを **閉じる** ことができます。 ウィザードを閉じても、インストールとサイトの初期構成がバックグラウンドで続けられます。  

    -   セットアップが完了する前に Configuration Manager コンソールをサイトに接続できます。 このコンソールは読み取り専用として接続するため、オブジェクトや設定を表示することはできますが、編集することはできません。  

    -   セットアップの完了後は、オブジェクトや設定を編集できるコンソールを接続できます。  


## <a name="a-namebkmkexpanda-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> スタンドアロン プライマリ サイトを拡張する
最初のサイトとしてスタンドアロン プライマリ サイトをインストールした場合は、後から中央管理サイトをインストールすることで、そのサイトを大きな階層に拡張できます。   

スタンドアロン プライマリ サイトを拡張するときに、既存のスタンドアロン プライマリ サイトのデータベースを参照として使用する新しい中央管理サイトをインストールします。 新しい中央管理サイトをインストールした後は、スタンドアロン プライマリ サイトは子プライマリ サイトとして機能します。


-   新しい階層に拡張できるのは、スタンドアロン プライマリ サイトのみです。  

-   特定の階層に拡張できるスタンドアロン プライマリ サイトは 1 つのみです。 このオプションを使用して、追加のスタンドアロン プライマリ サイトを同じ階層に含めることはできません。 代わりに、移行操作を使用して、階層間でデータを移行します。  

-   スタンドアロン サイトを、中央管理サイトを持つ階層に拡張すると、子プライマリ サイトを追加できます。  

-   中央管理サイトを持つ階層からプライマリ サイトを削除するには、プライマリ サイトをアンインストールする必要があります。  

サイトを拡張するには、System Center Configuration Manager セットアップ ウィザードを使用して、新しい中央管理サイトをインストールします。その際は、次の点にご注意ください。  

-   スタンドアロン プライマリ サイトと同じバージョンの Configuration Manager を使用して、中央管理サイトをインストールする必要があります。  

-   セットアップ ウィザードの [はじめに] ページで、中央管理サイトをインストールするオプションを選びます。 セットアップの後の段階で、既存のスタンドアロン プライマリ サイトを拡張するオプションを選びます。  

-   新しい中央管理サイトの [クライアント言語の選択] ページを構成する場合に、拡張するスタンドアロン プライマリ サイトに構成されているのと同じクライアント言語を選ぶ必要があります。  

-   [サイトのインストール] ページで、スタンドアロン プライマリ サイトを拡張するオプションを選びます。  

スタンドアロン プライマリ サイトを拡張するには、この記事の前半の「*[プライマリ サイトまたは中央管理サイトをインストールするには](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*」にある手順に従います。


## <a name="a-namebkmksecondarya-install-a-secondary-site"></a><a name="bkmk_secondary"></a> セカンダリ サイトをインストールする
 Configuration Manager コンソールを使用して、セカンダリ サイトをインストールします。  

-   使用するコンソールが新しいセカンダリ サイトの親サイトとなるプライマリ サイトに接続されていない場合は、サイトをインストールするコマンドが適切なプライマリ サイトにレプリケートされます。  

-   サイトのインストールを開始する前に、ユーザー アカウントに前提条件となる権限があり、新しいセカンダリ サイトをホストするコンピューターがセカンダリ サイト サーバーとして使用するための前提条件をすべて満たしていることを確認します。  

-   セカンダリ サイトをインストールすると、親プライマリ サイトで構成されているクライアント通信用ポートを新しいサイトで使用するように構成されます。  

### <a name="a-namebkmkinstallsecondarya-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> セカンダリ サイトをインストールするには  


1.  Configuration Manager コンソールで、 **[管理]** > **[サイトの構成]** > **[サイト]**の順に移動し、新しいセカンダリ サイトの親プライマリ サイトとなるサイトを選びます。  

2.  **[セカンダリ サイトの作成]** をクリックして、 **セカンダリ サイトの作成ウィザード**を開始します。  

3.  **[開始する前に]** ページで、新しいセカンダリ サイトの親にするプライマリ サイトが表示されていることを確認して、 **[次へ]**をクリックします。  

4.  **[全般]** ページで、次の値を指定します。  

    -   **サイト コード:**階層内の各サイト コードは、一意であり、3 つの英数字 (A から Z および 0 から 9) で構成されている必要があります。 サイト コードはフォルダー名に使用されるため、次のような Windows で予約されている名前をサイトに使用しないでください。  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       >  セットアップ時に、指定したサイト コードがまだ使用されていないかどうかや、予約されている名前かどうかは検証されません。  

    -   **サイト サーバー名:**これは新しいセカンダリ サイトをインストールするサーバーの FQDN です。  

    -   **サイト名:**各サイトには、サイトを識別するのに役立つこのフレンドリ名が必要です。  

    -   **インストール先フォルダー:**これは Configuration Manager のインストール フォルダーのパスです。 サイトのインストール後に場所を変更することはできません。また、パスに Unicode 文字を使用することや、パスの末尾にスペースを含めることはできません。  

    > [!IMPORTANT]  
    >  このページで詳細を指定した後は、 **[概要]** をクリックして、セカンダリ サイトの残りのオプションに既定の設定を使用し、ウィザードの **[概要]** ページに直接移動できます。  
    >   
    >  -   このウィザードの既定の設定を把握しており、それらの設定を使用する場合にのみ、このオプションをご使用ください。  
    >  -   既定の設定を使用すると、境界グループが配布ポイントに関連付けられません。 そのため、セカンダリ サイト サーバーを含む境界グループを構成するまで、クライアントはこのセカンダリ サイトにインストールされている配布ポイントをコンテンツ ソースの場所として使用しません。  

5.  **[インストール ソース ファイル]** ページで、セカンダリ サイト コンピューターがサイト インストール用のソース ファイルを取得する方法を選びます。  

     ネットワークに格納されているソース ファイル、またはセカンダリ サイト コンピューターに格納されているソース ファイルを使用する場合:  

    -   ソース ファイルの場所には、 **Redist** という名前のフォルダーが含まれている必要があります。このフォルダーには、セットアップ ダウンローダーを使用して以前にダウンロードしたすべてのファイルが含まれています。  

    -   **Redist** のいずれかのファイルが利用できない場合は、セカンダリ サイトをインストールできません。  

    -   セカンダリ サイト コンピューターのコンピューター アカウントには、ソース ファイルのあるフォルダーおよび共有の **読み取り** 権限が必要です。  

6.  **[SQL Server の設定]** ページで、使用する SQL Server のバージョンを指定し、関連する設定を構成します。  

    > [!NOTE]  
    >  このページに入力した情報は、インストールを開始するまで検証されません。 操作を続行する前に、設定に間違いがないことを確認してください。  

     **セカンダリ サイト コンピューターに SQL Express のローカル コピーをインストールして構成する場合**  

    -   **SQL Server サービス ポート**: SQL Server Express で使用する SQL Server サービス ポートを指定します。 通常、TCP ポート 1433 に設定しますが、別のポートにすることもできます。  

    -   **SQL Server Broker ポート**: SQL Server Express で使用する SQL Server Service Broker (SSB) ポートを指定します。 通常、TCP ポート 4022 に設定しますが、別のポートにすることもできます。 別のサイトやサービスによって使用されておらず、ファイアウォールでブロックされていない有効なポートを指定してください。  

    > [!IMPORTANT]  
    >  Configuration Manager で SQL Server Express をインストールする場合は、Service Pack なしの SQL Server Express 2012 がインストールされます。  
    >   
    >  -   セカンダリ サイトをサポートするには、インストール後に、Service Pack 2 (以降) をインストールして、SQL Server Express 2012 をアップグレードする必要があります。
    >  -   また、新しいセカンダリ サイトのインストールが完了に失敗したが、最初の SQL Server Express 2012 のインストールが完了した場合、Configuration Manager がセカンダリ サイトのインストールを正常にもう一度試すには、SQL Server Express のインスタンスを更新しておく必要があります。  

     **既存の SQL Server インスタンスを使用する場合**  

    -   **SQL Server の FQDN**: SQL Server コンピューターの FQDN を確認します。 ローカル SQL Server でセカンダリ サイト データベースをホストする必要があります。この設定を変更することはできません。  

    -   **SQL Server インスタンス**: セカンダリ サイト データベースとして使用する SQL Server インスタンスを指定します。 既定のインスタンスを使用する場合は、このオプションを空のままにしてください。  

    -   **ConfigMgr サイト データベース名**: セカンダリ サイト データベースの名前を指定します。  

    -   **SQL Server Broker ポート**: SQL Server で使用する SQL Server Service Broker (SSB) ポートを指定します。 別のサイトやサービスによって使用されておらず、ファイアウォールでブロックされていない有効なポートを指定してください。  

    > [!TIP]  
    >  System Center Configuration Manager でサポートされている SQL Server のバージョンの一覧については、「[Support for SQL Server versions](../../../../core/plan-design/configs/support-for-sql-server-versions.md)」(SQL Server のバージョンのサポート) を参照してください。  

7.  **[配布ポイント]** ページで、セカンダリ サイト サーバーにインストールする配布ポイントの設定を構成します。  

     **必須の設定:**  

    -   **[クライアント デバイスが配布ポイントと通信する方法を指定します]** – HTTP と HTTPS のどちらかを選びます。  

    -   **[自己署名入り証明書を作成するか、PKI クライアント証明書をインポートします]** – 自己署名入り証明書を使用するか (自己署名入り証明書を使用して、Configuration Manager クライアントからコンテンツ ライブラリへの匿名接続を許可することもできます)、PKI 証明書をインポートするかを選びます。  

         証明書は、配布ポイントがステータス メッセージを送信する前に、管理ポイントに対する配布ポイントの認証に使用されます。  

         証明書の要件について詳しくは、「Configuration Manager での PKI 証明書の要件」をご覧ください。  

    **オプションの設定:**  

    -   **[Configuration Manager で必要な場合は IIS をインストールして構成する]** – インターネット インフォメーション サービス (IIS) がまだサーバーにインストールされていない場合に Configuration Manager によってインストールされるようにする場合は、この設定を選びます。 IIS はすべての配布ポイントにインストールされなければなりません。  

        > [!NOTE]  
        >  この設定はオプションですが、配布ポイントを正常にインストールするためには、先に IIS をサーバーにインストールしておく必要があります。  

    -   **[この配布ポイントの BranchCache を有効にして構成する]** •  

    -   **[説明]** – これは配布ポイントを識別するためのわかりやすい説明です。  

    -   **事前設定されたコンテンツ用にこの配布ポイントを有効にする**  

8.  **[ドライブ設定]** ページで、セカンダリ サイトの配布ポイントのドライブ設定を指定します。  

     コンテンツ ライブラリにはディスク ドライブを最大 2 つ、パッケージ共有にはディスク ドライブを 2 つ構成できます。ただし、最初の 2 つが、構成されたドライブの予約領域に達した場合は、Configuration Manager で追加のドライブが使用されます。 [ **ドライブ設定** ] ページで、ディスク ドライブの優先度と各ディスク ドライブに残しておく空き容量を構成します。  

    -   **ドライブの予約領域 (MB)**: ドライブにどの程度空き領域を残しておくかを指定します。空き領域がこの値に達すると、Configuration Manager が別のドライブを選択して、そのドライブへのコピーを続けます。 コンテンツ ファイルは、複数のドライブにまたがって保存されます。  

    -   **コンテンツの場所**:コンテンツ ライブラリとパッケージの共有のコンテンツの場所を指定します。 Configuration Manager は、ドライブの空き領域が **[ドライブの予約領域 (MB)]** で指定した値になるまで、コンテンツの第 1 の場所にコンテンツをコピーします。 既定では、コンテンツの場所は [ **自動**] に設定されています。第 1 の場所は、インストール時に空き領域の最も大きいディスク ドライブに、第 2 の場所は、2 番目に空き領域の大きいディスク ドライブに割り当てられます。 第 1 と第 2 のドライブが予約領域に達すると、Configuration Manager は、使用可能なドライブのうち、空き領域が最も大きなドライブを選択してコピーを続けます。  

9. [ **コンテンツの検証** ] ページで、コンテンツ ファイルの整合性を配布ポイントで検証するかどうかを指定します。  

    -   スケジュールに従ったコンテンツの検証を有効にすると、指定した時刻に Configuration Manager が配布ポイントのコンテンツの検証プロセスを開始し、すべてのコンテンツが検証されます。  

    -   また、 **[コンテンツの検証の優先順位]**を構成することもできます。  

    -   コンテンツの検証プロセスの結果を見るには、Configuration Manager コンソールで、**[監視]** >  **[配布ステータス]** >  **[コンテンツのステータス]** に移動します。 パッケージの種類 (アプリケーション、ソフトウェアの更新パッケージ、ブート イメージなど) ごとにコンテンツが表示されます。  

10. **[境界グループ]** ページで、この配布ポイントを割り当てる境界グループを管理します。  

    -   コンテンツを展開するときに、クライアントがコンテンツ ソースの場所として配布ポイントを使用するには、クライアントは、その配布ポイントに関連付けられた境界グループ内になければなりません。  

    -   これらの境界グループの外にあるクライアントが、優先配布ポイントがない場合に、代わりの配布ポイントをコンテンツのソースの場所として使用できるようにするには、[ **代替のコンテンツ ソースの場所の使用を許可する** ] オプションを選択します。  

     優先配布ポイントの詳細については、「[コンテンツ管理の基本的な概念](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)」を参照してください。  

11. [ **概要** ] ページで設定を確認し、[ **次へ** ] をクリックしてセカンダリ サイトをインストールします。 ウィザードの **[完了]** ページが表示されたら、ウィザードを閉じることができます。 セカンダリ サイトのインストールはバックグラウンドで続けられます。  


### <a name="a-namebkmkverifya-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> セカンダリ サイトのインストール ステータスを確認するには  

1.  Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** に移動します。  

2.  インストールするセカンダリ サイト サーバーを選び、 **[インストール ステータスの表示]**をクリックします。  

    > [!TIP]  
    >  一度に複数のセカンダリ サイトをインストールする場合、一度に 1 つのサイトに対して前提条件のチェックが実行されます。現在のサイトのチェックが完了するまで、次のサイトのチェックは開始されません。  



<!--HONumber=Nov16_HO1-->

