---
title: Verwalten von Logik-Apps mit Visual Studio – Azure Logic Apps | Microsoft-Dokumentation
description: Verwalten von Logik-Apps und anderen Azure-Ressourcen mit dem Cloud-Explorer von Visual Studio
author: ecfan
manager: SyntaxC4
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: ''
ms.service: logic-apps
ms.workload: logic-apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: mvc
ms.date: 03/15/2018
ms.author: estfan; LADocs
ms.openlocfilehash: db847d5fa3d5f5b2b2f0293f1756226870a8b47e
ms.sourcegitcommit: 8aab1aab0135fad24987a311b42a1c25a839e9f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2018
---
# <a name="manage-logic-apps-with-visual-studio"></a>Verwalten von Logik-Apps mit Visual Studio

Sie können Logik-Apps zwar auch im <a href="https://portal.azure.com" target="_blank">Azure-Portal</a> erstellen, bearbeiten, verwalten und bereitstellen, aber Visual Studio können Sie auch verwenden, wenn Sie Logik-Apps der Quellcodeverwaltung hinzufügen, unterschiedliche Versionen veröffentlichen und [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-Vorlagen für verschiedene Bereitstellungsumgebungen erstellen möchten. Mit dem Cloud-Explorer von Visual Studio können Sie Ihre Logik-Apps zusammen mit anderen Azure-Ressourcen suchen und verwalten. Sie können z.B. bereits im Azure-Portal bereitgestellte Logik-Apps öffnen, herunterladen, bearbeiten, ausführen, ihren Ausführungsverlauf anzeigen, sie deaktivieren und aktivieren. Wenn die Arbeit mit Azure Logic Apps in Visual Studio für Sie neu ist, lernen Sie, [Logik-Apps mit Visual Studio zu erstellen](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).

> [!IMPORTANT]
> Bereitstellen oder Veröffentlichen einer Logik-App von Visual Studio aus überschreibt die Version dieser App im Azure-Portal. Wenn Sie also Änderungen im Azure-Portal vornehmen, die Sie beibehalten möchten, achten Sie darauf, dass Sie [die Logik-App in Visual Studio](#refresh) vom Azure-Portal aus aktualisieren, bevor Sie sie das nächste Mal von Visual Studio aus bereitstellen oder veröffentlichen.

<a name="requirements"></a>

## <a name="prerequisites"></a>Voraussetzungen

* Wenn Sie nicht über ein Azure-Abonnement verfügen, können Sie sich <a href="https://azure.microsoft.com/free/" target="_blank">für ein kostenloses Azure-Konto registrieren</a>.

* Laden Sie diese Tools herunter, und installieren Sie sie, falls sie noch nicht vorhanden sind: 

  * <a href="https://www.visualstudio.com/downloads" target="_blank">Visual Studio 2017 oder Visual Studio 2015 – Community Edition oder höher</a>. 
  In dieser Schnellstartanleitung wird die kostenlose Version Visual Studio Community 2017 verwendet.

  * <a href="https://azure.microsoft.com/downloads/" target="_blank">Azure SDK (2.9.1 oder höher)</a> und <a href="https://github.com/Azure/azure-powershell#installation" target="_blank">Azure PowerShell</a>

  * <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551" target="_blank">Azure Logic Apps-Tools für Visual Studio 2017</a> oder <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio" target="_blank">Visual Studio 2015</a> 
  
    Sie können die Azure Logic Apps-Tools entweder direkt vom Visual Studio Marketplace herunterladen und installieren oder sich über das <a href="https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions" target="_blank">Installieren dieser Erweiterung aus Visual Studio</a> informieren. 
    Achten Sie darauf, dass Sie Visual Studio nach Abschluss der Installation neu starten.

* Internetzugriff bei Verwendung des eingebetteten Logik-App-Designers

  Für den Designer ist eine Internetverbindung zum Erstellen von Ressourcen in Azure und zum Lesen der Eigenschaften und Daten von Connectors in Ihrer Logik-App erforderlich. 
  Wenn Sie beispielsweise den Dynamics CRM Online-Connector verwenden, prüft der Designer Ihre CRM-Instanz auf verfügbare standardmäßige und benutzerdefinierte Eigenschaften.

<a name="find-logic-apps-vs"></a>

## <a name="find-your-logic-apps"></a>Suchen nach Ihren Logik-Apps

In Visual Studio finden Sie alle Logik-Apps, die Ihrem Azure-Abonnement zugeordnet sind und mithilfe von Cloud-Explorer im Azure-Portal bereitgestellt werden.

1. Öffnen Sie Visual Studio. Wählen Sie im Menü **Ansicht** die Option **Cloud-Explorer** aus.

2. Wählen Sie im Cloud-Explorer **Kontenverwaltung** aus. Wählen Sie das Azure-Abonnement aus, dem Ihre Logik-Apps zugeordnet sind, und wählen Sie dann **Übernehmen** aus. Beispiel: 

   ![„Kontenverwaltung“ auswählen](./media/manage-logic-apps-with-visual-studio/account-management-select-Azure-subscription.png)

2. Je nachdem, ob Sie nach **Ressourcengruppen** oder **Ressourcentypen** suchen, gehen Sie folgendermaßen vor:

   * **Ressourcengruppen**: Unter Ihrem Azure-Abonnement zeigt der Cloud-Explorer alle Ressourcengruppen an, die diesem Abonnement zugeordnet sind. 
   Erweitern Sie die Ressourcengruppe, die die Logik-App enthält, und wählen Sie dann Ihre Logik-App aus.

   * **Ressourcentypen**: Erweitern Sie unter Ihrem Azure-Abonnement **Logik-Apps**. Sobald der Cloud-Explorer alle bereitgestellten Logik-Apps anzeigt, die Ihrem Abonnement zugeordnet sind, wählen Sie Ihre Logik-App aus.

<a name="open-designer"></a>

## <a name="open-in-visual-studio"></a>Öffnen in Visual Studio

In Visual Studio können Sie Logik-Apps öffnen, die zuvor entweder direkt über das Azure-Portal oder als Azure Resource Manager-Projekte mit Visual Studio erstellt und bereitgestellt worden sind.

1. Öffnen Sie den Cloud-Explorer, und suchen Sie Ihre Logik-App. 

2. Wählen Sie im Kontextmenü der Logik-App **Mit Logik-App-Editor öffnen** aus.

   Dieses Beispiel zeigt die Logik-Apps nach Ressourcentyp an, sodass Ihre Logik-Apps im Abschnitt **Logik-Apps** angezeigt werden.

  ![Bereitgestellte Logik-Apps vom Azure-Portal aus öffnen](./media/manage-logic-apps-with-visual-studio/open-logic-app-in-editor.png)

   Sobald die Logik-App am unteren Rand des Logik-App-Designers angezeigt wird, können Sie **Codeansicht** auswählen, um die zugrunde liegende Definitionsstruktur der Logik-App zu überprüfen. 
   Wenn Sie eine Bereitstellungsvorlage für die Logik-App erstellen möchten, informieren Sie sich, wie Sie für diese Logik-App [eine Azure Resource Manager-Vorlage herunterladen](#download-logic-app) können. Weitere Informationen zu [Resource Manager-Vorlagen](../azure-resource-manager/resource-group-overview.md#template-deployment).

<a name="download-logic-app"></a>

## <a name="download-from-azure"></a>Herunterladen aus Azure

Sie können Logik-Apps aus dem <a href="https://portal.azure.com" target="_blank">Azure-Portal</a> herunterladen und sie als [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-Vorlagen speichern. Sie können die Vorlagen dann lokal mit Visual Studio bearbeiten und Logik-Apps für verschiedene Bereitstellungsumgebungen anpassen. Das Herunterladen von Logik-Apps *parametrisiert* automatisch deren Definitionen in [Resource Manager-Vorlagen](../azure-resource-manager/resource-group-overview.md#template-deployment), die auch JavaScript Object Notation (JSON) verwenden.

1. Öffnen Sie in Visual Studio den Cloud-Explorer, suchen Sie die Logik-App, die Sie aus Azure herunterladen möchten, und wählen Sie sie aus.

2. Wählen Sie im Kontextmenü der Logik-App **Mit Logik-App-Editor öffnen** aus.

   Der Logik-App-Designer wird geöffnet und zeigt die Logik-App an. 
   Um die zugrunde liegende Definition und Struktur der Logik-App zu überprüfen, wählen Sie am unteren Rand des Designers **Codeansicht** aus. 

3. Wählen Sie auf der Symbolleiste des Designers die Option **Herunterladen** aus.

   ![„Herunterladen“ auswählen](./media/manage-logic-apps-with-visual-studio/download-logic-app.png)

4. Wenn Sie aufgefordert werden, einen Speicherort einzugeben, navigieren Sie zu diesem Speicherort, und speichern Sie die Resource Manager-Vorlage für die Definition der Logik-App im JSON-Dateiformat (.json). 

Die Definition der Logik-App wird im `resources`-Unterabschnitt der Resource Manager-Vorlage angezeigt. Sie können nun die Definition der Logik-App und Resource Manager-Vorlage mit Visual Studio bearbeiten. Sie können die Vorlage auch als Azure Resource Manager-Projekt einer Visual Studio-Projektmappe hinzufügen. Erfahren Sie mehr über [Resource Manager-Projekte für Logik-Apps in Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md). 

<a name="refresh"></a>

## <a name="refresh-from-azure"></a>Aktualisieren von Azure aus

Wenn Sie Ihre Logik-App im Azure-Portal bearbeiten und die Änderungen beibehalten möchten, stellen Sie sicher, dass Sie die Version dieser App in Visual Studio mit diesen Änderungen aktualisieren. 

* Wählen Sie in Visual Studio auf der Logik-App-Designer-Symbolleiste **Aktualisieren** aus.

  Oder

* Öffnen Sie im Cloud-Explorer von Visual Studio das Kontextmenü Ihrer Logik-App, und wählen Sie **Aktualisieren** aus. 

![Logik-App mit Updates aktualisieren](./media/manage-logic-apps-with-visual-studio/refresh-logic-app.png)

## <a name="publish-logic-app-updates"></a>Veröffentlichen von Logik-App-Updates

Wenn Sie bereit sind, Ihre Logik-App-Updates von Visual Studio aus in Azure bereitzustellen, wählen Sie auf der Logik-App-Designer-Symbolleiste **Veröffentlichen** aus.

![Aktualisierte Logik-App veröffentlichen](./media/manage-logic-apps-with-visual-studio/publish-logic-app.png)

## <a name="manually-run-your-logic-app"></a>Manuelles Ausführen Ihrer Logik-App

Sie können eine von Visual Studio aus in Azure bereitgestellte Logik-App manuell auslösen. Wählen Sie auf der Symbolleiste des Logik-App-Designers **Trigger ausführen** aus.

![Logik-App manuell ausführen](./media/manage-logic-apps-with-visual-studio/manually-run-logic-app.png)

## <a name="review-run-history"></a>Überprüfen des Ausführungsverlaufs

Um den Status zu überprüfen und Probleme mit Logik-App-Ausführungen zu diagnostizieren, können Sie die Details wie Eingaben und Ausgaben für solche Ausführungen in Visual Studio überprüfen.

1. Öffnen Sie im Cloud-Explorer das Kontextmenü Ihrer Logik-App, und wählen Sie **Ausführungsverlauf öffnen** aus.

   ![„Ausführungsverlauf öffnen“](./media/manage-logic-apps-with-visual-studio/view-run-history.png)

2. Um die Details für eine bestimmte Ausführung anzuzeigen, doppelklicken Sie auf eine Ausführung. Beispiel: 

   ![Detaillierter Ausführungsverlauf](./media/manage-logic-apps-with-visual-studio/view-run-history-details.png)
  
   > [!TIP]
   > Wählen Sie zum Sortieren der Tabelle nach Eigenschaft die Spaltenüberschrift für diese Eigenschaft aus. 

3. Erweitern Sie die Schritte, deren Eingaben und Ausgaben Sie überprüfen möchten. Beispiel: 

   ![Eingaben und Ausgaben für jeden Schritt anzeigen](./media/manage-logic-apps-with-visual-studio/run-inputs-outputs.png)

## <a name="disable-or-enable-logic-app"></a>Deaktivieren oder Aktivieren der Logik-App

Ohne Ihre Logik-App zu löschen, können Sie verhindern, dass der Trigger ausgelöst wird, wenn die Auslöserbedingung das nächste Mal erfüllt ist. Das Deaktivieren Ihrer Logik-App verhindert, dass das Logic Apps-Modul zukünftige Workflowinstanzen für Ihre Logik-App erstellt und ausführt.
Öffnen Sie im Cloud-Explorer das Kontextmenü Ihrer Logik-App, und wählen Sie **Deaktivieren** aus.

![Ihre Logik-App deaktivieren](./media/manage-logic-apps-with-visual-studio/disable-logic-app.png)

Wenn Sie wünschen, dass Ihre Logik-App den Betrieb fortsetzt, können Sie Ihre Logik-App erneut aktivieren. Öffnen Sie im Cloud-Explorer das Kontextmenü Ihrer Logik-App, und wählen Sie **Aktivieren** aus.

![Ihre Logik-App aktivieren](./media/manage-logic-apps-with-visual-studio/enable-logic-app.png)

## <a name="delete-your-logic-app"></a>Löschen Ihrer Logik-App

Um Ihre Logik-App aus dem Azure-Portal zu löschen, öffnen Sie im Cloud-Explorer das Kontextmenü Ihrer Logik-App, und wählen Sie **Löschen** aus.

![Löschen Ihrer Logik-App](./media/manage-logic-apps-with-visual-studio/delete-logic-app.png)

## <a name="next-steps"></a>Nächste Schritte

In diesem Artikel haben Sie gelernt, bereitgestellte Logik-Apps mit Visual Studio zu verwalten. Als Nächstes lernen Sie, Logik-App-Definitionen für die Bereitstellung anzupassen:

> [!div class="nextstepaction"]
> [Erstellen von Logik-App-Definitionen in JSON](../logic-apps/logic-apps-author-definitions.md)