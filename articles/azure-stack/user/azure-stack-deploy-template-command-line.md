---
title: Bereitstellen von Vorlagen mithilfe der Befehlszeile in Azure Stack | Microsoft-Dokumentation
description: Hier erfahren Sie, wie Sie mit der plattformübergreifenden Befehlszeilenschnittstelle (Command Line Interface, CLI) Vorlagen in Azure Stack bereitstellen.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 761e09889a230642c42697b6bc4f96dc32fe03a0
ms.sourcegitcommit: 20d103fb8658b29b48115782fe01f76239b240aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="deploy-templates-in-azure-stack-using-the-command-line"></a>Bereitstellen von Vorlagen in Azure Stack mithilfe der Befehlszeile

*Gilt für: integrierte Azure Stack-Systeme und Azure Stack Development Kit*

Verwenden Sie die Befehlszeile zum Bereitstellen von Azure Resource Manager-Vorlagen im Azure Stack Development Kit. Azure Resource Manager-Vorlagen stellen alle Ressourcen für Ihre Anwendung in einem einzigen, koordinierten Vorgang bereit.

## <a name="before-you-begin"></a>Voraussetzungen
 - Verwenden Sie die Azure CLI, um Azure Stack zu [installieren und eine Verbindung herzustellen](azure-stack-version-profiles-azurecli2.md).
 - Laden Sie die Dateien *azuredeploy.json* und *azuredeploy.parameters.json* aus der [Beispielvorlage zum Erstellen von Speicherkonten](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account) herunter.
 
## <a name="deploy-template"></a>Bereitstellen der Vorlage
Navigieren Sie zu dem Ordner, in den diese Dateien heruntergeladen wurden, und führen Sie den folgenden Befehl zum Bereitstellen der Vorlage aus:

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

Dieser Befehl stellt die Vorlage für die Ressourcengruppe **cliRG** am Standardspeicherort für Azure Stack POC bereit.

## <a name="validate-template-deployment"></a>Überprüfen der Vorlagenbereitstellung
Um diese Ressourcengruppe und das Speicherkonto anzuzeigen, verwenden Sie die folgenden Befehle:

    azure group list

    azure storage account list




