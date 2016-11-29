---
title: "コンテンツ管理の基礎 | System Center Configuration Manager"
description: "System Center Configuration Manager のツールとオプションを使用して、展開するコンテンツを管理します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 27342ef83d877c31f39bc232e3e19e37b78e62da


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのコンテンツ管理の基本的な概念

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager は、アプリケーション、パッケージ、ソフトウェア更新プログラム、およびオペレーティング システム展開として展開するコンテンツを管理するための、信頼性の高いツールとオプションのシステムをサポートしています。  

 展開したコンテンツは、サイト サーバーと配布ポイント サイト システム サーバーの両方に格納されます。 このコンテンツを地点間で転送するときに、大きなネットワーク帯域幅が必要になる場合があります。  コンテンツ管理インフラストラクチャを効果的に計画および使用するには、使用可能なオプションと構成を理解したうえで、ネットワーク環境とコンテンツ展開のニーズに合うように効果的に使用する方法を検討する必要があります。  

コンテンツ管理の主要概念を以下に示します。 概念について追加情報または複雑な情報が必要な場合は、該当する詳細情報へのリンクが示されています。  

## <a name="accounts-used-for-content-management"></a>コンテンツ管理に使用されるアカウント  
 コンテンツ管理では、次のアカウントを使用できます。  

-   **ネットワーク アクセス アカウント** - クライアントが配布ポイントに接続してコンテンツにアクセスするために使用します。 既定では、クライアントは最初にコンピューター アカウントを使用します。  

     このアカウントは、リモート フォレスト内のソース配布ポイントからコンテンツを取得するためにプル配布ポイントによっても使用されます  

-   **パッケージ アクセス アカウント** - 既定では、Configuration Manager は、汎用アクセス アカウントである Users および Administrators に対して配布ポイント上のコンテンツへのアクセスを許可します。 ただし、追加のアクセス許可を構成してアクセスを制限することができます。 「&lt;パッケージ コンテンツにアクセスするためのアカウントの管理\>」をご覧ください。  

-   **マルチキャスト接続アカウント** - オペレーティング システムの展開に使用します。  

これらのアカウントの詳細については、「[コンテンツにアクセスするためのアカウントの管理](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)」を参照してください。

## <a name="bandwidth-throttling-and-scheduling"></a>帯域幅調整とスケジュール  
 調整とスケジュールのどちらも、コンテンツをサイト サーバーから配布ポイントに配布する処理を管理するためのオプションです。 これは、サイト間のファイルベースのレプリケーションに関する帯域幅の制御に似ていますが、直接の関係はありません。  

 詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。

## <a name="binary-differential-replication"></a>バイナリ差分レプリケーション  
 他のサイトまたはリモート配布ポイントに以前に展開したコンテンツの更新を配布するときに使用される帯域幅を小さくするために、配布ポイントの前提条件であるバイナリ差分レプリケーション (BDR) (デルタ レプリケーションとも呼ばれます) が自動的に使用されます。  

 BDR は、コンテンツ ソース ファイルが変更されるたびにすべてのファイルを送信するのではなく、新しいコンテンツまたは変更されたコンテンツのみを再送信することで、配布コンテンツの更新を送信するために使用されるネットワーク帯域幅を最小限に抑えます。  

 バイナリ差分レプリケーションを使用する場合、Configuration Manager は、以前に配布された各コンテンツ セットについて、ソース ファイルに加えられた変更を特定します。  

-   ソース コンテンツのファイルに変更がある場合、Configuration Manager は新しい増分バージョンのコンテンツ セットを作成し、変更されたファイルのみを対象のサイトと配布ポイントにレプリケートします。 ファイルの名前が変更された場合、移動された場合、内容が変更された場合、ファイルは変更されたと見なされます。 たとえば、以前に複数のサイトに配布したオペレーティング システム展開パッケージの 1 つのドライバー ファイルを置き換える場合、変更されたドライバー ファイルのみが、その対象サイトにレプリケートされます。  

-   Configuration Manager は、全体のコンテンツ セットを再送信するまでに、最大 5 つの増分バージョンのコンテンツ セットを保持できます。 5 番目の更新の後で、コンテンツ セットを次に変更すると、Configuration Manager はコンテンツ セットの新しいバージョンを作成します。 Configuration Manager はその後、コンテンツ セットの新しいバージョンを配布し、前のセットとその増分バージョンを置き換えます。 新しいコンテンツ セットが配布された後は、バイナリ差分レプリケーションによって、またソース ファイルの増分の変更がレプリケートされます。  


BDR は、同じ階層内の親サイトと子サイト間でサポートされます。 また、BDR は、同じサイト内のサイト サーバーとその配布ポイント間でサポートされます。 このサポートにプル配布ポイントは含まれますが、クラウドベースの配布ポイントは含まれません。 クラウドベースの配布ポイントは、バイナリ差分アプリケーションによるコンテンツの転送をサポートしません。  

アプリケーションは、常にバイナリ差分レプリケーションを使用します。 パッケージの場合、バイナリ差分レプリケーションはオプションであり、既定では無効です。 パッケージにバイナリ差分レプリケーションを使用するには、各パッケージでこの機能を有効にする必要があります。 有効にするには、新しいパッケージを作成するとき、またはパッケージ プロパティの [ **データ ソース** ] タブを編集するときに、オプション [ **バイナリ差分レプリケーションを有効にする** ] をオンにします。  

## <a name="branchcache"></a>BranchCache  
 BranchCache をサポートし、BranchCache 用に構成されている展開のダウンロードが済んでいるクライアントが、他の BranchCache が有効なクライアントに対するコンテンツ ソースとして機能することを可能にする Windows テクノロジ。  

 たとえば、BranchCache が有効な最初のクライアント コンピューターが、Windows Server 2012 が実行されていて BranchCache サーバーとして構成されている配布ポイントからコンテンツを要求するとき、クライアント コンピューターは、コンテンツをダウンロードしてキャッシュします。  

-   次に、このクライアント コンピューターは、同じサブネット上で BranchCache が有効になっている他のクライアントがコンテンツを利用できるようにします。これらのクライアントも、コンテンツをキャッシュします。  

-   このため、同じサブネット上の後続のクライアントは配布ポイントからコンテンツをダウンロードする必要がなく、その後の転送ではコンテンツは複数のクライアントから配布されます。  





## <a name="windows-pe-peer-cache"></a>Windows PE ピア キャッシュ
新しいオペレーティング システムを System Center Configuration Manager に展開すると、タスク シーケンスを実行しているコンピューターで、配布ポイントからコンテンツをダウンロードするのではなく、Windows PE ピア キャッシュを使用してローカル ピア (ピア キャッシュ ソース) からコンテンツを取得することができます。 これにより、ローカル配布ポイントが存在しないブランチ オフィス シナリオでワイド エリア ネットワーク (WAN) トラフィックが最小限に抑えられます。

詳細については、「[Windows PE ピア キャッシュ](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)」を参照してください。


## <a name="client-locations"></a>クライアントの場所  
 クライアントは、次の場所にあるコンテンツにアクセスします。  

-   **イントラネット** (オンプレミス):  

    -   配布ポイントでは、HTTP または HTTPS を使用できます  

    -   オンプレミスの配布ポイントを使用できない場合、フォールバックとしてクラウドベースの配布ポイントのみを使用します  

-   **インターネット** :  

    -   HTTPS を受け入れるには配布ポイントが必要です  

    -   フォールバックとしてクラウドベースの配布ポイントを使用できます  

-   **ワークグループ**:  

    -   HTTPS を受け入れるには配布ポイントが必要です  

    -   フォールバックとしてクラウドベースの配布ポイントを使用できます  



## <a name="content-library"></a>コンテンツ ライブラリ  
 配布するコンテンツの合計サイズを減らすために Configuration Manager が使用する、コンテンツの単一インスタンス ストア。  

[コンテンツ ライブラリ](../../../core/plan-design/hierarchy/the-content-library.md)の詳細


## <a name="distribution-point"></a>配布ポイント  
 Configuration Manager は、配布ポイントを使用して、クライアント コンピューターで実行するソフトウェアに必要なファイルを格納します。 クライアントは、展開するコンテンツのファイルがダウンロード可能な 1 つ以上の配布ポイントにアクセスできる必要があります。  

 基本的な (特殊化されていない) 配布ポイントは、標準配布ポイントとも呼ばれます。  標準配布ポイントには次の 2 つのバリエーションがあることに注目してください。  

-   **プル配布ポイント** - クライアントが配布ポイントからコンテンツをダウンロードするのと同様に、配布ポイントが他の配布ポイント (ソース配布ポイント) からコンテンツを取得する、配布ポイントのバリエーションの 1 つ。 プル配布ポイントを使用すると、サイト サーバーが各配布ポイントにコンテンツを直接配布する必要があるときに発生する可能性があるネットワーク帯域幅のボトルネックを解消することができます。  [System Center Configuration Manager でのプル配布ポイントの使用](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

-   **クラウドベースの配布ポイント** - Microsoft Azure にインストールされている配布ポイントのバリエーションの 1 つ。 [System Center Configuration Manager でのクラウド ベースの配布ポイントの使用](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  


標準配布ポイントは、調整とスケジュール、PXE、マルチキャスト、事前設定されたコンテンツなどの一連の構成および機能をサポートします。  

-   **スケジュール****帯域幅調整**などのコントロールを使用して、この転送を制御できます。  

-   また、**事前設定コンテンツ**、**プル配布ポイント** などの他のオプションを使用する、または **BranchCache** を活用して、コンテンツの展開時に使用するネットワーク帯域幅の使用量を削減することもできます。  

-   配布ポイントは、オペレーティング システムの展開用の **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** や **[マルチキャスト](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** などのさまざまな構成、または **モバイル デバイス** をサポートする構成をサポートしています。  

 クラウドベースのプル配布ポイントは、これらの同じ構成の多くをサポートしますが、各配布ポイントのバリエーションに固有の制限事項があります。  

## <a name="distribution-point-group"></a>配布ポイント グループ  
 コンテンツ配布の簡素化に役立つ、配布ポイントの論理的グループ。  

 詳細については、「[配布ポイント グループの管理](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)」を参照してください。

## <a name="distribution-point-priority"></a>配布ポイントの優先順位  
 配布ポイントの優先順位値は、以前の展開をその配布ポイントに転送するのに要した時間に基づきます。  

-   これは配布ポイントに割り当てられている自己調整値で、これにより、Configuration Manager は、より短い時間でより多くの配布ポイントにコンテンツを転送できるようになります。  

-   同時に複数の配布ポイントにコンテンツを配布するとき、または 1 つの配布ポイント グループに配布するとき、Configuration Manager は最も優先順位が高い配布ポイントにコンテンツを送信してから、優先順位が低い配布ポイントに同じコンテンツを送信します。  

-   これは、異なるパッケージを転送するときにそのシーケンスを決定するパッケージの配布優先順位を置き換えるものではありません。  


**たとえば、** 配布の優先順位が高いコンテンツを、低い優先順位を持つ配布ポイントに配布する場合は、この配布の優先順位が高いパッケージが、常に、配布の優先順位が低いパッケージより前に転送されます。 配付の優先順位が低いパッケージを、高い優先順位を持つ配付ポイントに配布する場合でも、配付の優先順位が考慮されます。 つまり、Configuration Manager では、配布の優先順位の高いパッケージが配布ポイントに転送されるより前に、それより配布の優先順位の低いパッケージが転送されることはありません。  

> [!NOTE]  
>  また、プル配布ポイントは、優先順位の概念を使用して、ソース配布ポイントのシーケンスを決定しています。  
>   
>  -   配布ポイントにコンテンツを転送するための配布ポイントの優先順位は、プル配布ポイントがソース配布ポイントのコンテンツを検索するときに使用する優先順位とは異なります。  
> -   詳細については、「[System Center Configuration Manager でのプル配布ポイントの使用](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)」を参照してください。  


## <a name="fallback"></a>フォールバック  
 フォールバックの設定は、 **優先配布ポイント** の使用と、クライアントによって使用されるコンテンツ ソースの場所に関連しています。  

-   既定では、クライアントは、優先配布ポイント (クライアントの境界グループに関連付けられている配布ポイント) からのみコンテンツをダウンロードします。  

-   ただし、配布ポイントで **[クライアントがコンテンツの代替ソースの場所としてこのサイト システムを使用することを許可する]** が構成されている場合、優先配布ポイントのいずれかから展開を取得できないすべてのクライアントに対して、この配布ポイントを有効なコンテンツ ソースとしてのみ提供することができます。  


さまざまなコンテンツの場所とフォールバック シナリオの詳細については、[コンテンツ ソースの場所の例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)をご覧ください。

## <a name="network-bandwidth"></a>ネットワークの帯域幅  
 コンテンツを配布するときに使用されるネットワーク帯域幅を管理するために、次のオプションを使用できます。  

-   事前設定されたコンテンツの使用:  ネットワーク経由でコンテンツを配布する際に Configuration Manager に依存することなく配布ポイントにコンテンツを転送するプロセス。  

-   スケジュールと調整の使用: 配布ポイントにコンテンツを配布するタイミングと方法を制御するための構成。  

詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。

## <a name="network-connection-speed-to-content-source"></a>コンテンツ ソースへのネットワーク接続の速度  
 境界グループ内の配布ポイントごとにネットワーク接続速度を構成できます。  

-   クライアントは、配布ポイントに接続するときにこの値を使用します。  

-   ネットワーク接続速度は既定で **[高速]**に構成されていますが、 **[低速]**に設定することもできます。  

-   **ネットワーク接続速度** と展開構成を基に、クライアントが関連付けられた境界グループ内にある場合に、コンテンツを配布ポイントからダウンロードできるかどうかが決定されます。  


さまざまなコンテンツの場所とフォールバック シナリオの詳細については、[コンテンツ ソースの場所の例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)をご覧ください。  

## <a name="on-demand-content-distribution"></a>オンデマンドのコンテンツ配布  
 優先配布ポイントへのオンデマンドのコンテンツ配布を有効にするために個々のアプリケーションとパッケージ (展開) に対して設定できるオプション。  

-   展開に対してこのオプションを有効にするには、 **[このパッケージのコンテンツを優先配布ポイントに配布する]**を有効にします。  

-   このオプションが展開で有効になっていて、クライアントがこのコンテンツを要求したときにコンテンツがクライアントの優先配布ポイントのいずれかで利用できない場合、Configuration Manager は、このコンテンツを自動的にクライアントの優先配布ポイントに配布します。  

-   このオプションが有効になっていると、Configuration Manager によってクライアントの優先配布ポイントにコンテンツが自動的に配布されますが、クライアントの優先配布ポイントが展開を受け取る前にクライアントが他の配布ポイントからコンテンツを取得する可能性があります。 その場合、コンテンツは、その展開を必要とする他のクライアントで利用できるように、その配布ポイント上に保持されます。  


さまざまなコンテンツの場所とフォールバック シナリオの詳細については、[コンテンツ ソースの場所の例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)をご覧ください。  


## <a name="package-transfer-manager"></a>Package Transfer Manager  
 他のコンピューター上の配布ポイントにコンテンツを転送するサイト サーバー コンポーネント。  

 [Package Transfer Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md) の詳細  

## <a name="preferred-distribution-point"></a>優先配布ポイント  
 クライアントの現在の境界グループに関連付けられている配布ポイント。  

 各配布ポイントを 1 つまたは複数の境界グループに関連付けることができます。  

-   この関連付けにより、コンテンツをダウンロードできる配布ポイントをクライアントが識別できるようになります。  

-   既定では、クライアントは、優先配布ポイントからのみコンテンツをダウンロードできます。  


さまざまなコンテンツの場所とフォールバック シナリオの詳細については、[コンテンツ ソースの場所の例](../../../core/plan-design/hierarchy/content-source-location-scenarios.md)をご覧ください。  

## <a name="prestage-content"></a>コンテンツの事前設定  
 ネットワーク経由でコンテンツを配布する際に Configuration Manager に依存することなく配布ポイントにコンテンツを転送するプロセス。  

 詳細については、「[ネットワーク帯域幅の管理](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)」を参照してください。



<!--HONumber=Nov16_HO1-->

