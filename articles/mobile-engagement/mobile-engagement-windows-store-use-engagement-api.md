---
title: Verwenden der Engagement-API auf der universellen Windows-Plattform
description: Verwenden der Engagement-API auf der universellen Windows-Plattform
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f8f211764646bc53319f435d74a16a026329039
ms.sourcegitcommit: 34e0b4a7427f9d2a74164a18c3063c8be967b194
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a>Verwenden der Engagement-API auf der universellen Windows-Plattform
> [!IMPORTANT]
> Azure Mobile Engagement wird am 31.3.2018 außer Kraft gesetzt. Diese Seite wird kurz danach gelöscht.
> 

Dieses Dokument ist ein Zusatz zu dem Dokument [Integration von Engagement in die universelle Windows-Plattform](mobile-engagement-windows-store-integrate-engagement.md): Es bietet tiefergehende Details zur Verwendung der Engagement-API zur Ausgabe von Anwendungsstatistiken.

Beachten Sie: Wenn Engagement nur die Sitzungsaktivitäten der Anwendung, Abstürze und technische Informationen melden soll, ist es am einfachsten, wenn alle `Page`-Unterklassen von der `EngagementPage`-Klasse erben.

Wenn Sie darüber hinaus noch mehr Meldungen wünschen, z. B. wenn Sie anwendungsspezifische Ereignisse, Fehler und Aufträge melden möchten, oder wenn die Aktivitäten Ihrer Anwendung anders als in den `EngagementPage`-Klassen implementiert gemeldet werden sollen, dann müssen Sie die Engagement-API verwenden.

Die Engagement-API wird von der `EngagementAgent` -Klasse zur Verfügung gestellt. Sie können über `EngagementAgent.Instance`auf diese Methoden zugreifen.

Auch wenn das Agent-Modul nicht initialisiert wurde, wird jeder Aufruf zur API verzögert und erneut ausgeführt, sobald der Agent verfügbar ist.

## <a name="engagement-concepts"></a>Engagement-Konzepte
In den folgenden Abschnitten werden die [Mobile Engagement-Konzepte](mobile-engagement-concepts.md) für die universelle Windows-Plattform genauer dargestellt.

### <a name="session-and-activity"></a>`Session` und `Activity`
Eine *Aktivität* ist normalerweise einer Seite der Anwendung zugeordnet, d.h. die *Aktivität* beginnt, wenn die Seite angezeigt wird, und wird beendet, wenn die Seite geschlossen wird: Dies ist der Fall, wenn das Engagement-SDK unter Verwendung der `EngagementPage`-Klasse integriert wurde.

*Aktivitäten* können aber auch manuell mithilfe der Engagement-API gesteuert werden. Auf diese Weise können Sie eine bestimmte Seite in mehrere Teile unterteilen, um weitere Informationen zur Verwendung dieser Seite zu erhalten und etwa zu erfahren, wie oft und wie lange Dialogfelder im Rahmen dieser Seite verwendet werden.

## <a name="reporting-activities"></a>Berichterstellung für Aktivitäten
### <a name="user-starts-a-new-activity"></a>Benutzer startet eine neue Aktivität
#### <a name="reference"></a>Verweis
            void StartActivity(string name, Dictionary<object, object> extras = null)

Sie müssen jedes Mal `StartActivity()` aufrufen, wenn sich die Benutzeraktivität ändert. Der erste Aufruf dieser Funktion startet eine neue Benutzersitzung.

> [!IMPORTANT]
> Das SDK ruft automatisch die EndActivity-Methode auf, wenn die Anwendung geschlossen wird. Daher wird DRINGEND empfohlen, die StartActivity-Methode aufzurufen, sobald sich die Aktivität des Benutzers ändert, und die EndActivity-Methode NIE aufzurufen, weil dadurch ein Beenden der aktuellen Sitzung erzwungen wird.
> 
> 

#### <a name="example"></a>Beispiel
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>Der Benutzer beendet seine aktuelle Aktivität
#### <a name="reference"></a>Verweis
            void EndActivity()

Damit werden die Aktivität und die Sitzung beendet. Sie sollten diese Methode nur dann aufrufen, wenn Sie sich wirklich sicher sind.

#### <a name="example"></a>Beispiel
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Berichterstellung für Aufträge
### <a name="start-a-job"></a>Starten eines Auftrags
#### <a name="reference"></a>Verweis
            void StartJob(string name, Dictionary<object, object> extras = null)

Sie können den Auftrag verwenden, um bestimmte Aufgaben eine Zeit lang nachzuverfolgen.

#### <a name="example"></a>Beispiel
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Beenden eines Auftrags
#### <a name="reference"></a>Verweis
            void EndJob(string name)

Sobald eine Aufgabe, die von einem Auftrag nachverfolgt wird, beendet ist, sollten Sie die EndJob-Methode für diesen Auftrag aufrufen, indem Sie den Auftragsnamen angeben.

#### <a name="example"></a>Beispiel
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Berichterstellung für Ereignisse
Es gibt drei Arten von Ereignissen:

* Eigenständige Ereignisse
* Sitzungsereignisse
* Auftragsereignisse

### <a name="standalone-events"></a>Eigenständige Ereignisse
#### <a name="reference"></a>Verweis
            void SendEvent(string name, Dictionary<object, object> extras = null)

Eigenständige Ereignisse können außerhalb des Kontexts einer Sitzung auftreten.

#### <a name="example"></a>Beispiel
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Sitzungsereignisse
#### <a name="reference"></a>Verweis
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Sitzungsereignisse werden normalerweise verwendet, um die Aktionen eines Benutzers während seiner Sitzung zu melden.

#### <a name="example"></a>Beispiel
**Ohne Daten:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Mit Daten:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Auftragsereignisse
#### <a name="reference"></a>Verweis
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Auftragsereignisse werden normalerweise verwendet, um die Aktionen eines Benutzers während eines Auftrags zu melden.

#### <a name="example"></a>Beispiel
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Melden von Fehlern
Es gibt drei Fehlertypen:

* Eigenständige Fehler
* Sitzungsfehler
* Auftragsfehler

### <a name="standalone-errors"></a>Eigenständige Fehler
#### <a name="reference"></a>Verweis
            void SendError(string name, Dictionary<object, object> extras = null)

Im Gegensatz zu Sitzungsfehlern können eigenständige Fehler außerhalb des Kontexts einer Sitzung auftreten.

#### <a name="example"></a>Beispiel
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Sitzungsfehler
#### <a name="reference"></a>Verweis
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Sitzungsfehler werden normalerweise zum Melden der Fehler verwendet, die Auswirkungen auf den Benutzer während seiner Sitzung haben.

#### <a name="example"></a>Beispiel
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Auftragsfehler
#### <a name="reference"></a>Verweis
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Fehler können mit einem ausgeführten Auftrag in Zusammenhang stehen anstatt mit der aktuellen Benutzersitzung.

#### <a name="example"></a>Beispiel
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Berichterstellung von Abstürzen
Der Agent stellt zwei Methoden für den Umgang mit Abstürzen zur Verfügung.

### <a name="send-an-exception"></a>Senden einer Ausnahme
#### <a name="reference"></a>Verweis
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Beispiel
Sie können eine Ausnahme jederzeit durch folgenden Aufruf senden:

            EngagementAgent.Instance.SendCrash(aCatchedException);

Sie können auch einen optionalen Parameter zum Beenden der Engagement-Sitzung zur gleichen Zeit wie bei der Übermittlung des Absturzes verwenden. Hierzu rufen Sie Folgendes auf:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Wenn Sie dies tun, werden die Sitzung und die Aufträge direkt nach dem Senden des Absturzes geschlossen.

### <a name="send-an-unhandled-exception"></a>Senden Sie eine nicht behandelte Ausnahme
#### <a name="reference"></a>Verweis
            void SendCrash(Exception e)

Engagement bietet auch eine Methode, um unbehandelte Ausnahmen zu senden, wenn der automatische **Absturz**-Bericht von Engagement **DEAKTIVIERT** ist. Dies ist besonders bei Verwendung in der Anwendung UnhandledException-Ereignishandler nützlich.

Durch diese Methode werden **IMMER** die Engagement-Sitzungen und -Aufträge nach dem Aufrufen beendet.

#### <a name="example"></a>Beispiel
Sie können sie verwenden, um Ihren eigenen UnhandledExceptionEventArgs-Handler zu implementieren. Fügen Sie z. B. die `Current_UnhandledException`-Methode der `App.xaml.cs`-Datei hinzu:

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

Fügen Sie in "App.xaml.cs" in "Public App(){}" Folgendes hinzu:

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a>Geräte-ID
            String EngagementAgent.Instance.GetDeviceId()

Sie können die Engagement-Geräte-ID durch Aufrufen dieser Methode abrufen.

## <a name="extras-parameters"></a>Extras-Parameter
Einem Ereignis, einem Fehler, einer Aktivität oder einem Auftrag können beliebige Daten zugeordnet werden. Diese Daten können unter Verwendung eines Wörterbuchs strukturiert werden. Schlüssel und Werte können einen beliebigen Typ aufweisen.

Extras-Daten werden serialisiert; wenn Sie also einen eigenen Typ in Extras einfügen möchten, müssen Sie einen Datenvertrag für diesen Typ hinzufügen.

### <a name="example"></a>Beispiel
Erstellen Sie die neue Klasse "Person".

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Fügen Sie anschließend eine `Person` -Instanz zu einem Extra hinzu.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Wenn Sie andere Objekttypen einfügen, stellen Sie sicher, dass deren ToString()-Methode implementiert wird, sodass eine visuell lesbare Zeichenfolge zurückgegeben wird.
> 
> 

### <a name="limits"></a>Einschränkungen
#### <a name="keys"></a>Schlüssel
Jeder Schlüssel in dem Objekt muss mit dem folgenden regulären Ausdruck übereinstimmen:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Das bedeutet, dass Schlüssel mit mindestens einem Buchstaben beginnen müssen, gefolgt von Buchstaben, Ziffern oder Unterstrichen (\_).

#### <a name="size"></a>Größe
Extras sind beschränkt auf **1024** Zeichen pro Aufruf.

## <a name="reporting-application-information"></a>Informationen zur Berichterstellung für Anwendungen
### <a name="reference"></a>Verweis
            void SendAppInfo(Dictionary<object, object> appInfos)

Sie können Nachverfolgungsinformationen (oder beliebige andere anwendungsspezifische Informationen) manuell mithilfe der SendAppInfo()-Funktion melden.

Beachten Sie, dass diese Daten inkrementell gesendet werden können: Nur der letzte Wert für einen bestimmten Schlüssel wird für ein bestimmtes Gerät gespeichert. Verwenden Sie wie bei Ereignisextras ein Dictionary\<Objekt, Objekt\>-Element, um Daten anzufügen.

### <a name="example"></a>Beispiel
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Einschränkungen
#### <a name="keys"></a>Schlüssel
Jeder Schlüssel in dem Objekt muss mit dem folgenden regulären Ausdruck übereinstimmen:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Das bedeutet, dass Schlüssel mit mindestens einem Buchstaben beginnen müssen, gefolgt von Buchstaben, Ziffern oder Unterstrichen (\_).

#### <a name="size"></a>Größe
Anwendungsinformationen sind auf **1024** Zeichen pro Aufruf beschränkt.

Im vorherigen Beispiel enthält die an den Server gesendete JSON 44 Zeichen:

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a>Protokollierung
### <a name="enable-logging"></a>Aktivieren der Protokollierung
Das SDK kann zum Erzeugen von Testprotokollen in der IDE-Konsole konfiguriert werden.
Diese Protokolle sind nicht standardmäßig aktiviert. Um diese anzupassen, aktualisieren Sie die Eigenschaft `EngagementAgent.Instance.TestLogEnabled` auf einen der aus der `EngagementTestLogLevel`-Enumeration verfügbaren Werte, beispielsweise:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

