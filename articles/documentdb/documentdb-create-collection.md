---
title: Erstellen einer DocumentDB-Datenbank und -Sammlung | Microsoft Docs
description: "Erfahren Sie, wie Sie NoSQL-Datenbanken und JSON-Dokumentsammlungen mit dem Onlinedienstportal für die cloudbasierte Dokumentendatenbank Azure DocumentDB erstellen. Holen Sie sich noch heute eine kostenlose Testversion."
services: documentdb
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b81ad2f6-df7f-4c6d-8ca9-f8a9982d647e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: mimig
translationtype: Human Translation
ms.sourcegitcommit: fba82c5c826da7d1912814b61c5065ca7f726011
ms.openlocfilehash: 8ee846e659d0a47a5fb39d6baa3235f59e19d653
ms.lasthandoff: 02/23/2017


---
# <a name="how-to-create-a-documentdb-collection-and-database-using-the-azure-portal"></a>So erstellen Sie eine DocumentDB-Sammlung und -Datenbank über das Azure-Portal
Um Microsoft Azure DocumentDB zu verwenden, müssen Sie über ein [DocumentDB-Konto](documentdb-create-account.md), eine Datenbank, eine Sammlung und Dokumente verfügen. In diesem Thema wird die Erstellung einer DocumentDB-Sammlung im Azure-Portal beschrieben.

Sie wissen nicht, was eine Sammlung ist? Dann lesen Sie den Abschnitt [Was ist eine DocumentDB-Sammlung?](#what-is-a-documentdb-collection)

1. Klicken Sie im [Azure-Portal](https://portal.azure.com/) auf der Navigationsleiste auf **DocumentDB (NoSQL)**, und wählen Sie anschließend auf dem Blatt **DocumentDB (NoSQL)** das Konto aus, dem Sie eine Sammlung hinzufügen möchten. Wenn keine Konten aufgeführt sind, müssen Sie [ein DocumentDB-Konto erstellen](documentdb-create-account.md).

   ![Screenshot mit „DocumentDB-Konten“ in der Navigationsleiste, mit dem Konto im Blatt „DocumentDB-Konten“ und mit der Datenbank im Blatt „DocumentDB-Konten“ im Fokus „Datenbanken“](./media/documentdb-create-collection/docdb-database-creation-1-2.png)

   Wenn **DocumentDB (NoSQL)** nicht in der Navigationsleiste angezeigt wird, klicken Sie auf **Weitere Dienste** und dann auf **DocumentDB (NoSQL)**. Wenn keine Konten aufgeführt sind, müssen Sie [ein DocumentDB-Konto erstellen](documentdb-create-account.md).
2. Klicken Sie auf dem Blatt **DocumentDB-Konto** für das ausgewählte Konto auf **Sammlung hinzufügen**.

    ![Screenshot mit „DocumentDB-Konten“ in der Navigationsleiste, mit dem Konto im Blatt „DocumentDB-Konten“ und mit der Datenbank im Blatt „DocumentDB-Konten“ im Fokus „Datenbanken“](./media/documentdb-create-collection/docdb-database-creation-3.png)
3. Geben Sie auf dem Blatt **Sammlung hinzufügen** im Feld **Sammlungs-ID** die ID für Ihre neue Sammlung ein. Der Namen einer Sammlung muss zwischen 1 und 255 Zeichen lang sein und darf weder `/ \ # ?` noch nachstehende Leerzeichen enthalten. Wenn der Name überprüft wurde, wird im ID-Feld ein grünes Häkchen angezeigt.

    ![Screenshot mit Schaltfläche „Sammlung hinzufügen“ auf dem Blatt „Datenbank“, mit den Einstellungen im Blatt „Sammlung hinzufügen“ und Schaltfläche „OK“ – Azure-Portal für DocumentDB – Cloudbasierte Datenbankerstellung für NoSQL-JSON-Datenbanken](./media/documentdb-create-collection/docdb-collection-creation-5-8.png)
4. Die Voreinstellung für **Speicherkapazität** ist **250 GB**, um partitionierte Sammlungen verarbeiten zu können.

    Legen Sie die Speicherkapazität auf **10 GB** fest, wenn Sie eine [einzelne Partitionssammlung](documentdb-partition-data.md#single-partition-and-partitioned-collections) mit einem Durchsatz von 400 bis 10.000 Anforderungseinheiten pro Sekunde (Request Unit, RU/s) verwenden möchten. Eine Anforderungseinheit (Request Unit, RU) entspricht dem Durchsatz des Lesevorgangs eines Dokuments mit 1 KB. Weitere Informationen zu Anforderungseinheiten finden Sie unter [Anforderungseinheiten](documentdb-request-units.md).

    Legen Sie die Speicherkapazität auf **250 GB** fest, wenn Sie eine [partitionierte Sammlung](documentdb-partition-data.md#single-partition-and-partitioned-collections) verwenden möchten, die skaliert werden kann, um eine unbegrenzte Menge an Speicher über mehrere Partitionen verteilt zu verarbeiten. Es werden Durchsatzebenen ab 2.500 Anforderungseinheiten pro Sekunde unterstützt.

    Legen Sie die Speicherkapazität auf **Benutzerdefiniert** fest, wenn Sie einen anderen Betrag als 10 GB oder 250 GB bereitstellen möchten. DocumentDB ist praktisch unbegrenzt skalierbar. Sie sollten daher die angeforderte Speichergröße und den Durchsatzwert in die Supportanfrage einschließen.

6. Geben Sie im Feld **Partitionsschlüssel** einen Partitionsschlüssel für die Sammlung ein. Dies ist für partitionierte Sammlungen erforderlich und für Sammlungen mit einer einzelnen Partition optional. Die Auswahl des richtigen Partitionsschlüssels ist wichtig für die Erstellung einer leistungsfähigen Sammlung. Weitere Informationen zum Auswählen eines Partitionsschlüssels finden Sie unter [Entwerfen für Partitionierung](documentdb-partition-data.md#designing-for-partitioning).
7. Erstellen Sie auf dem Blatt **Datenbank** entweder eine neue Datenbank, oder verwenden Sie eine vorhandene Datenbank. Datenbanknamen müssen zwischen 1 und 255 Zeichen lang sein und dürfen weder `/ \ # ?` noch nachgestellte Leerzeichen enthalten. Klicken Sie außerhalb des Textfelds, damit der Name überprüft wird. Nach der Überprüfung des Namens wird im Feld ein grünes Häkchen angezeigt.
8. Klicken Sie am unteren Bildschirmrand auf **OK**, um die neue Sammlung zu erstellen.
9. Die neue Sammlung wird jetzt im Fokus **Sammlungen** auf dem Blatt **Übersicht** angezeigt.

    ![Screenshot mit der neuen Sammlung in Blatt „Datenbank“ – Azure-Portal für DocumentDB – Cloudbasierte Datenbankerstellung für NoSQL-JSON-Datenbanken](./media/documentdb-create-collection/docdb-collection-creation-9.png)
10. **Optional:** Klicken Sie im Menü „Ressource“ auf **Skalieren**, um den Durchsatz für Sammlungen im Portal zu ändern.

    ![Screenshot des Menüs „Ressource“ mit Auswahl von „Skalieren“](./media/documentdb-create-collection/docdb-collection-creation-scale.png)

## <a name="what-is-a-documentdb-collection"></a>Was ist eine DocumentDB-Sammlung?
Eine Sammlung ist ein Container für JSON-Dokumente und die zugehörige JavaScript-Anwendungslogik. Eine Sammlung ist eine abrechnungsfähige Entität, bei der die [Kosten](documentdb-performance-levels.md) durch den bereitgestellten Durchsatz der Sammlung bestimmt werden. Sammlungen können eine/n oder mehrere Partitionen oder Server umfassen und können skaliert werden, um praktisch unbegrenzte Mengen an Speicher oder Durchsatz zu verarbeiten.

Sammlungen werden von DocumentDB automatisch in einen oder mehrere physische Server partitioniert. Wenn Sie eine Sammlung erstellen, können Sie den bereitgestellten Durchsatz in Form von Anforderungseinheiten pro Sekunde und einer Partitionsschlüsseleigenschaft angeben. Der Wert dieser Eigenschaft wird von DocumentDB zum Verteilen von Dokumenten zwischen Partitionen und zum Weiterleiten von Anforderungen wie Abfragen verwendet. Der Partitionsschlüssel fungiert außerdem als die Transaktionsgrenze für gespeicherte Prozeduren und Trigger. Jede Sammlung hat eine reservierte Durchsatzmenge, die für diese Sammlung spezifisch ist und die nicht mit anderen Sammlungen im gleichen Konto gemeinsam genutzt wird. Daher können Sie Ihre Anwendung sowohl im Hinblick auf Speicher als auch Durchsatz horizontal hochskalieren.

Sammlungen sind nicht identisch mit Tabellen in relationalen Datenbanken. Sammlungen erzwingen kein Schema. Als Datenbank erzwingt DocumentDB grundsätzlich keine Schemas, es handelt sich um eine schemafreie Datenbank. Daher können Sie unterschiedliche Arten von Dokumenten mit unterschiedlichen Schemas in derselben Sammlung speichern. Falls gewünscht, können Sie Sammlungen auch verwenden, um wie bei Tabellen Objekte eines einzelnen Typs zu speichern. Das geeignetste Modell ist nur davon abhängig, wie die Daten zusammen in Abfragen und Transaktionen angezeigt werden.

## <a name="other-ways-to-create-a-documentdb-collection"></a>Weitere Methoden zum Erstellen einer DocumentDB-Sammlung
Sammlungen müssen nicht über das Portal erstellt werden, sondern können auch mithilfe der [DocumentDB SDKs](documentdb-sdk-dotnet.md) und der REST-API erstellt werden.

* Ein C#-Codebeispiel finden Sie in den [C#-Sammlungsbeispielen](documentdb-dotnet-samples.md#collection-examples).
* Ein Node.js-Codebeispiel finden Sie in den [Node.js-Sammlungsbeispielen](documentdb-nodejs-samples.md#collection-examples).
* Ein Python-Codebeispiel finden Sie in den [Python-Sammlungsbeispielen](documentdb-python-samples.md#collection-examples).
* Ein REST-API-Beispiel finden Sie unter [Erstellen einer Sammlung](https://msdn.microsoft.com/library/azure/mt489078.aspx).

## <a name="troubleshooting"></a>Problembehandlung
Wenn **Sammlung hinzufügen** im Azure-Portal deaktiviert ist, bedeutet dies, dass Ihr Konto derzeit deaktiviert ist. Normalerweise passiert dies, wenn alle Leistungsguthaben für den Monat aufgebraucht sind.    

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie nun über eine Sammlung verfügen, besteht der nächste Schritt darin, Dokumente zur Sammlung hinzufügen oder in die Sammlung zu importieren. Zum Hinzufügen von Dokumenten zu einer Sammlung stehen Ihnen verschiedene Möglichkeiten zur Verfügung:

* Sie können [Dokumente hinzufügen](documentdb-view-json-document-explorer.md) , indem Sie den Dokument-Explorer im Portal verwenden.
* Sie können [Dokumente und Daten importieren](documentdb-import-data.md), indem Sie das Datenmigrationstool für DocumentDB verwenden, mit dem Sie JSON- und CSV-Dateien importieren können. Außerdem können Sie Daten aus SQL Server, MongoDB, dem Azure-Tabellenspeicher und anderen DocumentDB-Sammlungen importieren.
* Sie können Dokumente auch mithilfe eines der [DocumentDB-SDKs](documentdb-sdk-dotnet.md)hinzufügen. DocumentDB verfügt über SDKs für .NET, Java, Python, Node.js und JavaScript-API. C#-Codebeispiele, die die Verwendung von Dokumenten mithilfe des .NET SDK für DocumentDB veranschaulichen, finden Sie unter [C#-Dokumentbeispiele](documentdb-dotnet-samples.md#document-examples). Node.js-Codebeispiele, die die Verwendung von Dokumenten mithilfe des Node.js SDK für DocumentDB veranschaulichen, finden Sie unter [Node.js-Dokumentbeispiele](documentdb-nodejs-samples.md#document-examples).

Wenn eine Sammlung Dokumente enthält, können Sie in [DocumentDB SQL](documentdb-sql-query.md) an den Dokumenten [Abfragen ausführen](documentdb-sql-query.md#ExecutingSqlQueries), indem Sie den [Abfrage-Explorer](documentdb-query-collections-query-explorer.md) im Portal, die [REST-API](https://msdn.microsoft.com/library/azure/dn781481.aspx) oder eines der [SDKs](documentdb-sdk-dotnet.md) verwenden. 

