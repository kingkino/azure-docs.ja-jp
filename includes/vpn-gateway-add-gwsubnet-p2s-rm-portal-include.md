---
title: インクルード ファイル
description: インクルード ファイル
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: a8dec00373d991a7aeaf11f1a4d95463ab71d9a2
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2018
ms.locfileid: "30197084"
---
1. [ポータル](http://portal.azure.com)で、仮想ネットワーク ゲートウェイを作成する Resource Manager 仮想ネットワークに移動します。
2. VNet のページの **[設定]** セクションで、**[サブネット]** をクリックして **[サブネット]** ページを展開します。
3. **[サブネット]** ページで **[+ゲートウェイ サブネット]** をクリックして、**[サブネットの追加]** ページを開きます。 

  ![ゲートウェイ サブネットの追加](./media/vpn-gateway-add-gwsubnet-p2s-rm-portal-include/addgwsubnet.png "ゲートウェイ サブネットの追加")
4. サブネットの **[名前]** には、"GatewaySubnet" という値が自動的に入力されます。 この値は、Azure がゲートウェイ サブネットとしてこのサブネットを認識するために必要になります。 自動入力される **[アドレス範囲]** の値を実際の構成要件に合わせて調整し、ページの下部にある **[OK]** をクリックしてサブネットを作成します。

  ![サブネットの追加](./media/vpn-gateway-add-gwsubnet-p2s-rm-portal-include/p2sgwsub.png "サブネットの追加")