---
title: "Windows 10 のサポート | Microsoft Docs"
description: "System Center Configuration Manager クライアントの実行がサポートされている Windows 10 のバージョンについて説明します。"
ms.custom: na
ms.date: 2/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3702993d6cf9644d5aebaadd168749668fbcb62c
ms.openlocfilehash: 4b90384621dd20475ab9ea33ea062c24f5ecf5fa
ms.lasthandoff: 02/22/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>System Center Configuration Manager のクライアントとしての Windows 10 のサポート

*適用対象: System Center Configuration Manager (Current Branch)*


 このトピックでは、さまざまなバージョンの System Center Configuration Manager Current Branch でクライアントとして使用できる Windows 10 のバージョンを示します。

- これは、「[クライアントとデバイスのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)」の補足です。
- Configuration Manager の Long-Term Servicing Branch を使用する場合は、「[Long-Term Servicing Branch でサポートされている構成](/sccm/core/understand/supported-configurations-for-ltsb)」を参照してください。

Configuration Manager は、Windows 10 の新しいバージョンがリリースされると、できるだけ早く、そのバージョンに対するサポートを提供しようとします。 製品には個別の開発およびリリースのスケジュールがあるため、Configuration Manager で提供するサポートは、各製品のバージョンおよびブランチのリリース時期によって異なります。  



|Windows 10 のバージョン |Configuration Manager 1602|Configuration Manager 1606|Configuration Manager 1610|
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|1507 <br />Enterprise、Pro | ![サポートされています](media/green_check.png)| ![サポートされています](media/green_check.png)|![サポートされています](media/green_check.png) |
|1511 <br />Enterprise、Pro <br />(CB)、(CBB) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |![サポートされています](media/green_check.png) |
|Enterprise 2016 LTSB    |![サポートされていません](media/Red_X.png) |![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png)|
|1607 <br />Enterprise、Pro<br /> (CB)    |![サポートされていません](media/Red_X.png) |![下位互換性あり](media/blue_compat.png) |![サポートされています](media/green_check.png) |
|1607 <br />Enterprise、Pro <br />(CBB)    |![サポートされていません](media/Red_X.png) |![下位互換性あり](media/Red_X.png) |![サポートされています](media/green_check.png) |


|キー|
|--|
|![サポートされています](media/green_check.png) = **サポートされています**  |
|![サポートされていません](media/blue_compat.png)  = **下位互換性あり** - つまり、既存のクライアント管理機能 (ハードウェア インベントリ、ソフトウェア インベントリ、ソフトウェア更新プログラムなど) は、新しい Windows 10 Current Branch のビルドで動作する必要があります。 既知の問題や注意事項が記述されます。 <br><br>この方法では、新しい Configuration Manager 更新バージョンを必要とせずに、アプリケーションの互換性サポートが含まれる新しい Windows 10 CB ビルドを 1 日で展開して管理することができます。 |
|![サポートされています](media/Red_X.png) = **サポートされていません**|
