---
title: Visual Studio Code を使って Azure Resource Manager テンプレートを作成する | Microsoft Docs
description: Visual Studio Code と Azure Resource Manager ツールの拡張機能を使用して Resource Manager テンプレートを操作する方法について説明します。
services: azure-resource-manager
documentationcenter: ''
author: mumian
manager: dougeby
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 08/24/2018
ms.topic: quickstart
ms.author: jgao
ms.openlocfilehash: 540aabc9164e43776d2166926430f4512dd23f49
ms.sourcegitcommit: f6e2a03076679d53b550a24828141c4fb978dcf9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43106051"
---
# <a name="quickstart-create-azure-resource-manager-templates-by-using-visual-studio-code"></a>クイック スタート: Visual Studio Code を使って Azure Resource Manager テンプレートを作成する

Visual Studio Code と Azure Resource Manager ツール拡張機能を使用して Azure Resource Manager テンプレートを作成する方法について説明します。 Visual Studio Code では、拡張機能を使わずに Resource Manager テンプレートを作成することもできますが、拡張機能を利用すれば、オートコンプリート機能によってテンプレートの開発を省力化することができます。 Azure ソリューションのデプロイと管理に関する概念について理解を深めるには、「[Azure Resource Manager の概要](resource-group-overview.md)」を参照してください。

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウントを作成](https://azure.microsoft.com/free/)してください。

## <a name="prerequisites"></a>前提条件

この記事を完了するには、以下が必要です。

- [Visual Studio Code](https://code.visualstudio.com/)。
- Resource Manager ツール拡張機能。 インストールするには、次の手順を使用します。

    1. Visual Studio Code を開きます。
    2. **Ctrl + Shift + X** キーを押して、拡張機能ウィンドウを開きます
    3. **[Azure Resource Manager ツール]** を探して、**[インストール]** を選択します。
    4. **[再読み込み]** を選択して、拡張機能のインストールを完了します。

## <a name="open-a-quickstart-template"></a>クイック スタート テンプレートを開く

ゼロからテンプレートを作成するのではなく、[Azure クイック スタート テンプレート](https://azure.microsoft.com/resources/templates/)からテンプレートを開きます。 Azure クイック スタート テンプレートは、Resource Manager テンプレートのリポジトリです。

このクイック スタートで使用されるテンプレートは、[Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/) と呼ばれます。 テンプレートにより、Azure ストレージ アカウント リソースが定義されます。

1. Visual Studio Code から、**[ファイル]**>**[ファイルを開く]** を選択します。
2. **[ファイル名]** に以下の URL を貼り付けます。

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
    ```
3. **[開く]** を選択して、ファイルを開きます。
4. **[ファイル]**>**[名前を付けて保存]** を選択し、ファイルを **azuredeploy.json** としてご自身のローカル コンピューターに保存します。

## <a name="edit-the-template"></a>テンプレートの編集

Visual Studio Code を使用してテンプレートを編集する方法を確認するために、outputs セクションに要素をもう 1 つ追加します。

1. Visual Studio Code で、エクスポートしたテンプレートに出力をもう 1 つ追加します。

    ```json
    "storageUri": {
      "type": "string",
      "value": "[reference(variables('storageAccountName')).primaryEndpoints.blob]"
    }
    ```

    完了すると、outputs セクションは次のようになります。

    ```json
    "outputs": {
      "storageAccountName": {
        "type": "string",
        "value": "[variables('storageAccountName')]"
      },
      "storageUri": {
        "type": "string",
        "value": "[reference(variables('storageAccountName')).primaryEndpoints.blob]"
      }
    }
    ```

    Visual Studio Code 内でコードをコピーして貼り付けたら、**value** 要素を再入力して、Resource Manager ツール拡張機能の IntelliSense 機能を体験してみます。

    ![Resource Manager テンプレートにおける Visual Studio Code の IntelliSense](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/resource-manager-templates-visual-studio-code-intellisense.png)

2. **[ファイル]**>**[保存]** を選択して、ファイルを保存します。

## <a name="deploy-the-template"></a>テンプレートのデプロイ

テンプレートをデプロイする方法は多数あります。  このチュートリアルでは、Azure Portal から Azure Cloud Shell を使用します。 Cloud Shell では、Azure CLI と Azure PowerShell の両方がサポートされます。 

1. [Azure ポータル](https://portal.azure.com)
2. 次の図のように、右上隅の **[Cloud Shell]** を選択します。

    ![Azure portal の Cloud Shell](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell.png)

    画面の下部に Cloud Shell が開きます。

3. Cloud Shell の左上隅に、**PowerShell** または **Bash** のいずれかが表示されます。 CLI を使用するには、Bash セッションを開く必要があります。 PowerShell を実行するには、PowerShell セッションを開く必要があります。 切り替えるには、下向き矢印を選択し、インタープリターを選択します。 次の図は、PowerShell から Bash への切り替えを示しています。

    ![Azure portal の Cloud Shell の CLI](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-choose-cli.png)

    切り替えた場合は、シェルを再起動する必要があります。
4. **[ファイルのアップロード/ダウンロード]** を選択し、**[アップロード]** を選択します。

    ![Azure portal の Cloud Shell のファイルのアップロード](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-upload-file.png)

    シェルからデプロイする前に、テンプレート ファイルをアップロードする必要があります。
5. クイック スタートで前に保存したファイルを選択します。 既定の名前は **azuredeploy.json** です。
6. Cloud Shell から **Is** コマンドを実行し、ファイルが適切にアップロードされていることを確認します。 **cat** コマンドを使用して、テンプレートの内容を確認することもできます。 次の図は、Bash からのコマンドの実行を示しています。  PowerShell セッションでも同じコマンドを使用します。

    ![Azure portal の Cloud Shell のファイルの一覧表示](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-list-file.png)
7. Cloud Shell で次のコマンドを実行します。 PowerShell コードまたは CLI コードを表示するタブを選択します。

    # <a name="clitabcli"></a>[CLI](#tab/CLI)
    ```cli
    az group create --name <ResourceGroupName> --location <AzureLocation>

    az group deployment create --name <DeploymentName> --resource-group <ResourceGroupName> --template-file <TemplateFileName>
    ```
   
    # <a name="powershelltabpowershell"></a>[PowerShell](#tab/PowerShell)
    
    ```powershell
    New-AzureRmResourceGroup -Name <ResourceGroupName> -Location <AzureLocation>

    New-AzureRmResourceGroupDeployment -ResourceGroupName <ResourceGroupName> -TemplateFile <TemplateFileName>
    ```
    
    ---

    次のスクリーンショットは、サンプル CLI のデプロイを示しています。

    ![Azure portal の Cloud Shell のテンプレートのデプロイ](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-deploy-template.png)

    スクリーンショットでは、次の値が使用されています。

    - **&lt;ResourceGroupName>**: myresourcegroup0709。 パラメーターが 2 つ表示されます。  同じ値を使用してください。
    - **&lt;AzureLocation>**: eastus2
    - **&lt;DeployName>**: mydeployment0709
    - **&lt;TemplateFile>**: azuredeploy.json

    スクリーンショットの出力では、ストレージ アカウント名は *3tqebj3slyfyestandardsa* です。 

7. 次の CLI または PowerShell コマンドを実行して、新しく作成されたストレージ アカウントの一覧を表示します。

    # <a name="clitabcli"></a>[CLI](#tab/CLI)
    ```cli
    az storage account show --resource-group <ResourceGroupName> --name <StorageAccountName>
    ```
   
    # <a name="powershelltabpowershell"></a>[PowerShell](#tab/PowerShell)
    
    ```powershell
    Get-AzureRmStorageAccount -ResourceGroupName <ResourceGroupName> -Name <StorageAccountName>
    ```
    
    ---

## <a name="clean-up-resources"></a>リソースのクリーンアップ

Azure リソースが不要になったら、リソース グループを削除して、デプロイしたリソースをクリーンアップします。

1. Azure portal で、左側のメニューから **[リソース グループ]** を選択します。
2. **[名前でフィルター]** フィールドに、リソース グループ名を入力します。
3. リソース グループ名を選択します。  リソース グループ内の合計 6 つのリソースが表示されます。
4. トップ メニューから **[リソース グループの削除]** を選択します。

## <a name="next-steps"></a>次の手順

このチュートリアルの主な目的は、Visual Studio Code を使用して、Azure クイック スタート テンプレートの既存のテンプレートを編集することです。 Azure Cloud Shell から CLI または PowerShell を使用してテンプレートをデプロイする方法も学習しました。 Azure クイック スタート テンプレートのテンプレートでは、必要なものすべてを得ることができないことがあります。 次のチュートリアルでは、テンプレート リファレンスから情報を検索して、暗号化された Azure Storage アカウントを作成できるようにする方法を示します。

> [!div class="nextstepaction"]
> [暗号化されたストレージ アカウントを作成する](./resource-manager-tutorial-create-encrypted-storage-accounts.md)
