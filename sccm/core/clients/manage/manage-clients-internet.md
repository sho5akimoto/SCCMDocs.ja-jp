---
title: "クライアント管理 | インターネット | クラウド管理ゲートウェイ | Microsoft Docs"
description: 
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: e71ae1f654fcf3dd8c57a299c727588eed26ccac

---

# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>インターネット上のクライアントを Configuration Manager で管理する

*適用対象: System Center Configuration Manager (Current Branch)*

一般的に、Configuration Manager では、コンピューターやサーバーのほとんどは、管理機能を実行するサイト システム サーバーと同じ内部のプライベートまたはコーポレート ネットワークで物理的に管理されます。 ただし、インターネットに接続されている場合、サイト システム サーバーに到達するために仮想プライベート ネットワークを経由して接続することをクライアント コンピューターに要求せずに、コーポレート ネットワークの外部にあるクライアント コンピューターを管理できます。

Configuration Manager では、インターネットに接続されているクライアントを 2 つの方法で管理できます。

-   クラウド管理ゲートウェイ

-   インターネット ベースのクライアント管理

## <a name="cloud-management-gateway"></a>クラウド管理ゲートウェイ

バージョン 1610 以降、Configuration Manager にはクラウド管理ゲートウェイが導入されています。 この新しい方法では、Microsoft Azure にデプロイされているクラウド サービスとそのサービスと通信する新しいサイト システム ロールの組み合わせでインターネット ベースのクライアントを管理できます。 クライアントはこのサービスを利用し、Configuration Manager と通信します。

利点: 

-   インフラストラクチャの追加投資は必要ありません。

-   オンプレミス インフラストラクチャをインターネットに公開しません。

-   このサービスを実行するクラウド仮想マシンは Azure により完全管理され、保守管理を必要としません。

-   Configuration Manager コンソールで簡単にセットアップし、構成できます。

欠点: 

-   クラウド サブスクリプションにコストがかかります。

-   管理データがクラウド サービス経由で送信されます。

詳細については、「[クラウド管理ゲートウェイの計画](plan-cloud-management-gateway.md)」を参照してください。

## <a name="internet-based-client-management"></a>インターネット ベースのクライアント管理

この方法は、管理目的でクライアントが通信する、インターネットに接続されたサイト システム サーバーに依存します。 この方法では、クライアントとサイト システム サーバーにインターネット ベースの管理を構成する必要があります。

利点: 

-   クラウド サービスの依存関係はありません。

-   クラウド サブスクリプションに関連する追加コストはありません。

-   サービスを提供するサーバーとロールを完全制御できます。

欠点: 

-   インフラストラクチャの追加投資が必要です。

-   追加のインフラストラクチャに運用費と間接費がかかります。

-   インフラストラクチャをインターネットに公開する必要があります。

詳細は、「[インターネット ベースのクライアント管理の計画](plan-internet-based-client-management.md)」を参照してください。



<!--HONumber=Dec16_HO3-->

