---
title: "構成基準の作成 | System Center Configuration Manager"
description: "System Center Configuration Manager でコレクションに展開できる構成基準を作成します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9494524b68586d34b93b323a16829949b416c035


---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>System Center Configuration Manager での構成基準の作成

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager の構成基準には、定義済みの構成項目と、場合によっては他の構成基準が含まれています。 構成基準を作成すると、構成基準をコレクションに展開できるようになります。それによって、そのコレクションに含まれるデバイスで構成基準をダウンロードしたり、そのデバイスが構成基準に対して対応しているかを評価できます。  

 Configuration Manager の構成基準には、構成項目の特定のリビジョンを含めたり、構成項目の最新バージョンを常に使用するように構成することができます。 構成項目のリビジョンの詳細については、「[構成データの管理タスク](../../compliance/deploy-use/management-tasks-for-configuration-data.md)」を参照してください。  

 構成基準の作成に使用できる方法は、2 つあります。  

-   構成データをファイルからインポートします。 起動する、 **構成データのインポート ウィザード**, で、 **構成項目** または **構成基準** 内のノード、 **資産とコンプライアンス** ] ワークスペースで、をクリックして **構成データのインポート**です。  

-   [構成基準の作成] ダイアログ ボックスを使用して、新しい構成基準を作成します。 ****  

 [構成基準の作成] ダイアログ ボックスを使用して構成基準を作成するには、次の手順に従います。 ****  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[構成基準]** の順にクリックします。  

3.  **ホーム** ] タブで、 **作成** グループで、[ **構成基準の作成**です。  

4.  [構成基準の作成] ダイアログ ボックスで、構成基準に、一意の名前と説明を入力します。 **** 名前には最大 255 文字を、説明には最大 512 文字を使用できます。  

5.  [構成データ] 一覧に、この構成基準に含まれる、すべての構成項目または構成基準が表示されます。 **** 新しい構成項目または構成基準を一覧に追加するには、[追加] をクリックします。 **** 次のオプションから選択できます。  

    -   **構成項目**  

    -   **ソフトウェア更新プログラム**  

    -   ****  
      > [!IMPORTANT]
      > ソフトウェア更新プログラムが 1000 を超えないように各構成基準を制限する必要があります。
6.  使用して、 **目的の変更** 一覧で選択した構成項目の動作を指定する、 **構成データ** ] ボックスの一覧です。 次のオプションから選択できます。  

    -   **[必須]** クライアント デバイスで構成項目が検出されない場合、構成基準の評価は "非対応" になります。 検出された場合、評価は "対応" になります。  

    -   **[オプション]** クライアント コンピューターで、構成項目が参照するアプリケーションが見つかる場合のみ、構成項目の評価が "対応" になります。 アプリケーションが見つからない場合、構成基準は "非対応" としてマークされません (アプリケーションの構成項目のみに適用されます)。  

    -   **[禁止]** クライアント コンピューターで構成項目が検出された場合、構成基準の評価は "非対応" になります (アプリケーションの構成項目のみに適用されます)。  

    > [!NOTE]
    >  **目的の変更** 一覧は、オプションをクリックした場合にのみ使用できます。 **この構成項目には、アプリケーションの設定が含まれています。** 上、 **全般的な** のページ、 **構成項目の作成ウィザード**です。  

7.  使用して、 **変更リビジョン** 特定またはクライアント デバイスでの対応評価のためかを選択する構成項目の最新の改訂版を選択する一覧 **常に最新** を常に最新の改訂版を使用します。 構成項目のリビジョンの詳細については、「[構成データの管理タスク](../../compliance/deploy-use/management-tasks-for-configuration-data.md)」を参照してください。  

8.  構成基準から構成項目を削除するには、構成項目を選択して、[**削除**] をクリックします。  

9. クリックして **[ok]** を閉じる、 **構成基準の作成** ] ダイアログ ボックスと、構成基準を作成します。  



<!--HONumber=Nov16_HO1-->

