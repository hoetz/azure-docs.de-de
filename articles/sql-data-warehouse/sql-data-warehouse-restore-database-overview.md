---
title: Wiederherstellen einer Azure Data Warehouse-Instanz – lokal und georedundant | Microsoft-Dokumentation
description: Übersicht über die Wiederherstellungsoptionen zur Wiederherstellung einer Datenbank in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jenniehubbard
editor: ''
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 12/06/2017
ms.author: barbkess
ms.openlocfilehash: abf8f0b1005aec71812dc8ebfd12fe65250d7a0e
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="sql-data-warehouse-restore"></a>SQL Data Warehouse-Wiederherstellung
> [!div class="op_single_selector"]
> * [Übersicht][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

SQL Data Warehouse bietet sowohl lokale als auch geografische Wiederherstellungen im Rahmen der Data Warehouse-Funktionalität für Notfallwiederherstellungen. Verwenden Sie Data Warehouse-Sicherungen, um Ihr Data Warehouse auf einen Wiederherstellungspunkt in der primären Region wiederherzustellen, oder verwenden Sie georedundante Sicherungen für eine Wiederherstellung in einer anderen geografischen Region. Dieser Artikel erläutert die Details der Wiederherstellung eines Data Warehouse.

## <a name="what-is-a-data-warehouse-restore"></a>Was ist eine Data Warehouse-Wiederherstellung?
Eine Data Warehouse-Wiederherstellung ist ein neues Data Warehouse, das aus einer Sicherung eines vorhandenen oder gelöschten Data Warehouse erstellt wird. Das wiederhergestellte Data Warehouse erstellt das gesicherte Data Warehouse zu einem bestimmten Zeitpunkt neu. Da SQL Data Warehouse ein verteiltes System ist, wird eine Data Warehouse-Wiederherstellung aus vielen Sicherungsdateien erstellt, die in Azure-Blobs gespeichert sind. 

Datenbankwiederherstellungen sind ein wesentlicher Bestandteil jeder Strategie für Geschäftskontinuität und Notfallwiederherstellung, da Ihre Daten nach versehentlichen Beschädigungen oder Löschungen neu erstellt werden.

Weitere Informationen finden Sie unter 

* [SQL Data Warehouse-Sicherungen](sql-data-warehouse-backups.md)
* [Übersicht über die Geschäftskontinuität](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Data Warehouse-Wiederherstellungspunkte
Azure Storage Premium bietet den Vorteil, dass SQL Data Warehouse Azure Storage Blob-Momentaufnahmen verwenden kann, um das primäre Data Warehouse zu sichern. Jede Momentaufnahme ist ein Wiederherstellungspunkt, der den Zeitpunkt zu Beginn der Momentaufnahme darstellt. Um ein Data Warehouse wiederherzustellen, wählen Sie einen Wiederherstellungspunkt aus und geben einen Wiederherstellungsbefehl aus.  

SQL Data Warehouse stellt die Sicherung stets in einem neuen Data Warehouse wieder her. Sie können entweder das wiederhergestellte Data Warehouse und das aktuelle beibehalten oder eines davon löschen. Wenn Sie das aktuelle Data Warehouse durch das wiederhergestellte Data Warehouse ersetzen möchten, können Sie es umbenennen.

Wenn Sie ein gelöschtes oder angehaltenes Data Warehouse wiederherstellen müssen, können Sie [ein Supportticket erstellen](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a>Georedundante Wiederherstellung
Sie können Ihr Data Warehouse in einer beliebigen Region wiederherstellen, die Azure SQL Data Warehouse auf der gewählten Leistungsebene unterstützt. Beachten Sie, dass 9000 und 18000 DWU in der Vorschauversion nicht in allen Regionen unterstützt werden.

> [!NOTE]
> Zum Ausführen einer georedundanten Wiederherstellung müssen Sie dieses Feature nicht deaktiviert haben.
> 
> 

## <a name="restore-timeline"></a>Zeitachse der Wiederherstellung
Sie können eine Datenbank auf jeden verfügbaren Wiederherstellungspunkt innerhalb der letzten sieben Tage wiederherstellen. Momentaufnahmen werden alle vier bis acht Stunden gestartet und sind sieben Tage lang verfügbar. Wenn eine Momentaufnahme älter als sieben Tage ist, läuft sie ab, und ihr Wiederherstellungspunkt ist nicht mehr verfügbar.

## <a name="restore-costs"></a>Kosten für die Wiederherstellung
Die Speichergebühren für das wiederhergestellte Data Warehouse werden zum Azure Storage Premium-Tarif abgerechnet. 

Wenn Sie ein wiederhergestelltes Data Warehouse anhalten, wird Ihnen der Speicher zum Azure Storage Premium-Tarif in Rechnung gestellt. Der Vorteil des Anhaltens besteht darin, dass Ihnen die DWU-Computerressourcen nicht berechnet werden.

Weitere Informationen zu den Preisen für SQL Data Warehouse finden Sie in der [Preisübersicht für SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Einsatzbereiche der Wiederherstellung
Der vorrangige Einsatzbereich für die Data Warehouse-Wiederherstellung ist das Wiederherstellen von Daten nach versehentlichen Datenverlusten oder -beschädigungen.

Mit der Data Warehouse-Wiederherstellung können Sie auch eine Sicherung für mehr als sieben Tage beibehalten. Nachdem die Sicherung wiederhergestellt wurde, ist das Data Warehouse online, und Sie können es unbegrenzt anhalten, um Computekosten zu sparen. Für die angehaltene Datenbank fallen Speichergebühren nach dem Azure Storage Premium-Tarif an. 

## <a name="related-topics"></a>Verwandte Themen
### <a name="scenarios"></a>Szenarien
* Eine Übersicht zum Thema Geschäftskontinuität finden Sie unter [Übersicht über die Geschäftskontinuität](../sql-database/sql-database-business-continuity.md).

<!-- ### Tasks -->

Um eine Data Warehouse-Wiederherstellung auszuführen, verwenden Sie Folgendes:

* Azure-Portal, siehe [Wiederherstellen eines Data Warehouse mit dem Azure-Portal](sql-data-warehouse-restore-database-portal.md)
* PowerShell-Cmdlets, siehe [Wiederherstellen eines Data Warehouse mit PowerShell-Cmdlets](sql-data-warehouse-restore-database-powershell.md)
* REST-APIs, siehe [Wiederherstellen eines Data Warehouse mit REST-APIs](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
