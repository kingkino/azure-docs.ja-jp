---
title: Azure PowerShell のサンプル - アプリをインストールする | Microsoft Docs
description: Azure PowerShell のサンプル
services: virtual-machine-scale-sets
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 4553dba3e7242f9c98f66b4851a1186ccd0cb31b
ms.sourcegitcommit: 0a84b090d4c2fb57af3876c26a1f97aac12015c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2018
ms.locfileid: "38605780"
---
# <a name="install-applications-into-a-virtual-machine-scale-set-with-powershell"></a>PowerShell を使用して仮想マシン スケール セットにアプリケーションをインストールする
このスクリプトでは、Windows Server 2016 を実行する仮想マシン スケール セットを作成し、カスタム スクリプト拡張機能を使用して基本的な Web アプリケーションをインストールします。 スクリプトを実行すると、Web ブラウザーで Web アプリにアクセスできるようになります。

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>サンプル スクリプト
[!code-powershell[main](../../../powershell_scripts/virtual-machine-scale-sets/install-apps/install-apps.ps1 "Install apps into a scale set")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ
次のコマンドを実行して、リソース グループ、スケール セット、すべての関連リソースを削除します。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>スクリプトの説明
このスクリプトでは、以下のコマンドを実行してデプロイを作成します。 表内の各項目は、コマンドごとのドキュメントにリンクされています。

| コマンド | メモ |
|---|---|
| [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvmss) | 仮想マシン スケール セットと、仮想ネットワーク、ロード バランサー、NAT 規則などのすべてのサポート リソースを作成します。 |
| [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) | 仮想マシン スケール セットに関する情報を取得します。 |
| [Add-AzureRmVmssExtension](/powershell/module/azurerm.compute/add-azurermvmssextension) | 基本的な Web アプリケーションをインストールするために、カスタム スクリプト用の VM 拡張機能を追加します。 |
| [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss) | VM 拡張機能を適用するために、仮想マシン スケール セット モデルを更新します。 |
| [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) | ロード バランサーによって使用される、割り当てられたパブリック IP アドレスについての情報を取得します。 |
|  [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | リソース グループと、それに含まれているすべてのリソースを削除します。 |

## <a name="next-steps"></a>次の手順
Azure PowerShell モジュールの詳細については、[Azure PowerShell のドキュメント](/powershell/azure/overview)を参照してください。

その他の仮想マシン スケール セット用の PowerShell サンプル スクリプトは、[Azure 仮想マシン スケール セットのドキュメント](../powershell-samples.md)にあります。