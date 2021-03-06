---
title: Konfigurieren von Datenquellen in Azure Log Analytics | Microsoft-Dokumentation
description: "Datenquellen definieren die Daten, die Log Analytics aus Agents und anderen verbundenen Quellen sammelt.  Dieser Artikel beschreibt das Konzept, nach dem Log Analytics Datenquellen verwendet, erläutert Details zur Konfiguration der Quellen und bietet eine Übersicht über die verschiedenen verfügbaren Datenquellen."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2017
ms.author: bwren
ms.openlocfilehash: 4237df0934d6191b77ff82c86a66585e72191ac9
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="data-sources-in-log-analytics"></a>Datenquellen in Log Analytics
Log Analytics sammelt Daten aus Ihren verbundenen Quellen und speichert diese in Ihrem Log Analytics-Arbeitsbereich.  Welche Daten gesammelt werden, wird durch die von Ihnen konfigurierten Datenquellen definiert.  Daten in Log Analytics werden als Datensatzgruppe gespeichert.  Jede Datenquelle erstellt Datensätze eines bestimmten Typs, von denen jeder über einen eigenen Satz von Eigenschaften verfügt.

![Log Analytics-Datensammlung](./media/log-analytics-data-sources/overview.png)

Datenquellen unterscheiden sich von [Verwaltungslösungen](log-analytics-add-solutions.md), die ebenfalls Daten aus verbundenen Quellen sammeln und Datensätze in Log Analytics erstellen.  Neben der Sammlung von Daten beinhalten Lösungen in der Regel Protokollsuchvorgänge und Ansichten, mit denen Sie den Betrieb einer bestimmten Anwendung oder eines Diensts analysieren können.


## <a name="summary-of-data-sources"></a>Übersicht über Datenquellen
In der folgenden Tabelle werden die zurzeit in Log Analytics verfügbaren Datenquellen aufgeführt.  In den Links zu den Datenquellen finden Sie weitere Informationen zur jeweiligen Datenquelle.

| Data source | Ereignistyp | BESCHREIBUNG |
|:--- |:--- |:--- |
| [Benutzerdefinierte Protokolle](log-analytics-data-sources-custom-logs.md) |\<ProtokollName\>_CL |Textdateien auf Windows- oder Linux-Agents mit Protokollinformationen |
| [Windows-Ereignisprotokolle](log-analytics-data-sources-windows-events.md) |Ereignis |Aus dem Ereignisprotokoll auf Windows-Computern erfasste Ereignisse |
| [Windows-Leistungsindikatoren](log-analytics-data-sources-performance-counters.md) |Perf |Auf Windows-Computern erfasste Leistungsindikatoren |
| [Linux-Leistungsindikatoren](log-analytics-data-sources-performance-counters.md) |Perf |Auf Linux-Computern erfasste Leistungsindikatoren |
| [IIS-Protokolle](log-analytics-data-sources-iis-logs.md) |W3CIISLog |IIS-Protokoll (Internetinformationsdienste) im W3C-Format |
| [Syslog](log-analytics-data-sources-syslog.md) |syslog |Syslog-Ereignisse auf Windows- oder Linux-Computern |

## <a name="configuring-data-sources"></a>Konfigurieren von Datenquellen
Sie konfigurieren Datenquellen in Log Analytics über das Menü **Daten** unter **Erweiterte Einstellungen**.  Jede Konfiguration wird an alle verbundenen Quellen in Ihrem Arbeitsbereich übermittelt.  Sie können zurzeit keine Agents aus dieser Konfiguration ausschließen.

![Windows-Ereignisse konfigurieren](./media/log-analytics-data-sources/configure-events.png)

1. Klicken Sie im Azure-Portal auf **Log Analytics**, auf Ihren Arbeitsbereich und anschließend auf **Erweiterte Einstellungen**.
2. Wählen Sie **Daten**aus.
3. Klicken Sie auf die Datenquelle, die Sie konfigurieren möchten.
4. Folgen Sie den Links in der oben stehenden Tabelle, um zur Dokumentation für jede Datenquelle zu gelangen und detaillierte Informationen zur jeweiligen Konfiguration zu erhalten.


## <a name="data-collection"></a>Datensammlung
Die Konfigurationen der Datenquellen werden innerhalb weniger Minuten an Agents übermittelt, die direkt mit Log Analytics verbunden sind.  Die angegebenen Daten werden vom Agent gesammelt und in den für jede Datenquelle spezifischen Intervallen direkt an Log Analytics übermittelt.  Informationen zu diesen Spezifikationen finden Sie in der Dokumentation zu jeder Datenquelle.

Bei System Center Operations Manager-Agents in einer verbundenen Verwaltungsgruppe werden Datenquellenkonfigurationen in Management Packs übersetzt und standardmäßig alle fünf Minuten an die Verwaltungsgruppe übermittelt.  Der Agent lädt das Management Pack wie jedes andere Paket herunter und sammelt die angegebenen Daten. Je nach Datenquelle werden die Daten entweder an einen Verwaltungsserver gesendet, der die Daten an Log Analytics weiterleitet, oder der Agent sendet die Daten ohne den Umweg über den Verwaltungsserver direkt an Log Analytics. Weitere Informationen finden Sie im Artikel zur [Datensammlung](log-analytics-add-solutions.md#data-collection-details).  Informationen zum Verbinden von Operations Manager und Log Analytics und zum Ändern der Häufigkeit, mit der die Konfiguration übermittelt wird, finden Sie unter [Herstellen einer Verbindung zwischen Operations Manager und Log Analytics](log-analytics-om-agents.md).

Falls der Agent keine Verbindung mit Log Analytics oder Operations Manager herstellen kann, sammelt er weiter Daten und übermittelt diese, sobald eine Verbindung hergestellt wird.  Daten können verloren, wenn die Datenmenge die maximale Cachegröße für den Client erreicht oder der Agent 24 Stunden lang keine Verbindung herstellen kann.

## <a name="log-analytics-records"></a>Log Analytics-Datensätze
Alle von Log Analytics gesammelten Daten werden im Arbeitsbereich als Datensätze gespeichert.  Datensätze, die aus verschiedenen Datenquellen gesammelt wurde, verfügen über einen eigenen Eigenschaftensatz und werden über die Eigenschaft **Typ** identifiziert.  Weitere Informationen zu den Datensatztypen finden Sie in der Dokumentation zur jeweiligen Datenquelle und Lösung.

## <a name="next-steps"></a>Nächste Schritte
* Erfahren Sie mehr über [Lösungen](log-analytics-add-solutions.md), die Log Analytics um zusätzliche Funktionen erweitern und ebenfalls Daten für den Arbeitsbereich sammeln.
* Erfahren Sie mehr über [Protokollsuchvorgänge](log-analytics-log-searches.md) zum Analysieren der aus Datenquellen und Lösungen gesammelten Daten.  
* Konfigurieren Sie [Warnungen](log-analytics-alerts.md), damit Sie bei kritischen Daten, die aus Datenquellen und Lösungen gesammelt werden, direkt benachrichtigt werden.
