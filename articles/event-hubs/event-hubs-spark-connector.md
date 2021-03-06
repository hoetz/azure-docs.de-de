---
title: Integrieren von Apache Spark in Azure Event Hubs | Microsoft-Dokumentation
description: Integrieren von Apache Spark für strukturiertes Streaming mit Event Hubs
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.service: event-hubs
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2018
ms.author: shvija;sethm;sagrewal
ms.openlocfilehash: b430b731bdb38f6fe8af347e082fdfb1ef36a945
ms.sourcegitcommit: d74657d1926467210454f58970c45b2fd3ca088d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="integrating-apache-spark-with-azure-event-hubs"></a>Integrieren von Apache Spark in Azure Event Hubs

Azure Event Hubs lässt sich nahtlos in [Apache Spark](https://spark.apache.org/) integrieren, um die Erstellung von Anwendungen für verteiltes Streaming zu vereinfachen. Diese Integration unterstützt [Spark Core](http://spark.apache.org/docs/latest/rdd-programming-guide.html), [Spark Streaming](http://spark.apache.org/docs/latest/streaming-programming-guide.html) und [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html). Der Event Hubs-Connector für Apache Spark ist auf [GitHub](https://github.com/Azure/azure-event-hubs-spark) verfügbar. Diese Bibliothek steht zudem für die Verwendung in Maven-Projekten über das [zentrale Maven-Repository](http://search.maven.org/#artifactdetails%7Ccom.microsoft.azure%7Cazure-eventhubs-spark_2.11%7C2.1.6%7C) bereit.

In diesem Artikel erfahren Sie, wie Sie eine fortlaufende Anwendung in [Azure Databricks](https://azure.microsoft.com/services/databricks/) erstellen. Wenngleich in diesem Artikel auf [Azure Databricks](https://azure.microsoft.com/services/databricks/) eingegangen wird, so stehen auch Spark-Cluster in [HDInsight](../hdinsight/spark/apache-spark-overview.md) zur Verfügung.

Im folgenden Beispiel werden zwei Scala-Notebooks verwendet: eins für das Streaming von Ereignissen aus einem Event Hub und eins für das Zurücksenden von Ereignissen.

## <a name="prerequisites"></a>Voraussetzungen

* Ein Azure-Abonnement. Wenn Sie noch keins haben, [erstellen Sie ein kostenloses Konto](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).
* Eine Event Hubs-Instanz. Wenn Sie noch keine haben, [erstellen Sie eine](event-hubs-create.md).
* Eine [Azure Databricks](https://azure.microsoft.com/services/databricks/)-Instanz. Wenn Sie noch keine haben, [erstellen Sie eine](../azure-databricks/quickstart-create-databricks-workspace-portal.md).
* [Erstellen Sie eine Bibliothek mithilfe der Maven-Koordinate](https://docs.databricks.com/user-guide/libraries.html#upload-a-maven-package-or-spark-package): `com.microsoft.azure:azure‐eventhubs‐spark_2.11:2.3.1`

Verwenden Sie den folgenden Code, um Ereignisse aus Ihrem Event Hub zu streamen:

```scala
import org.apache.spark.eventhubs._

// To connect to an event hub, EntityPath is required as part of the connection string.
// Here, we assume that the connection string from the Azure portal does not have the EntityPath part.
val connectionString = ConnectionStringBuilder("{EVENT HUB CONNECTION STRING FROM AZURE PORTAL}")
  .setEventHubName("{EVENT HUB NAME}")
  .build 
val ehConf = EventHubsConf(connectionString)
  .setStartingPosition(EventPosition.fromEndOfStream)

// Create a stream that reads data from the specified Event Hub.
val reader = spark.readStream
  .format("eventhubs")
  .options(ehConf.toMap)
  .load()
val eventhubs = reader.select($"body" cast "string")

eventhubs.writeStream
  .format("console")
  .outputMode("append")
  .start()
  .awaitTermination()
```
Der folgende Beispielcode sendet Ereignisse mit den Spark-Batch-APIs an Ihren Event Hub. Sie können auch eine Streamingabfrage schreiben, um Ereignisse an den Event Hub zu senden.

```scala
import org.apache.spark.eventhubs._
import org.apache.spark.sql.functions._

// To connect to an event hub, EntityPath is required as part of the connection string.
// Here, we assume that the connection string from the Azure portal does not have the EntityPath part.
val connectionString = ConnectionStringBuilder("{EVENT HUB CONNECTION STRING FROM AZURE PORTAL}")
  .setEventHubName("{EVENT HUB NAME}")
  .build
val ehConf = EventHubsConf(connectionString)

// Create random strings as the body of the message.
val bodyColumn = concat(lit("random nunmber: "), rand()).as("body")

// Write 200 rows to the specified event hub.
val df = spark.range(200).select(bodyColumn)
df.write
  .format("eventhubs")
  .options(eventHubsConf.toMap)
  .save() 
```

## <a name="next-steps"></a>Nächste Schritte

Sie haben gelernt, wie Sie mit dem Event Hubs-Connector für Apache Spark einen skalierbaren, fehlertoleranten Datenstrom einrichten. Weitere Informationen zur Verwendung von Event Hubs mit strukturiertem Streaming und Spark-Streaming finden Sie unter folgenden Links:

* [Structured Streaming + Azure Event Hubs Integration Guide](https://github.com/Azure/azure-event-hubs-spark/blob/master/docs/structured-streaming-eventhubs-integration.md) (Integrationsleitfaden zu strukturiertem Streaming und Azure Event Hubs)
* [Spark Streaming + Event Hubs Integration Guide](https://github.com/Azure/azure-event-hubs-spark/blob/master/docs/spark-streaming-eventhubs-integration.md) (Integrationsleitfaden zu Spark-Streaming und Event Hubs)
