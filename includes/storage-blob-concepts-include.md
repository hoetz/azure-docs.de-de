## <a name="what-is-blob-storage"></a>Was ist Blobspeicher?
Der Azure-Blobspeicher ist ein Dienst zur Speicherung großer Mengen unstrukturierter Objektdaten, beispielsweise Text- oder Binärdaten, auf die von überall auf der Welt über HTTP oder HTTPS zugegriffen werden kann. Sie können den Blobspeicher verwenden, um Daten öffentlich auf der ganzen Welt zur Verfügung zu stellen oder um Anwendungsdaten privat zu speichern.

BLOB-Speicherungen werden hauptsächlich für folgende Zwecke verwendet:

* Speichern von Bildern oder Dokumenten direkt für einen Browser
* Speichern von Dateien für verteilten Zugriff
* Video- und Audio-Streaming
* Speichern von Daten für Sicherung und Wiederherstellung, Notfallwiederherstellung und Archivierung
* Speichern von Daten für Analysen durch einen lokalen oder von Azure gehosteten Dienst

## <a name="blob-service-concepts"></a>Konzepte des Blob-Diensts
Der BLOB-Dienst umfasst die folgenden Komponenten:

![Diagramm der Blob-Dienst-Architektur](./media/storage-blob-concepts-include/blob1.png)

* **Speicherkonto:** Alle Zugriffe auf Azure Storage erfolgen über ein Speicherkonto. Bei diesem Speicherkonto kann es sich um ein **allgemeines Speicherkonto** oder ein **BLOB-Speicherkonto** handeln, das speziell für die Speicherung von Objekten oder Blobs verwendet wird. Weitere Informationen finden Sie unter [Informationen zu Azure-Speicherkonten](../articles/storage/common/storage-create-storage-account.md).
* **Container:** Ein Container dient zur Gruppierung eines Satzes von Blobs. Alle BLOBs müssen sich in Containern befinden. Ein Konto kann eine beliebige Anzahl von Containern enthalten. In einem Container kann eine beliebige Anzahl von BLOBs gespeichert sein. Beachten Sie, dass der Containername ausschließlich Kleinbuchstaben enthalten darf.
* **Blob:** Eine Datei von beliebiger Art und Größe. Azure Storage verfügt über drei Arten von Blobs: Blockblobs, Anfügeblobs und Seitenblobs.
  
    *Blockblobs* eignen sich ideal zum Speichern von Text- oder Binärdateien, z.B. Dokumente und Mediendateien. Ein einzelnes Blockblob kann bis zu 50.000 Blöcke mit jeweils bis zu 100 MB enthalten; dies ergibt eine Gesamtgröße von etwas mehr als 4,75 TB (100 MB X 50.000). 

    *Anfügeblobs* ähneln Blockblobs dahingehend, dass sie aus Blöcken bestehen. Allerdings sind sie für Anfügevorgänge optimiert, sodass sie für Protokollierungsszenarien nützlich sind. Ein einzelnes Anfügeblob kann bis zu 50.000 Blöcke mit jeweils bis zu 4 MB enthalten; dies ergibt eine Gesamtgröße von etwas mehr als 195 GB (4 MB X 50.000).
  
    *Seitenblobs* können bis zu 1 TB groß sein und sind besonders für häufige Lese-und Schreibvorgänge effizient. Virtuelle Azure-Computer verwenden Seitenblobs als Betriebssystem und Datenträger.
  
    Ausführliche Informationen zum Benennen von Containern und Blobs finden Sie unter [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata)(Benennen von Containern, Blobs und Metadaten und Verweisen auf diese).

