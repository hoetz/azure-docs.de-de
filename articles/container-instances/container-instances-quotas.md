---
title: 'Azure Container Instances: Kontingente und Regionsverfügbarkeit'
description: Hier finden Sie Informationen zu den Standardkontingenten und zur Regionsverfügbarkeit des Azure Container Instances-Diensts.
services: container-instances
author: mmacy
manager: timlt
ms.service: container-instances
ms.topic: overview
ms.date: 02/27/2018
ms.author: marsma
ms.openlocfilehash: 2ed067542942cd314d61def5154c3c83cad6cc1c
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="quotas-and-region-availability-for-azure-container-instances"></a>Kontingente und Regionsverfügbarkeit für Azure Container Instances

Für die Ressourcen und Funktionen aller Azure-Dienste gelten bestimmte Standardlimits und Kontingente. Die folgenden Abschnitte enthalten Informationen zu den Standardressourcenlimits für mehrere ACI-Ressourcen (Azure Container Instances) sowie zur Verfügbarkeit des ACI-Diensts in Azure-Regionen.

## <a name="service-quotas-and-limits"></a>Dienstkontingente und Limits

[!INCLUDE [container-instances-limits](../../includes/container-instances-limits.md)]

## <a name="region-availability"></a>Regionale Verfügbarkeit

Azure Container Instances ist mit den angegebenen CPU- und Arbeitsspeicherlimits in den folgenden Regionen verfügbar:

| Speicherort | Betriebssystem | CPU | Arbeitsspeicher (GB) |
| -------- | -- | :---: | :-----------: |
| „USA, Westen“, „USA, Osten“, „Europa, Westen“, „Europa, Norden“ | Linux | 4 | 14 |
| USA, Westen 2; Asien, Südosten | Linux | 2 | 7 |
| „USA, Westen“, „USA, Osten“, „Europa, Westen“, „Europa, Norden“ | Windows | 4 | 14 |
| USA, Westen 2; Asien, Südosten | Windows | 2 | 3,5 |

Containerinstanzen, die innerhalb dieser Ressourcenlimits erstellt werden, unterliegen der Verfügbarkeit in der Bereitstellungsregion. Wenn eine Region stark ausgelastet ist, kann bei der Bereitstellung von Instanzen ein Fehler auftreten. Um einen solchen Fehler bei der Bereitstellung zu beheben, versuchen Sie, Instanzen mit niedrigeren CPU- und Arbeitsspeichereinstellungen bereitzustellen, oder führen Sie die Bereitstellung zu einem späteren Zeitpunkt durch.

Teilen Sie dem Team auf [aka.ms/aci/feedback](https://aka.ms/aci/feedback) mit, wenn zusätzliche Regionen und eine Erhöhung der CPU-/Arbeitsspeichergrenzwerte erforderlich sind.

Weitere Informationen zur Problembehandlung bei der Bereitstellung von Containerinstanzen finden Sie unter [Beheben von Bereitstellungsproblemen für Azure Container Instances](container-instances-troubleshooting.md).

## <a name="next-steps"></a>Nächste Schritte

Bestimmte Standardlimits und Kontingente können erhöht werden. Wenn Sie eine Erhöhung von Ressourcen anfordern möchten, für die dies unterstützt wird, müssen Sie eine [Azure-Supportanfrage][azure-support] übermitteln und dabei als **Problemtyp** die Option „Kontingent“ auswählen.

<!-- LINKS - External -->
[azure-support]: https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest
