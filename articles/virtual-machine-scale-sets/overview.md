---
title: Übersicht über Azure-VM-Skalierungsgruppen | Microsoft-Dokumentation
description: Enthält Informationen zu Azure-VM-Skalierungsgruppen und zur automatischen Skalierung Ihrer Anwendungen.
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.custom: mvc
ms.date: 03/27/2018
ms.author: negat
ms.openlocfilehash: 8ded9b20bd70d18b8a68df0c9775f3a56f8b185b
ms.sourcegitcommit: d74657d1926467210454f58970c45b2fd3ca088d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="what-are-virtual-machine-scale-sets"></a>Was sind Skalierungsgruppen für virtuelle Computer?
Mit Azure-VM-Skalierungsgruppen können Sie eine Gruppe von identischen virtuellen Computern mit Lastenausgleich erstellen und verwalten. Die Anzahl von VM-Instanzen kann automatisch erhöht oder verringert werden, wenn sich der Bedarf ändert, oder es kann ein Zeitplan festgelegt werden. Skalierungsgruppen ermöglichen Hochverfügbarkeit für Ihre Anwendungen und das zentrale Verwalten, Konfigurieren und Aktualisieren einer großen Zahl von VMs. Mit VM-Skalierungsgruppen können Sie umfassende Dienste für Bereiche wie Compute, Big Data und Containerworkloads erstellen.


## <a name="why-use-virtual-machine-scale-sets"></a>Gründe für die Verwendung von VM-Skalierungsgruppen
Zur Sicherstellung von Redundanz und einer höheren Leistung werden Anwendungen normalerweise auf mehrere Instanzen verteilt. Kunden können auf Ihre Anwendung über ein Lastenausgleichsmodul zugreifen, mit dem Anforderungen jeweils auf eine der Anwendungsinstanzen verteilt werden. Wenn Sie Wartungsarbeiten durchführen oder eine Anwendungsinstanz aktualisieren müssen, müssen Ihre Kunden auf eine andere verfügbare Anwendungsinstanz verteilt werden. Unter Umständen müssen Sie die Anzahl von Anwendungsinstanzen erhöhen, auf denen Ihre Anwendung ausgeführt wird, um eine steigende Kundennachfrage abzudecken.

Über Azure-VM-Skalierungsgruppen werden die Verwaltungsfunktionen für Anwendungen, die auf vielen VMs ausgeführt werden, die [automatische Skalierung von Ressourcen](virtual-machine-scale-sets-autoscale-overview.md) und der Lastenausgleich für Datenverkehr bereitgestellt. Skalierungsgruppen verfügen über die folgenden wichtigen Vorteile:

- **Einfaches Erstellen und Verwalten von mehreren VMs**
    - Wenn Sie über viele VMs verfügen, auf denen Ihre Anwendung ausgeführt wird, ist es wichtig, für Ihre gesamte Umgebung eine einheitliche Konfiguration zu nutzen. Eine zuverlässige Leistung der Anwendung wird erzielt, wenn die VM-Größe, Datenträgerkonfiguration und Anwendungsinstallationen für alle VMs gleich sind.
    - Bei Skalierungsgruppen werden alle VM-Instanzen aus demselben Betriebssystem-Basisimage und derselben Konfiguration erstellt. Mit diesem Ansatz können Sie leicht Hunderte von VMs verwalten, ohne dass zusätzliche Konfigurationsaufgaben oder Schritte für die Netzwerkverwaltung anfallen.
    - Skalierungsgruppen unterstützen die Verwendung von [Azure Load Balancer](../load-balancer/load-balancer-overview.md) für eine grundlegende Layer-4-Datenverkehrsverteilung und von [Azure Application Gateway](../application-gateway/application-gateway-introduction.md) für eine erweiterte Layer-7-Datenverkehrsverteilung und SSL-Beendigung.

- **Hochverfügbarkeit und Anwendungsresilienz**
    - Skalierungsgruppen werden verwendet, um mehrere Instanzen Ihrer Anwendung auszuführen. Wenn für eine dieser VM-Instanzen ein Problem besteht, können Kunden nach einer minimalen Unterbrechung über eine der anderen VM-Instanzen weiter auf Ihre Anwendung zugreifen.
    - Zur weiteren Steigerung der Verfügbarkeit können Sie [Verfügbarkeitszonen](../availability-zones/az-overview.md) einsetzen. Hierbei werden VM-Instanzen einer Skalierungsgruppe in einem Rechenzentrum oder über mehrere Rechenzentren hinweg automatisch verteilt.

- **Automatische Skalierung der Anwendung bei sich änderndem Ressourcenbedarf**
    - Die Kundennachfrage nach Ihrer Anwendung kann sich innerhalb eines Tages oder einer Woche ändern. Zur Erfüllung der Kundennachfrage können Skalierungsgruppen die Anzahl von VM-Instanzen automatisch erhöhen, wenn der Bedarf für die Anwendung zunimmt, und sie dann wieder verringern, wenn der Bedarf sinkt.
    - Die automatische Skalierung verringert auch die Anzahl von unnötigen VM-Instanzen, auf denen Ihre Anwendung ausgeführt wird, wenn die Nachfrage gering ist. Kunden erhalten weiterhin eine akzeptable Leistungsebene, wenn die Nachfrage zunimmt und automatisch weitere VM-Instanzen hinzugefügt werden. Diese Möglichkeit trägt zur Reduzierung von Kosten und zur effizienten bedarfsabhängigen Erstellung von Azure-Ressourcen bei.

- **Großer Umfang**
    - Skalierungsgruppen unterstützen bis zu 1.000 VM-Instanzen. Wenn Sie eigene benutzerdefinierte VM-Images erstellen und hochladen, beträgt der Grenzwert 300 VM-Instanzen.
    - Verwenden Sie [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) und [Storage Premium](../virtual-machines/windows/premium-storage.md), um für Produktionsworkloads die beste Leistung zu erzielen.


## <a name="differences-between-virtual-machines-and-scale-sets"></a>Unterschiede zwischen virtuellen Computern und Skalierungsgruppen
Skalierungsgruppen werden aus virtuellen Computern erstellt. Mit Skalierungsgruppen werden die Verwaltungs- und Automatisierungsebenen für die Ausführung und Skalierung Ihrer Anwendungen bereitgestellt. Stattdessen können Sie einzelne VMs manuell erstellen und verwalten oder vorhandene Tools integrieren, um eine ähnliche Automatisierungsebene zu schaffen. In der folgenden Tabelle sind die Vorteile von Skalierungsgruppen im Vergleich zur manuellen Verwaltung von mehreren VM-Instanzen angegeben.

| Szenario                           | Manuelles Gruppieren von VMs                                                                    | VM-Skalierungsgruppe |
|------------------------------------|----------------------------------------------------------------------------------------|---------------------------|
| Hinzufügung von weiteren VM-Instanzen        | Manueller Prozess zum Erstellen, Konfigurieren und Sicherstellen der Konformität                             | Automatisches Erstellen über die zentrale Konfiguration |
| Ausgleich und Verteilung von Datenverkehr | Manueller Prozess zum Erstellen und Konfigurieren einer Azure Load Balancer- oder Application Gateway-Instanz      | Automatische Erstellung und Integration in Azure Load Balancer oder Application Gateway |
| Hochverfügbarkeit und Redundanz   | Manuelle Erstellung einer Verfügbarkeitszone oder Verteilung und Nachverfolgung von VMs über Verfügbarkeitszonen hinweg | Automatische Verteilung von VM-Instanzen über Verfügbarkeitszonen und Verfügbarkeitsgruppen hinweg |
| Skalierung von VMs                     | Manuelle Überwachung und Azure Automation                                                 | Automatische Skalierung basierend auf Hostmetriken, Metriken auf Gastsystemen, Application Insights oder Zeitplan |

Für Skalierungsgruppen fallen keine zusätzlichen Kosten an. Sie zahlen nur für die zugrunde liegenden Computeressourcen, z.B. die VM-Instanzen, den Lastenausgleich oder Speicher für verwaltete Datenträger. Für die Verwaltungs- und Automatisierungsfeatures, z.B. automatische Skalierung und Redundanz, fallen bei der Nutzung von VMs keine weiteren Gebühren an.


## <a name="next-steps"></a>Nächste Schritte
Erstellen Sie im Azure-Portal Ihre erste VM-Skalierungsgruppe, um zu beginnen.

> [!div class="nextstepaction"]
> [Erstellen einer Skalierungsgruppe im Azure-Portal](quick-create-portal.md)
