---
title: Verwenden von Hadoop Hive mit Curl in HDInsight – Azure | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Pig-Aufträge mithilfe von Curl remote an HDInsight übermitteln.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: conceptual
ms.date: 01/26/2018
ms.author: larryfr
ms.openlocfilehash: 8a7627e35a39dd4c9c94d273aa9f02c977dc88bf
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Ausführen von Hive-Abfragen mit Hadoop in HDInsight mit REST

[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

Erfahren Sie, wie Sie die WebHCat-REST-API verwenden, um Hive-Abfragen mit Hadoop in Azure HDInsight-Clustern auszuführen.

## <a name="prerequisites"></a>Voraussetzungen

* Ein Linux-basierter Hadoop-Cluster in HDInsight, Version 3.4 oder höher.

  > [!IMPORTANT]
  > Linux ist das einzige Betriebssystem, das unter HDInsight Version 3.4 oder höher verwendet wird. Weitere Informationen finden Sie unter [Welche Hadoop-Komponenten und -Versionen sind in HDInsight verfügbar?](../hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Ein REST-Client. In diesem Dokument werden Windows PowerShell und [Curl](http://curl.haxx.se/)-Beispiele verwendet.

    > [!NOTE]
    > Azure PowerShell stellt dedizierte Cmdlets zum Arbeiten mit Hive unter HDInsight bereit. Weitere Informationen finden Sie im Dokument [Verwenden von Hive mit Azure PowerShell](apache-hadoop-use-hive-powershell.md).

Dieses Dokument verwendet außerdem Windows PowerShell und [Jq](http://stedolan.github.io/jq/) zum Verarbeiten der JSON-Daten, die aus REST-Anforderungen zurückgegeben werden.

## <a id="curl"></a>Ausführen einer Hive-Abfrage

> [!NOTE]
> Wenn Sie cURL oder eine andere REST-Kommunikation mit WebHCat verwenden, müssen Sie die Anforderungen authentifizieren, indem Sie den Benutzernamen und das Kennwort des Administrators des HDInsight-Clusters bereitstellen.
>
> Die REST-API wird durch [Standardauthentifizierung](http://en.wikipedia.org/wiki/Basic_access_authentication)gesichert. Stellen Sie Anforderungen immer über HTTPS (Secure HTTP), um sicherzustellen, dass Ihre Anmeldeinformationen sicher an den Server gesendet werden.

1. Um die Clusteranmeldung festzulegen, die von den Skripts in diesem Dokument verwendet wird, verwenden Sie einen der folgenden Befehle:

    ```bash
    read -p "Enter your cluster login account name: " LOGIN
    ```

    ```powershell
    $creds = Get-Credential -UserName admin -Message "Enter the cluster login name and password"
    ```

2. Um den Namen des Clusters festzulegen, verwenden Sie einen der folgenden Befehle:

    ```bash
    read -p "Enter the HDInsight cluster name: " CLUSTERNAME
    ```

    ```powershell
    $clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
    ```

3. Verwenden Sie einen der folgenden Befehle, um zu überprüfen, ob Sie eine Verbindung mit Ihrem HDInsight-Cluster herstellen können:

    ```bash
    curl -u $LOGIN -G https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/status)
    ```
    
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/status" `
       -Credential $creds `
       -UseBasicParsing
    $resp.Content
    ```

    Sie empfangen eine Antwort, die in etwa dem folgenden Text entspricht:

    ```json
    {"status":"ok","version":"v1"}
    ```

    Folgende Parameter werden in diesem Befehl verwendet:

    * `-u`: Der Benutzername und das Kennwort für die Authentifizierung der Anforderung.
    * `-G`: Gibt an, dass diese Anforderung ein GET-Vorgang ist.

   Der Anfang der URL (`https://$CLUSTERNAME.azurehdinsight.net/templeton/v1`) ist für alle Anforderungen gleich. Der Pfad (`/status`) gibt an, dass die Anforderung einen Status von WebHCat (auch als Templeton bezeichnet) für den Server zurückgeben soll. Sie können mit dem folgenden Befehl auch die Version von Hive anfordern:

    ```bash
    curl -u $LOGIN -G https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/version/hive" `
       -Credential $creds `
       -UseBasicParsing
    $resp.Content
    ```

    Die Anforderung gibt in etwa folgenden Text zurück:

    ```json
        {"module":"hive","version":"0.13.0.2.1.6.0-2103"}
    ```

4. Verwenden Sie Folgendes, um eine Tabelle namens **log4jLogs**zu erstellen:

    ```bash
    JOBID=`curl -s -u $LOGIN -d user.name=$LOGIN -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/rest" https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/hive | jq .id`
    echo $JOBID
    ```

    ```powershell
    $reqParams = @{"user.name"="admin";"execute"="set hive.execution.engine=tez;DROP TABLE log4jLogs;CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED BY ' ' STORED AS TEXTFILE LOCATION '/example/data/;SELECT t4 AS sev,COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;";"statusdir"="/example/rest"}
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/hive" `
       -Credential $creds `
       -Body $reqParams `
       -Method POST `
       -UseBasicParsing
    $jobID = (ConvertFrom-Json $resp.Content).id
    $jobID
    ```

    Diese Anforderung verwendet die POST-Methode, die Daten als Teil der Anforderung an die REST-API sendet. Die folgenden Datenwerte werden mit der Anforderung gesendet:

     * `user.name`: Der Benutzer, der den Befehl ausführt.
     * `execute`: Die auszuführenden HiveQL-Anweisungen.
     * `statusdir`: Das Verzeichnis, in das der Status für diesen Auftrag geschrieben wird.

   Diese Anweisungen führen die folgenden Aktionen aus:
   
   * `DROP TABLE`: Wenn die Tabelle bereits vorhanden ist, wird sie gelöscht.
   * `CREATE EXTERNAL TABLE`: Erstellt eine neue „externe“ Tabelle in Hive. Externe Tabellen speichern nur die Tabellendefinition in Hive. Die Daten verbleiben an ihrem ursprünglichen Speicherort.

     > [!NOTE]
     > Externe Tabellen sollten Sie verwenden, wenn Sie erwarten, dass die zugrunde liegenden Daten aus einer externen Quelle aktualisiert werden. Das könnte z.B. ein automatisierter Datenupload oder ein anderer MapReduce-Vorgang sein.
     >
     > Durch das Löschen einer externen Tabelle werden **nicht** die Daten, sondern nur die Tabellendefinitionen gelöscht.

   * `ROW FORMAT`: Gibt an, wie die Daten formatiert werden. Die Felder werden in den einzelnen Protokollen durch Leerzeichen getrennt.
   * `STORED AS TEXTFILE LOCATION`: Der Speicherort der Daten (das Verzeichnis „example/data“) und die Information, dass sie als Text gespeichert werden.
   * `SELECT`: Wählt die Anzahl aller Zeilen aus, bei denen die Spalte **t4** den Wert **[ERROR]** enthält. Mit dieser Anweisung wird der Wert **3** zurückgegeben, da dieser Wert in drei Zeilen enthalten ist.

     > [!NOTE]
     > Beachten Sie, dass die Leerzeichen zwischen HiveQL-Anweisungen bei Curl durch das Zeichen `+` ersetzt werden. Werte in Anführungszeichen, die ein Leerzeichen enthalten, z. B. das Trennzeichen, dürfen nicht durch `+` ersetzt werden.

      Dieser Befehl gibt eine Auftrags-ID zurück, mit der der Status des Auftrags überprüft werden kann.

5. Verwenden Sie den folgenden Befehl, um den Status des Auftrags zu prüfen:

    ```bash
    curl -G -u $LOGIN -d user.name=$LOGIN https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/$JOBID | jq .status.state
    ```

    ```powershell
    $reqParams=@{"user.name"="admin"}
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/jobs/$jobID" `
       -Credential $creds `
       -Body $reqParams `
       -UseBasicParsing
    # ConvertFrom-JSON can't handle duplicate names with different case
    # So change one to prevent the error
    $fixDup=$resp.Content.Replace("jobID","job_ID")
    (ConvertFrom-Json $fixDup).status.state
    ```

    Wenn der Auftrag abgeschlossen ist, wird der Status **ERFOLGREICH** angezeigt.

6. Sobald der Status des Auftrags zu **ERFOLGREICH** wechselt, können Sie die Ergebnisse des Auftrags aus Azure Blob Storage abrufen. Der mit der Abfrage übergebene Parameter `statusdir` enthält den Speicherort der Ausgabedatei. In diesem Fall ist dies `/example/rest`. Diese Adresse speichert die Ausgabe im Verzeichnis `example/curl` im Standardspeicher des Clusters.

    Sie können diese Dateien mithilfe der [Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/cli/azure/install-azure-cli) auflisten und herunterladen. Weitere Informationen zur Verwendung der Azure-Befehlszeilenschnittstelle mit Azure Storage finden Sie im Artikel [Verwenden der Azure CLI 2.0 mit Azure Storage](https://docs.microsoft.com/azure/storage/storage-azure-cli#create-and-manage-blobs).

## <a id="nextsteps"></a>Nächste Schritte

Allgemeine Informationen zu Hive mit HDInsight:

* [Verwenden von Hive mit Hadoop in HDInsight](hdinsight-use-hive.md)

Informationen zu anderen Möglichkeiten, wie Sie mit Hadoop in HDInsight arbeiten können:

* [Verwenden von Pig mit Hadoop in HDInsight](hdinsight-use-pig.md)
* [Verwenden von MapReduce mit Hadoop in HDInsight](hdinsight-use-mapreduce.md)

Wenn Sie mit Tez mit Hive verwenden, finden Sie in den folgenden Dokumenten Informationen zum Debuggen:

* [Verwenden der Ambari-Tez-Ansicht in Linux-basiertem HDInsight](../hdinsight-debug-ambari-tez-view.md)

Weitere Informationen zu der in diesem Artikel verwendeten REST-API finden Sie in der [WebHCat-Referenz](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


