---
title: Erstellen einer Linux-VM in Azure mithilfe einer Vorlage | Microsoft-Dokumentation
description: Verwenden der Azure-CLI-2.0 zum Erstellen einer Linux-VM aus einer Ressourcen-Manager-Vorlage
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 12/18/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2750bed40707872bb120a7cb7130d8be01aabf7d
ms.sourcegitcommit: 059dae3d8a0e716adc95ad2296843a45745a415d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Erstellen eines virtuellen Linux-Computers mithilfe von Azure Resource Manager-Vorlagen
In diesem Artikel erfahren Sie, wie Sie schnell einen virtuellen Linux-Computer (VM) mithilfe von Azure Resource Manager-Vorlagen und der Azure CLI 2.0 bereitstellen. Sie können diese Schritte auch per [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md) ausführen.


## <a name="templates-overview"></a>Übersicht über Vorlagen
Azure Resource Manager-Vorlagen sind JSON-Dateien, die die Infrastruktur und Konfiguration Ihrer Azure-Lösung definieren. Mit einer Vorlage können Sie die Lösung während ihres Lebenszyklus wiederholt bereitstellen und sicher sein, dass Ihre Ressourcen einheitlich bereitgestellt werden. Weitere Informationen zum Format der Vorlage und zur Erstellung finden Sie unter [Erstellen Ihrer ersten Azure Resource Manager-Vorlage](../../azure-resource-manager/resource-manager-create-first-template.md). Die JSON-Syntax für Ressourcentypen finden Sie unter [Define resources in Azure Resource Manager templates](/azure/templates/) (Definieren von Ressourcen in Azure Resource Manager-Vorlagen).


## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe
Eine Azure-Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen bereitgestellt und verwaltet werden. Vor dem virtuellen Computer muss eine Ressourcengruppe erstellt werden. Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen *myResourceGroupVM* in der Region *eastus* erstellt:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Erstellen eines virtuellen Computers
Im folgenden Beispiel wird eine VM aus [dieser Azure Resource Manager-Vorlage](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) mit [az group deployment create](/cli/azure/group/deployment#az_group_deployment_create) erstellt. Nur die SSH-Authentifizierung ist zulässig. Geben Sie bei Aufforderung den Wert Ihres eigenen öffentlichen SSH-Schlüssels ein, etwa den Inhalt von *~/.ssh/id_rsa.pub*. Informationen zum Erstellen eines SSH-Schlüsselpaars finden Sie unter [Erstellen und Verwenden eines SSH-Schlüsselpaars für Linux-VMs in Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

Im vorherigen Beispiel haben Sie eine in GitHub gespeicherte Vorlage angegeben. Sie können eine Vorlage außerdem herunterladen oder erstellen und den lokalen Pfad mit dem Parameter `--template-file` angeben.


## <a name="connect-to-virtual-machine"></a>Herstellen der Verbindung mit dem virtuellen Computer
Rufen Sie die öffentliche IP-Adresse mit [az vm show](/cli/azure/vm#az_vm_show) auf, um Ihre VM mit SSH zu schützen:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name sshvm \
    --show-details \
    --query publicIps \
    --output tsv
```

Anschließend können Sie wie gewohnt eine SSH-Verbindung mit dem virtuellen Computer herstellen. Geben Sie Ihre eigene öffentliche IP-Adresse aus dem vorherigen Befehl an:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Nächste Schritte
In diesem Beispiel haben Sie eine einfache Linux-VM erstellt. Weitere Resource Manager-Vorlagen, die Anwendungsframeworks enthalten oder komplexere Umgebungen erstellen, finden Sie mithilfe einer Suche im [Azure-Schnellstartvorlagen-Katalog](https://azure.microsoft.com/documentation/templates/).