---
title: Programmgesteuertes Erstellen von Richtlinien und Anzeigen von Konformitätsdaten mit Azure Policy | Microsoft-Dokumentation
description: In diesem Artikel wird das programmgesteuerte Erstellen und Verwalten von Richtlinien für Azure Policy Schritt für Schritt beschrieben.
services: azure-policy
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 03/28/2018
ms.topic: article
ms.service: azure-policy
manager: carmonm
ms.custom: ''
ms.openlocfilehash: 1809f0b7ef386bb9eeaa55982178e4cd5e1dd2e2
ms.sourcegitcommit: 34e0b4a7427f9d2a74164a18c3063c8be967b194
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="programmatically-create-policies-and-view-compliance-data"></a>Programmgesteuertes Erstellen von Richtlinien und Anzeigen von Konformitätsdaten

In diesem Artikel wird das programmgesteuerte Erstellen und Verwalten von Richtlinien Schritt für Schritt beschrieben. Außerdem wird veranschaulicht, wie Sie Konformitätszustände und -richtlinien für Ressourcen anzeigen. Mit Richtliniendefinitionen werden verschiedene Regeln und Aktionen für Ihre Ressourcen erzwungen. Durch die Erzwingung wird sichergestellt, dass die Ressourcen stets konform mit Ihren Unternehmensstandards und Vereinbarungen zum Servicelevel bleiben.

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie zunächst sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. Installieren Sie den [ARMClient](https://github.com/projectkudu/ARMClient), falls Sie dies noch nicht durchgeführt haben. Mit diesem Tool werden HTTP-Anforderungen an Azure Resource Manager-basierte APIs gesendet.
2. Aktualisieren Sie Ihr AzureRM-PowerShell-Modul auf die neueste Version. Weitere Informationen zur aktuellen Version finden Sie unter „Azure PowerShell“ https://github.com/Azure/azure-powershell/releases.
3. Registrieren Sie den Ressourcenanbieter „Policy Insights“ über Azure PowerShell, um sicherzustellen, dass Ihr Abonnement für den Ressourcenanbieter funktioniert. Um einen Ressourcenanbieter zu registrieren, benötigen Sie die Berechtigungen zum Ausführen des Vorgangs „Aktion registrieren“ für den Ressourcenanbieter. Dieser Vorgang ist in den Rollen „Mitwirkender“ und „Besitzer“ enthalten. Führen Sie den folgenden Befehl aus, um den Ressourcenanbieter zu registrieren:

    ```
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.PolicyInsights
    ```

    Weitere Informationen zum Registrieren und Anzeigen von Ressourcenanbietern finden Sie unter [Ressourcenanbieter und -typen](../azure-resource-manager/resource-manager-supported-services.md).

4. Installieren Sie die Azure CLI, falls Sie dies noch nicht getan haben. Sie finden die aktuelle Version unter [Installieren der Azure CLI 2.0 unter Windows](/azure/install-azure-cli-windows?view=azure-cli-latest).

## <a name="create-and-assign-a-policy-definition"></a>Erstellen und Zuweisen einer Richtliniendefinition

Im ersten Schritt zur besseren Sichtbarkeit Ihrer Ressourcen werden Richtlinien für die Ressourcen erstellt und zugewiesen. Im nächsten Schritt erfahren Sie, wie Sie eine Richtlinie programmgesteuert erstellen und zuweisen. Mit der Beispielrichtlinie werden Speicherkonten überprüft, die für alle öffentlichen Netzwerke offen sind, indem PowerShell, Azure CLI und HTTP-Anforderungen verwendet werden.

Mit den folgenden Befehlen werden Richtliniendefinitionen für den Standard-Tarif erstellt. Der Standard-Tarif ermöglicht eine skalierbare Verwaltung, Konformitätsbewertung und Problembehandlung. Weitere Informationen zu Tarifen finden Sie unter [Azure Policy – Preise](https://azure.microsoft.com/pricing/details/azure-policy).

### <a name="create-and-assign-a-policy-definition-with-powershell"></a>Erstellen und Zuweisen einer Richtliniendefinition mit PowerShell

1. Verwenden Sie den folgenden JSON-Codeausschnitt, um eine JSON-Datei mit dem Namen „AuditStorageAccounts.json“ zu erstellen.

    ```
    {
    "if": {
      "allOf": [
        {
          "field": "type",
          "equals": "Microsoft.Storage/storageAccounts"
        },
        {
          "field": "Microsoft.Storage/storageAccounts/networkAcls.defaultAction",
          "equals": "Allow"
        }
      ]
    },
    "then": {
      "effect": "audit"
    }
  }

    ```

    Weitere Informationen zum Erstellen einer Richtliniendefinition finden Sie unter [Struktur von Azure Policy-Definitionen](policy-definition.md).

2. Führen Sie den folgenden Befehl aus, um mit der Datei „AuditStorageAccounts.json“ eine Richtliniendefinition zu erstellen.

    ```
    PS C:\>New-AzureRmPolicyDefinition -Name "AuditStorageAccounts" -DisplayName "Audit Storage Accounts Open to Public Networks" -Policy C:\AuditStorageAccounts.json
    ```

    Mit dem Befehl wird die Richtliniendefinition _Audit Storage Accounts Open to Public Networks_ erstellt. Weitere Informationen zu anderen Parametern, die Sie verwenden können, finden Sie unter [New-AzureRmPolicyDefinition](/powershell/module/azurerm.resources/new-azurermpolicydefinition?view=azurermps-4.4.1).

3. Nach dem Erstellen der Richtliniendefinition können Sie eine Richtlinienzuweisung erstellen. Führen Sie dazu die folgenden Befehle aus:

    ```
$rg = Get-AzureRmResourceGroup -Name "ContosoRG"
```

    ```
$Policy = Get-AzureRmPolicyDefinition -Name "AuditStorageAccounts"
    ```

    ```
New-AzureRmPolicyAssignment -Name "AuditStorageAccounts" -PolicyDefinition $Policy -Scope $rg.ResourceId –Sku @{Name='A1';Tier='Standard'}
    ```

    Ersetzen Sie _ContosoRG_ durch den Namen Ihrer gewünschten Ressourcengruppe.

Weitere Informationen zum Verwalten von Ressourcenrichtlinien unter Verwendung des Azure Resource Manager-PowerShell-Moduls finden Sie unter [AzureRM.Resources](/powershell/module/azurerm.resources/?view=azurermps-4.4.1#policies).

### <a name="create-and-assign-a-policy-definition-using-armclient"></a>Erstellen und Zuweisen einer Richtliniendefinition per ARMClient

Verwenden Sie das folgende Verfahren, um eine Richtliniendefinition zu erstellen.

1. Kopieren Sie den folgenden JSON-Codeausschnitt, um eine JSON-Datei zu erstellen. Sie rufen die Datei im nächsten Schritt auf.

    ```
    {
    "properties": {
        "displayName": "Audit Storage Accounts Open to Public Networks",
        "policyType": "Custom",
        "mode": "Indexed",
        "description": "This policy ensures that storage accounts with exposure to Public Networks are audited.",
        "parameters": {},
        "policyRule": {
              "if": {
                "allOf": [
                  {
                    "field": "type",
                    "equals": "Microsoft.Storage/storageAccounts"
                  },
                  {
                    "field": "Microsoft.Storage/storageAccounts/networkAcls.defaultAction",
                    "equals": "Allow"
                  }
                ]
              },
              "then": {
                "effect": "audit"
              }
            }
    }
}
```

2. Erstellen Sie die Richtliniendefinition, indem Sie den folgenden Aufruf verwenden:

    ```
    armclient PUT "/subscriptions/<subscriptionId>/providers/Microsoft.Authorization/policyDefinitions/AuditStorageAccounts?api-version=2016-12-01 @<path to policy definition JSON file>"
    ```

    Ersetzen Sie die vorangestellte &lt;subscriptionId&gt; durch die ID Ihres jeweiligen Abonnements.

Weitere Informationen zur Struktur der Abfrage finden Sie unter [Richtliniendefinitionen – Create oder Update](/rest/api/resources/policydefinitions/createorupdate).


Verwenden Sie das folgende Verfahren, um eine Richtlinienzuweisung zu erstellen und die Richtliniendefinition auf Ressourcengruppenebene zuzuweisen.

1. Kopieren Sie den folgenden JSON-Codeausschnitt, um eine Datei mit einer JSON-Richtlinienzuweisung zu erstellen. Ersetzen Sie die in &lt;&gt; gesetzten Angaben durch Ihre eigenen Werte.

    ```
    {
  "properties": {
"description": "This policy assignment makes sure that storage accounts with exposure to Public Networks are audited.",
"displayName": "Audit Storage Accounts Open to Public Networks Assignment",
"parameters": {},
"policyDefinitionId":"/subscriptions/<subscriptionId>/providers/Microsoft.Authorization/policyDefinitions/Audit Storage Accounts Open to Public Networks",
"scope": "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>"
},
"sku": {
    "name": "A1",
    "tier": "Standard"
    }
}
    ```

2. Erstellen Sie die Richtlinienzuweisung, indem Sie den folgenden Aufruf verwenden:

    ```
    armclient PUT "/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Authorization/policyAssignments/Audit Storage Accounts Open to Public Networks?api-version=2017-06-01-preview" @<path to Assignment JSON file>
    ```

    Ersetzen Sie die in &lt;&gt; gesetzten Angaben durch Ihre eigenen Werte.

 Weitere Informationen zur Durchführung von HTTP-Aufrufen für die REST-API finden Sie unter [Azure-REST-API-Ressourcen](/rest/api/resources/).

### <a name="create-and-assign-a-policy-definition-with-azure-cli"></a>Erstellen und Zuweisen einer Richtliniendefinition mit der Azure-Befehlszeilenschnittstelle

Verwenden Sie das folgende Verfahren, um eine Richtliniendefinition zu erstellen:

1. Kopieren Sie den folgenden JSON-Codeausschnitt, um eine Datei mit einer JSON-Richtlinienzuweisung zu erstellen.

    ```
    {
                  "if": {
                    "allOf": [
                      {
                        "field": "type",
                        "equals": "Microsoft.Storage/storageAccounts"
                      },
                      {
                        "field": "Microsoft.Storage/storageAccounts/networkAcls.defaultAction",
                        "equals": "Allow"
                      }
                    ]
                  },
                  "then": {
                    "effect": "audit"
                  }
    }
    ```

2. Führen Sie den folgenden Befehl aus, um eine Richtliniendefinition zu erstellen:

    ```
az policy definition create --name 'audit-storage-accounts-open-to-public-networks' --display-name 'Audit Storage Accounts Open to Public Networks' --description 'This policy ensures that storage accounts with exposures to public networks are audited.' --rules '<path to json file>' --mode All
    ```

Verwenden Sie den folgenden Befehl, um eine Richtlinienzuweisung zu erstellen. Ersetzen Sie die in &lt;&gt; gesetzten Angaben durch Ihre eigenen Werte.

```
az policy assignment create --name '<Audit Storage Accounts Open to Public Networks in Contoso RG' --scope '<scope>' --policy '<policy definition ID>' --sku 'standard'
```

Sie können die ID der Richtliniendefinition abrufen, indem Sie PowerShell mit dem folgenden Befehl verwenden:

```
az policy definition show --name 'Audit Storage Accounts with Open Public Networks'
```

Die ID für die Richtliniendefinition, die Sie erstellt haben, sollte in etwa wie im folgenden Beispiel aussehen:

```
"/subscription/<subscriptionId>/providers/Microsoft.Authorization/policyDefinitions/Audit Storage Accounts Open to Public Networks"
```

Weitere Informationen zum Verwalten von Ressourcenrichtlinien mit der Azure-Befehlszeilenschnittstelle finden Sie unter [Azure CLI-Ressourcenrichtlinien](/cli/azure/policy?view=azure-cli-latest).

## <a name="identify-non-compliant-resources"></a>Identifizieren nicht konformer Ressourcen

In einer Zuweisung ist eine Ressource nicht konform, wenn dafür die Richtlinien- oder Initiativenregeln nicht eingehalten werden. Die folgende Tabelle gibt Aufschluss über das Zusammenspiel zwischen den verschiedenen Richtlinienaktionen, der Bedingungsauswertung und dem resultierenden Konformitätszustand:

| **Ressourcenzustand** | **Aktion** | **Richtlinienauswertung** | **Konformitätszustand** |
| --- | --- | --- | --- |
| Exists | Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\* | True | Nicht konform |
| Exists | Deny, Audit, Append\*, DeployIfNotExist\*, AuditIfNotExist\* | False | Konform |
| Neu | Audit, AuditIfNotExist\* | True | Nicht konform |
| Neu | Audit, AuditIfNotExist\* | False | Konform |

\* Für die Aktionen Append, DeployIfNotExist und AuditIfNotExist muss die IF-Anweisung auf TRUE festgelegt sein. Für die Aktionen muss die Existenzbedingung außerdem auf FALSE festgelegt sein, damit sie nicht konform sind. Bei TRUE löst die IF-Bedingung die Auswertung der Existenzbedingung für die zugehörigen Ressourcen aus.

Um zu verdeutlichen, wie Ressourcen als nicht konform gekennzeichnet werden, verwenden wir das oben erstellte Beispiel zur Richtlinienzuweisung.

Angenommen, Sie verfügen über die Ressourcengruppe ContosoRG mit einigen Speicherkonten (rot hervorgehoben), die in öffentlichen Netzwerken verfügbar gemacht werden.

![In öffentlichen Netzwerken verfügbar gemachte Speicherkonten](./media/policy-insights/resource-group01.png)

In diesem Beispiel ist Vorsicht aufgrund von Sicherheitsrisiken geboten. Nachdem Sie nun eine Richtlinienzuweisung erstellt haben, wird sie für alle Speicherkonten in der Ressourcengruppe ContosoRG ausgewertet. Sie überprüft die drei nicht konformen Speicherkonten und ändert den Status daher jeweils in **nicht konform**.

![Überwachte nicht konforme Speicherkonten](./media/policy-insights/resource-group03.png)

Verwenden Sie das folgende Verfahren zum Identifizieren von Ressourcen in einer Ressourcengruppe, die nicht mit der Richtlinienzuweisung konform sind. In diesem Beispiel sind die Ressourcen Speicherkonten in der Ressourcengruppe ContosoRG.

1. Rufen Sie die ID der Richtlinienzuweisung ab, indem Sie die folgenden Befehle ausführen:

    ```
    $policyAssignment = Get-AzureRmPolicyAssignment | where {$_.properties.displayName -eq "Audit Storage Accounts with Open Public Networks"}
    ```

    ```
    $policyAssignment.PolicyAssignmentId
    ```

    Weitere Informationen zum Abrufen der ID einer Richtlinienzuweisung finden Sie unter [Get-AzureRMPolicyAssignment](https://docs.microsoft.com/en-us/powershell/module/azurerm.resources/Get-AzureRmPolicyAssignment?view=azurermps-4.4.1).

2. Führen Sie den folgenden Befehl aus, um die Ressourcen-IDs der nicht konformen Ressourcen in eine JSON-Datei zu kopieren:

    ```
    armclient post "/subscriptions/<subscriptionID>/resourceGroups/<rgName>/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2017-12-12-preview&$filter=IsCompliant eq false and PolicyAssignmentId eq '<policyAssignmentID>'&$apply=groupby((ResourceId))" > <json file to direct the output with the resource IDs into>
    ```

3. Die Ergebnisse sollten in etwa wie im folgenden Beispiel aussehen:

  ```
      {
  "@odata.context":"https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest",
  "@odata.count": 3,
  "value": [
  {
      "@odata.id": null,
      "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
        "ResourceId": "/subscriptions/<subscriptionId>/resourcegroups/<rgname>/providers/microsoft.storage/storageaccounts/<storageaccount1Id>"
      },
      {
        "@odata.id": null,
        "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
        "ResourceId": "/subscriptions/<subscriptionId>/resourcegroups/<rgname>/providers/microsoft.storage/storageaccounts/<storageaccount2Id>"
             },
  {
        "@odata.id": null,
        "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
        "ResourceId": "/subscriptions/<subscriptionName>/resourcegroups/<rgname>/providers/microsoft.storage/storageaccounts/<storageaccount3ID>"
             }
  ]
  }
  ```

Die Ergebnisse entsprechen in etwa dem, was üblicherweise in der [Azure-Portalansicht](assign-policy-definition.md#identify-non-compliant-resources) unter **Nicht konforme Ressourcen** zu sehen ist.

Derzeit werden nicht konforme Ressourcen nur über das Azure-Portal und mit HTTP-Anforderungen identifiziert. Weitere Informationen zum Abfragen von Richtlinienzuständen finden Sie im API-Referenzartikel zum [Richtlinienstatus](/rest/api/policy-insights/policystates).

## <a name="view-policy-events"></a>Anzeigen von Richtlinienereignissen

Wenn eine Ressource erstellt oder aktualisiert wird, wird ein Ergebnis der Richtlinienauswertung generiert. Diese Ergebnisse werden als _Richtlinienereignisse_ bezeichnet. Führen Sie die folgende Abfrage aus, um alle Richtlinienereignisse anzuzeigen, die der Richtlinienzuweisung zugeordnet sind.

```
armclient POST "/subscriptions/<subscriptionId>/providers/Microsoft.Authorization/policyDefinitions/Audit Storage Accounts Open to Public Networks/providers/Microsoft.PolicyInsights/policyEvents/default/queryResults?api-version=2017-12-12-preview"
```

Ihre Ergebnisse sollten in etwa wie im folgenden Beispiel aussehen:

```
{
  "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyEvents/$metadata#default",
  "@odata.count": 1,
  "value": [
    {
      "@odata.id": null,
      "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyEvents/$metadata#default/$entity",
      "NumAuditEvents": 3
    }
  ]
}

```

Wie Richtlinienzustände auch, können Richtlinienereignisse nur mit HTTP-Anforderungen angezeigt werden. Weitere Informationen zum Abfragen von Richtlinienereignissen finden Sie im Referenzartikel zu [Richtlinienereignissen](/rest/api/policy-insights/policyevents).

## <a name="change-a-policy-assignments-pricing-tier"></a>Ändern des Tarifs einer Richtlinienzuweisung

Sie können das PowerShell-Cmdlet *Set-AzureRmPolicyAssignment* verwenden, um den Tarif für eine vorhandene Richtlinienzuweisung auf Standard oder Free zu aktualisieren. Beispiel: 

```
Set-AzureRmPolicyAssignment -Id /subscriptions/<subscriptionId/resourceGroups/<resourceGroupName>/providers/Microsoft.Authorization/policyAssignments/<policyAssignmentID> -Sku @{Name='A1';Tier='Standard'}
```

Weitere Informationen zum Cmdlet finden Sie unter [Set-AzureRmPolicyAssignment](/powershell/module/azurerm.resources/Set-AzureRmPolicyAssignment?view=azurermps-4.4.1).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den in diesem Artikel verwendeten Befehlen und Abfragen finden Sie in den folgenden Artikeln.

- [Azure-REST-API-Ressourcen](/rest/api/resources/)
- [Azure RM-PowerShell-Module](/powershell/module/azurerm.resources/?view=azurermps-4.4.1#policies)
- [Befehle für Azure CLI-Richtlinien](/cli/azure/policy?view=azure-cli-latest)
- [Ressourcenanbieter „Policy Insights“ – REST-API-Referenz](/rest/api/policy-insights)
