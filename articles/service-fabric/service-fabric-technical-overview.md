---
title: Azure Service Fabric の用語を学習する | Microsoft Docs
description: Service Fabric の用語の概要です。 重要な用語の概念と、ドキュメントの他の部分で使用される用語について説明します。
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/26/2018
ms.author: ryanwi
ms.openlocfilehash: e3da081f9b327031d6d1e0afd2f2fb52383bf933
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2018
ms.locfileid: "34212070"
---
# <a name="service-fabric-terminology-overview"></a>Service Fabric の用語の概要
Azure Service Fabric は、拡張性と信頼性に優れたマイクロサービスのパッケージ化とデプロイ、管理を簡単に行うことができる分散システム プラットフォームです。 この記事では、Service Fabric 関連ドキュメントで使用される用語の意味を理解するうえで参考となるように、Service Fabric で使用される用語について詳しく説明します。

このセクションで示す概念は、<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">主要概念</a>、<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">デザイン時の概念</a>、<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">実行時の概念</a>に関する Microsoft Virtual Academy のビデオでも説明しています。

## <a name="infrastructure-concepts"></a>インフラストラクチャの概念
**クラスター**: ネットワークで接続された一連の仮想マシンまたは物理マシン。マイクロサービスは、クラスターにデプロイして管理することになります。  クラスターは多数のマシンにスケールできます。

**ノード**: クラスターに属しているコンピューターまたは VM を "*ノード*" といいます。 それぞれのノードには、ノード名 (文字列) が割り当てられます。 ノードには、配置プロパティなどの特性があります。 それぞれのコンピューターまたは VM には、自動的に開始される Windows サービス (`FabricHost.exe`) が存在します。このサービスがコンピューターまたは VM の起動時に開始され、`Fabric.exe` と `FabricGateway.exe` の 2 つの実行可能ファイルを起動します。 ノードは、この 2 つの実行可能ファイルから成ります。 テストのシナリオでは、`Fabric.exe` と `FabricGateway.exe` の複数のインスタンスを実行することによって、1 台のコンピューターまたは VM で複数のノードをホストできます。

## <a name="application-concepts"></a>アプリケーションの概念
**アプリケーションの種類**: 一連のサービスの種類に割り当てられる名前またはバージョン。 これは `ApplicationManifest.xml` ファイルで定義されて、アプリケーション パッケージ ディレクトリ内に埋め込まれます。 ディレクトリは、Service Fabric クラスターのイメージ ストアにコピーされます。 このアプリケーションの種類に基づいて、特定の名前のアプリケーションをクラスター内で作成することができます。

詳細については、[アプリケーション モデル](service-fabric-application-model.md)に関する記事をご覧ください。

**アプリケーション パッケージ**: アプリケーションの種類を定義した `ApplicationManifest.xml` ファイルが格納されるディスク上のディレクトリ。 アプリケーションの種類を構成するサービスの種類ごとに、対応するサービス パッケージを参照します。 アプリケーション パッケージ ディレクトリ内のファイルは、Service Fabric クラスターのイメージ ストアにコピーされます。 たとえば電子メール アプリケーション タイプのアプリケーション パッケージであれば、キューサービス パッケージやフロントエンドサービス パッケージ、データベースサービス パッケージへの参照が含まれることが考えられます。

**名前付きアプリケーション**: アプリケーション パッケージをイメージ ストアにコピーした後、アプリケーションのインスタンスをクラスター内に作成します。 対応する名前またはバージョンを使用して、アプリケーション パッケージのアプリケーションの種類を指定するときにインスタンスが作成されます。 アプリケーションの種類のインスタンスにはそれぞれ、URI (Uniform Resource Identifier) 名 (`"fabric:/MyNamedApp"` など) が割り当てられます。 1 つのアプリケーションの種類から複数の名前付きアプリケーションをクラスター内で作成することが可能です。 異なるアプリケーションの種類から名前付きアプリケーションを作成することもできます。 個々の名前付きアプリケーションは別々に管理され、バージョニングされます。      

**サービスの種類**: サービスのコード パッケージとデータ パッケージ、構成パッケージに割り当てられる名前またはバージョン。 サービスの種類は `ServiceManifest.xml` ファイルで定義されて、サービス パッケージ ディレクトリ内に埋め込まれます。 サービス パッケージ ディレクトリは、アプリケーション パッケージの `ApplicationManifest.xml` ファイルから参照されます。 クラスターには、名前付きアプリケーションを作成した後、そのアプリケーションの種類を構成するいずれかのサービスの種類から名前付きサービスを作成することができます。 サービスは、そのサービスの種類に対応する `ServiceManifest.xml` ファイルによって記述されます。

詳細については、[アプリケーション モデル](service-fabric-application-model.md)に関する記事をご覧ください。

サービスには、次の 2 種類があります。

* **ステートレス:** サービスの永続的な状態を外部ストレージ サービス (Azure Storage、Azure SQL Database、Azure Cosmos DB など) に保存する場合はステートレス サービスを使用します。 永続的なストレージがサービスに存在しない場合は、ステートレス サービスを使用します。 たとえば電卓サービスに値を渡すと、それらの値を使って計算が実行され、結果が返されます。
* **ステートフル:** Service Fabric の Reliable Collection や Reliable Actors のプログラミング モデルを介してサービスの状態を管理する場合は、ステートフル サービスを使用します。 名前付きサービスを作成するときに、拡張性を得るために状態を分散させるパーティションの数を指定します。 さらに、信頼性のために、状態をノード間でレプリケートさせる回数を指定します。 それぞれの名前付きサービスは、1 つのプライマリ レプリカと複数のセカンダリ レプリカを持ちます。 名前付きサービスの状態は、プライマリ レプリカに書き込むときに変更します。 その後、状態を同期させるために Service Fabric がその状態をすべてのセカンダリ レプリカにレプリケートします。Service Fabric は、プライマリ レプリカの障害を自動的に検出し、既存のセカンダリ レプリカをプライマリ レプリカに昇格させます。 その後、Service Fabric は、新しいセカンダリ レプリカを作成します。  

**レプリカまたはインスタンス**とは、デプロイされ、実行中であるサービスのコード (およびステートフル サービスの状態) のことです。 「[レプリカとインスタンス](service-fabric-concepts-replica-lifecycle.md)」をご覧ください。

**再構成**とは、サービスのレプリカ セット内で行われる任意の変更処理を示します。 [再構成](service-fabric-concepts-reconfiguration.md)に関するページをご覧ください。

**サービス パッケージ**: サービスの種類を定義した `ServiceManifest.xml` ファイルが格納されるディスク上のディレクトリ。 このファイルは、特定の種類のサービスに必要なコード、静的データ、構成パッケージを参照します。 サービス パッケージ ディレクトリ内のファイルは、アプリケーションの種類を定義した `ApplicationManifest.xml` ファイルから参照されます。 たとえばサービス パッケージは、データベース サービスを構成するコードや静的データ、構成パッケージを参照します。

**名前付きサービス**: 名前付きアプリケーションを作成した後、そのいずれかのサービスの種類のインスタンスをクラスターに作成できます。 サービスの種類を特定するには、対応する名前またはバージョンを使用します。 サービスの種類のインスタンスにはそれぞれ、対応する名前付きアプリケーションの URI に従属する URI 名が割り当てられます。 たとえば、名前付きサービス "MyDatabase" を名前付きアプリケーション "MyNamedApp" 内に作成した場合、 `"fabric:/MyNamedApp/MyDatabase"`のような URI が割り当てられます。 1 つの名前付きアプリケーションに複数の名前付きサービスを作成することができます。 名前付きサービスにはそれぞれ固有のパーティション構成とインスタンスまたはレプリカ数を割り当てることができます。

**コード パッケージ**: 特定の種類のサービスで使用される実行可能ファイル (通常、EXE または DLL ファイル) が格納されるディスク上のディレクトリ。 コード パッケージ ディレクトリ内のファイルは、サービスの種類を定義した `ServiceManifest.xml` ファイルから参照されます。 名前付きサービスの作成時に、名前付きサービスを実行するために選択されたノードにコード パッケージがコピーされます。 その後、コードが実行を開始します。 コード パッケージの実行可能ファイルには次の 2 種類があります。

* **ゲスト実行可能ファイル**: ホスト オペレーティング システム (Windows または Linux) 上において単体で動作する実行可能ファイル。 これらの実行可能ファイルは、Service Fabric のランタイム ファイルと連動したりそれらのファイルを参照したりしないため、Service Fabric のプログラミング モデルは一切使用しません。 これらの実行可能ファイルは、エンドポイント検出用のネーム サービスなどの Service Fabric の一部の機能を使用できません。 ゲスト実行可能ファイルは、各サービス インスタンスに固有のロード メトリックを報告できません。
* **サービス ホスト実行可能ファイル**: Service Fabric のランタイム ファイルと連動することによって Service Fabric のプログラミング モデルを使用し、Service Fabric の機能を有効にする実行可能ファイルです。 たとえば名前付きサービスのインスタンスが、Service Fabric のネーム サービスにエンドポイントを登録できるほか、負荷のメトリックを報告することもできます。      

**データ パッケージ**: 特定の種類のサービスで使用される読み取り専用の静的なデータ ファイル (通常、写真、サウンド、ビデオ ファイル) が格納されるディスク上のディレクトリ。 データ パッケージ ディレクトリ内のファイルは、サービスの種類を定義した `ServiceManifest.xml` ファイルから参照されます。 名前付きサービスの作成時に、名前付きサービスを実行するために選択されたノードにデータ パッケージがコピーされます。 コードが実行を開始し、データ ファイルにアクセスできるようになります。

**構成パッケージ**: 特定の種類のサービスで使用される読み取り専用の静的な構成ファイル (通常、テキスト ファイル) が格納されるディスク上のディレクトリ。 構成パッケージ ディレクトリ内のファイルは、サービスの種類を定義した `ServiceManifest.xml` ファイルから参照されます。 名前付きサービスの作成時に、名前付きサービスを実行するために選択された 1 つまたは複数のノードに構成パッケージ内のファイルがコピーされます。 その後、コードが実行を開始し、構成ファイルにアクセスできるようになります。

**コンテナー**: 既定では、Service Fabric はサービスをプロセスとしてデプロイし、アクティブ化します。 さらに、Service Fabric では、コンテナー イメージ内のサービスもデプロイできます。 コンテナーは、システムの基礎となるオペレーティング システムをアプリケーションで仮想化する、仮想化テクノロジです。 アプリケーションとそのランタイム、依存関係、およびシステム ライブラリは、コンテナー内で実行されます。 コンテナーには、オペレーティング システムの構成要素に関する、そのコンテナーに固有の分離されたビューへの完全なプライベート アクセスがあります。 Service Fabric では、Linux および Windows Server コンテナー上の Docker コンテナーをサポートします。 詳細については、[Service Fabric とコンテナー](service-fabric-containers-overview.md)に関する記事をご覧ください。

**パーティション構成**: パーティション構成は、名前付きサービスを作成するときに指定します。 さまざまな状態を伴うサービスでは、データが複数のパーティションに分割されて、状態がクラスターのノードに分散されます。 複数のパーティションにデータを分割することによって、名前付きサービスの状態をスケールできます。 パーティションには、ステートレスの名前付きサービスの場合はインスタンスが、ステートフルの名前付きサービスの場合はレプリカが格納されます。 通常、ステートレスの名前付きサービスは内部的な状態を持たないため、割り当てられるパーティションは 1 つだけです。 パーティションのインスタンスによってもたらされるのは可用性です。 つまり 1 つのインスタンスで障害が発生しても他のインスタンスは正常動作を保ち、Service Fabric によって新しいインスタンスが作成されます。 ステートフルの名前付きサービスでは、その状態がレプリカ内で管理されます。それぞれのパーティションが固有のレプリカ セットを持つため、状態が同期されます。万一レプリカに障害が発生した場合は、Service Fabric が既存のレプリカから新しいレプリカを構築します。

詳細については、「 [Service Fabric Reliable Services のパーティション分割](service-fabric-concepts-partitioning.md) 」をご覧ください。

## <a name="system-services"></a>システム サービス
すべてのクラスターには、Service Fabric のプラットフォーム機能を提供するシステム サービスが作成されています。

**ネーム サービス**: 各 Service Fabric クラスターには、サービス名をクラスター内の場所に解決するネーム サービスがあります。 インターネットのクラスター用のドメイン ネーム システム (DNS) と同じように、サービス名とプロパティを管理します。 クライアントは、ネーム サービスを使用することでクラスター内の任意のノードと安全に通信して、サービス名とその場所を解決します。 アプリケーションはクラスター内で移動されます。 これはたとえば、障害、リソース分散、クラスターのサイズ変更などが原因です。 現在のネットワークの場所を解決するサービスとクライアントを開発できます。 クライアントは、それが現在実行されている実際のコンピューターの IP アドレスとポートを取得します。

ネーム サービスと連動して動作するクライアントおよびサービス通信 API の使用方法の詳細については、[サービスとの通信](service-fabric-connect-and-communicate-with-services.md)に関する記事をご覧ください。

**イメージ ストア サービス**: 各 Service Fabric クラスターには、デプロイおよびバージョン管理されたアプリケーション パッケージが保持されるイメージ ストア サービスがあります。 アプリケーション パッケージをイメージ ストアにコピーした後、そのアプリケーション パッケージに含まれているアプリケーションの種類を登録します。 アプリケーションの種類をプロビジョニングした後、そのアプリケーションの種類から名前付きアプリケーションを作成します。 アプリケーションの種類は、そのアプリケーションの種類から作成されているすべての名前付きアプリケーションを削除した後、イメージ ストア サービスからの登録を解除できます。

Image Store サービスの詳細については、「[ImageStoreConnectionString 設定を理解する](service-fabric-image-store-connection-string.md)」をご覧ください。

イメージ ストア サービスへのアプリケーションのデプロイの詳細については、[アプリケーションのデプロイ](service-fabric-deploy-remove-applications.md)に関する記事をご覧ください。

**Failover Manager サービス**: 各 Service Fabric クラスターには、次の処理を担当する Failover Manager サービスがあります。
   - サービスの高可用性と整合性に関する役割を担います。
   - アプリケーションとクラスターのアップグレードを調整します。
   - 他のシステム コンポーネントとやり取りします。

**Repair Manager サービス**: これは、安全で、自動化可能、かつ透過的な方法でクラスター上で修復アクションを実行できるようにする、省略可能なシステム サービスです。 Repair Manager は、次の操作で使用されます。
   - [Silver および Gold 持続性](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) Azure Service Fabric クラスター上での Azure メンテナンス修復の実行。
   - [パッチ オーケストレーション アプリケーション](service-fabric-patch-orchestration-application.md)のための修復アクションの実行

## <a name="built-in-programming-models"></a>組み込みのプログラミング モデル
Service Fabric サービスをビルドできるように、次の .NET Framework および Java プログラミング モデルが使用可能になっています。

**Reliable Services**: ステートレス サービスとステートフル サービスを構築するための API。 ステートフル サービスの状態は、Reliable Collection (ディクショナリ、キューなど) に格納されます。 他にも、Web API や Windows Communication Foundation (WCF) など、さまざまな通信スタックを組み込むことができます。

**Reliable Actors**: 仮想アクター プログラミング モデルを使用してステートレス オブジェクトとステートフル オブジェクトを構築するための API。 このモデルは、独立した計算または状態の単位が多数存在するときに適しています。 このモデルは、順番に基づくスレッド モデルを採用しているため、他のアクターやサービスを呼び出すコードは避けた方が賢明です。それぞれのアクターは、すべての送信要求が完了するまで他の受信要求を処理できません。

また、Service Fabric 上で既存のアプリケーションを実行することもできます。

**Containers**: Service Fabric は、Hyper-V の分離モードのサポートと共に、Linux での Docker コンテナーおよび Windows Server 2016 での Windows Server コンテナーのデプロイをサポートしています。 Service Fabric の [アプリケーション モデル](service-fabric-application-model.md)では、コンテナーは複数のサービス レプリカが配置されたアプリケーション ホストを表します。 Service Fabric は任意のコンテナーを実行でき、そのシナリオは、コンテナーの内部で既存のアプリケーションをパッケージ化するゲスト実行可能ファイルのシナリオと同様です。 さらに、[コンテナーの内部で Service Fabric サービスを実行する](service-fabric-services-inside-containers.md)こともできます。

**ゲスト実行可能ファイル**: Node.js、Java、C++ などの任意の種類のコードを Azure Service Fabric でサービスとして実行できます。 Service Fabric では、これらの種類のサービスはゲスト実行可能ファイルと呼ばれます。これは、ステートレス サービスとして処理されます。 Service Fabric クラスターでゲスト実行可能ファイルを実行する利点には、高可用性、正常性の監視、アプリケーション ライフサイクル管理、高密度、および見つけやすさが含まれます。

詳細については、[サービスのプログラミング モデルの選択](service-fabric-choose-framework.md)に関する記事をご覧ください。

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>次の手順
Service Fabric の詳細については、以下の情報を参照してください。

* [Service Fabric の概要](service-fabric-overview.md)
* [マイクロサービスの手法でアプリケーションを構築する理由は何ですか。](service-fabric-overview-microservices.md)
* [アプリケーションのシナリオ](service-fabric-application-scenarios.md)


