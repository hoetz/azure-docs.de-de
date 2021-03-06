---
title: Einführung in Azure Container Service für Kubernetes
description: Azure Container Service für Kubernetes vereinfacht die Bereitstellung und Verwaltung containerbasierter Anwendungen in Azure.
services: container-service
author: gabrtv
manager: timlt
ms.service: container-service
ms.topic: overview
ms.date: 11/13/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: 5bfa445eb11ed8be608278d0b95249372f9976ab
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="introduction-to-azure-container-service-aks-preview"></a>Einführung in die Vorschauversion von Azure Container Service (AKS)

Azure Container Service (AKS) vereinfacht das Erstellen, Konfigurieren und Verwalten eines Clusters mit virtuellen Computern, die für die Ausführung von Anwendungen in Containern vorkonfiguriert sind. So können Sie Ihre vorhandenen Kenntnisse nutzen, bzw. auf einen großen und wachsenden Pool von Communityfachkenntnissen zur Bereitstellung und Verwaltung von containerbasierten Anwendungen in Microsoft Azure zurückgreifen.

Mit AKS können Sie die professionellen Features von Azure nutzen und müssen dank Kubernetes und Docker-Imageformat trotzdem nicht auf Anwendungsportabilität verzichten.

> [!IMPORTANT]
> Azure Container Service (AKS) befindet sich derzeit in der **Vorschauphase**. Vorschauversionen werden Ihnen zur Verfügung gestellt, wenn Sie die [zusätzlichen Nutzungsbedingungen](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) akzeptieren. Einige Aspekte dieses Features werden bis zur allgemeinen Verfügbarkeit unter Umständen noch geändert.
>

## <a name="managed-kubernetes-in-azure"></a>Managed Kubernetes in Azure

AKS verringert die Komplexität und den operativen Mehraufwand des Verwaltens eines Kubernetes-Clusters, indem ein Großteil dieser Zuständigkeit an Azure übertragen wird. Azure führt als gehosteter Kubernetes-Dienst wichtige Aufgaben für Sie aus, z.B. Systemüberwachung und Wartung. Zudem zahlen Sie nur für die Agent-Knoten in den Clustern und nicht für die Master. AKS bietet als Managed Kubernetes-Dienst folgende Vorteile:

> [!div class="checklist"]
> * Automatisierte Kubernetes-Versionsupgrades und -Patches
> * Einfache Clusterskalierung
> * Selbstheilende gehostete Steuerungsebene (Master)
> * Kostenersparnis: Sie zahlen nur für die ausgeführten Agentpoolknoten

Da die Verwaltung der Knoten im AKS-Cluster durch Azure erfolgt, müssen Sie viele Aufgaben, z.B. Clusterupgrades, nicht mehr manuell ausführen. Weil diese wichtigen Wartungsaufgaben von Azure ausgeführt werden, bietet AKS keinen direkten Zugriff (z.B. mit SSH) auf den Cluster.

## <a name="using-azure-container-service-aks"></a>Verwenden von Azure Container Service (AKS)
Mit AKS wird das Ziel verfolgt, mit Open Source-Tools und -Technologien, die heutzutage bei den Kunden beliebt sind, eine Umgebung für das Containerhosting bereitzustellen. Zu diesem Zweck machen wir die standardmäßigen Kubernetes-API-Endpunkte verfügbar. Mithilfe dieser Standardendpunkte können Sie jede Software nutzen, die mit einem Kubernetes-Cluster kommunizieren kann. Zur Auswahl stehen beispielsweise [kubectl][kubectl-overview], [helm][helm] und [draft][draft].

## <a name="creating-a-kubernetes-cluster-using-azure-container-service-aks"></a>Erstellen eines Kubernetes-Clusters mithilfe von Azure Container Service (AKS)
Stellen Sie zum Verwenden von AKS zunächst mithilfe der [Azure CLI][aks-quickstart] oder über das Portal einen AKS-Cluster bereit. (Suchen Sie im Marketplace nach **Azure Container Service**.) Erfahrene Benutzer, die mehr Kontrolle über Azure Resource Manager-Vorlagen benötigen, können mithilfe des Open-Source-Projekts [acs-engine][acs-engine] einen eigenen benutzerdefinierten Kubernetes-Cluster erstellen und über die `az`-Befehlszeilenschnittstelle bereitstellen.

### <a name="using-kubernetes"></a>Verwenden von Kubernetes
Kubernetes automatisiert die Bereitstellung, Skalierung und Verwaltung von Anwendungen in Containern. Das Tool bietet zahlreiche Funktionen, darunter:
* Automatisches Bin Packing
* Selbstreparatur
* Horizontale Skalierung
* Dienstermittlung und Lastenausgleich
* Automatisierte Rollouts und Rollbacks
* Geheimnis- und Konfigurationsverwaltung
* Speicherorchestrierung
* Batchausführung

## <a name="videos"></a>Videos

Azure Container Service (AKS) – Azure Friday, Oktober 2017:

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Container-Orchestration-Simplified-with-Managed-Kubernetes-in-Azure-Container-Service-AKS/player]
>
>

Tools für die Entwicklung und Bereitstellung von Anwendungen in Kubernetes – Azure OpenDev, Juni 2017:

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

Erfahren Sie mehr über die Bereitstellung und Verwaltung von AKS mit der AKS-Schnellstartanleitung.

> [!div class="nextstepaction"]
> [AKS-Tutorial][aks-quickstart]

<!-- LINKS - external -->
[acs-engine]: https://github.com/Azure/acs-engine
[draft]: https://github.com/Azure/draft
[helm]: https://helm.sh/
[kubectl-overview]: https://kubernetes.io/docs/user-guide/kubectl-overview/

<!-- LINKS - internal -->
[aks-quickstart]: ./kubernetes-walkthrough.md

