---
title: "Verwalten von App Service-Plänen in Azure | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie verschiedene Aufgaben zum Verwalten eines App Service-Plans ausführen."
keywords: "App Service, Azure App Service, Skalierung, App Services-Plan, ändern, verwalten, Verwaltung"
services: app-service
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 4859d0d5-3e3c-40cc-96eb-f318b2c51a3d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: cephalin
ms.openlocfilehash: 1dfe8a903e19ff524a1c4a0228e6aefcbe9ff183
ms.sourcegitcommit: 059dae3d8a0e716adc95ad2296843a45745a415d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="manage-an-app-service-plan-in-azure"></a>Verwalten eines App Service-Plans in Azure

Ein [Azure App Service-Plan](azure-web-sites-web-hosting-plans-in-depth-overview.md) stellt Ressourcen bereit, die zum Ausführen einer App Service-App erforderlich sind. Diese Anleitung veranschaulicht das Verwalten eines App Service-Plans.

## <a name="create-an-app-service-plan"></a>Wie erstelle ich einen Plan?

> [!TIP]
> Falls Sie eine App Service-Umgebung haben, finden Sie Informationen dazu im Abschnitt [Create an App Service plan (Erstellen eines App Service-Plans)](environment/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan).

Sie können einen leeren App Service-Plan erstellen; Sie können einen Plan aber auch im Rahmen der App-Erstellung erstellen.

1. Klicken Sie im [Azure-Portal](https://portal.azure.com) auf **Neu** > **Web + Mobil**, und wählen Sie dann die Option **Web-App** oder eine andere Art von App Service-App aus.

2. Wählen Sie einen vorhandenen App Service-Plan auswählen, oder erstellen Sie einen Plan für die neue App.

   ![Erstellen Sie eine App im Azure-Portal.][createWebApp]

   So erstellen Sie einen Plan:

   a. Wählen Sie **+ Neu erstellen** aus.

      ![Erstellen eines App Service-Plans][createASP] 

   b. Geben Sie einen Namen für Ihren **App Service-Plan** ein.

   c. Wählen Sie unter **Speicherort** einen geeigneten Speicherort aus.

   d. Wählen Sie einen geeigneten **Tarif** für den Dienst aus. Wählen Sie **Alle anzeigen** aus, um mehr Tarifoptionen anzuzeigen, z. B. **Free** und **Shared**. Klicken Sie nach dem Auswählen des Tarifs auf die Schaltfläche **Auswählen**.

<a name="move"></a>

## <a name="move-an-app-to-another-app-service-plan"></a>Verschieben einer App in einen anderen App Service-Plan

Sie können eine App in einen anderen App Service-Plan verschieben, solange sich der Quellplan und der Zielplan in der _gleichen Ressourcengruppe und geografischen Region_ befinden.

1. Navigieren Sie im [Azure-Portal](https://portal.azure.com) zu der App, die Sie verschieben möchten.

2. Suchen Sie im Menü nach dem Abschnitt **App Service-Plan**.

3. Wählen Sie **App Service-Plan ändern** aus, um die Auswahlfunktion für den **App Service-Plan** zu öffnen.

   ![Auswahlelement für App Service-Pläne][change] 

4. Wählen Sie in der Auswahlfunktion **App Service-Plan** einen vorhandenen Plan aus, in den Sie die App verschieben möchten.   

> [!IMPORTANT]
> Die Seite **App Service-Plan auswählen** wird anhand der folgenden Kriterien gefiltert: 
> - In derselben Ressourcengruppe vorhanden 
> - In derselben geografischen Region vorhanden 
> - Im selben Webspace vorhanden  
> 
> Ein _Webspace_ ist ein logisches Konstrukt in App Service, das eine Gruppierung von Serverressourcen definiert. Eine geografische Region (z.B. „USA, Westen“) enthält viele Webspaces, um Kunden zuzuordnen, die App Service verwenden. Zurzeit können Sie App Service-Ressourcen nicht zwischen verschiedenen Webspaces verschieben. 
> 

[!INCLUDE [app-service-dev-test-note](../../includes/app-service-dev-test-note.md)]

Jeder Plan hat einen eigenen Tarif. Wenn Sie beispielsweise eine Website aus einem **Free**-Tarif in einen **Standard**-Tarif verschieben, können alle zugewiesenen Apps die Features und Ressourcen des **Standard**-Tarifs nutzen. Allerdings bedeutet das Verschieben einer App von einem Plan mit einem höheren Tarif in einen Plan mit einem niedrigeren Tarif, dass Sie keinen Zugriff mehr auf bestimmte Features haben. Wenn Ihre Anwendung ein Feature verwendet, das im Zielplan nicht verfügbar ist, erhalten Sie eine Fehlermeldung, die anzeigt, welches Feature verwendet wird, das nicht verfügbar ist. 

Wenn beispielsweise eine Ihrer Apps SSL-Zertifikate verwendet, wird Ihnen möglicherweise folgende Fehlermeldung angezeigt:

`Cannot update the site with hostname '<app_name>' because its current SSL configuration 'SNI based SSL enabled' is not allowed in the target compute mode. Allowed SSL configuration is 'Disabled'.`

In diesem Fall müssen Sie einen der folgenden Schritte ausführen, bevor Sie die App in den Zielplan verschieben können:
- Skalieren Sie den Tarif des Zielplans zentral auf **Basic** oder einen höheren Tarif hoch.
- Entfernen Sie alle SSL-Verbindungen mit Ihrer App.

## <a name="move-an-app-to-a-different-region"></a>Verschieben einer App in eine andere Region

Die Region, in der Ihre App ausgeführt wird, ist die Region des App Service-Plans, in dem sie sich befindet. Sie können die Region eines App Service-Plans jedoch nicht ändern. Wenn Sie die App in einer anderen Region ausführen möchten, ist das Klonen der App eine Möglichkeit. Beim Klonen wird eine Kopie Ihrer App in einem neuen oder vorhandenen App Service-Plan in einer beliebigen Region erstellt.

Sie finden **App klonen** im Abschnitt **Entwicklungstools** des Menüs.

> [!IMPORTANT]
> Für das Klonen gelten einige Einschränkungen. Informationen dazu erhalten Sie unter [Klonen der Azure App Service-App](app-service-web-app-cloning.md).

## <a name="scale-an-app-service-plan"></a>Skalieren eines App Service-Plans

Informationen zum zentralen Hochskalieren des Tarifs eines App Service-Plans finden Sie unter [Zentrales Hochskalieren einer App in Azure](web-sites-scale.md).

Informationen zum horizontalen Hochskalieren einer App-Instanz finden Sie unter [Manuelles oder automatisches Skalieren der Instanzenzahl](../monitoring-and-diagnostics/insights-how-to-scale.md).

<a name="delete"></a>

## <a name="delete-an-app-service-plan"></a>Löschen eines App Service-Plans

Um unerwartete Kosten zu vermeiden, löscht App Service den Plan standardmäßig, wenn Sie die letzte App in einem App Service-Plan löschen. Wenn Sie den Plan beibehalten möchten, sollten Sie ihn in den **Free**-Tarif ändern, damit keine Kosten entstehen.

> [!IMPORTANT]
> Für App Service-Pläne, denen keine Apps zugeordnet sind, fallen trotzdem Gebühren an, da die konfigurierten VM-Instanzen weiterhin reserviert werden.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Zentrales Hochskalieren einer App in Azure](web-sites-scale.md)

[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
