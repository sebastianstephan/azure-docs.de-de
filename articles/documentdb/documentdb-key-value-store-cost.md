---
title: "Azure DocumentDB als Schlüsselwertspeicher – Kostenübersicht | Microsoft-Dokumentation"
description: "Hier erhalten Sie Informationen über die niedrigen Kosten des Einsatzes von Azure DocumentDB als Schlüsselwertspeicher."
keywords: "Schlüsselwertspeicher"
services: documentdb
author: ArnoMicrosoft
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: acomet
translationtype: Human Translation
ms.sourcegitcommit: b4802009a8512cb4dcb49602545c7a31969e0a25
ms.openlocfilehash: 4d6ea897ec24ab9cbf5c131cd4629f45447f1460
ms.lasthandoff: 03/29/2017

---

# <a name="documentdb-as-a-key-value-store--cost-overview"></a>DocumentDB als Schlüsselwertspeicher – Kostenübersicht

Azure DocumentDB ist ein vollständig verwalteter, global verteilter NoSQL-Datenbankdienst für die mühelose Erstellung hoch verfügbarer, umfangreicher [global verteilter](documentdb-distribute-data-globally.md) Anwendungen. Standardmäßig indiziert der Dienst DocumentDB automatisch effizient alle Daten, die er erfasst. Dies ermöglicht schnelle und konsistente [SQL](documentdb-sql-query.md)-Abfragen (und [JavaScript](documentdb-programming.md)-Abfragen) für jede Art von Daten. 

In diesem Artikel werden die Kosten von DocumentDB für einfache Schreib- und Lesevorgänge bei Verwendung als Schlüssel-/Wertspeicher beschrieben. Zu den Schreibvorgängen zählen Einfügungen, Ersetzungen, Löschungen und Upserts von Dokumenten. Neben der garantierten hohen Verfügbarkeit von 99,99% bietet DocumentDB garantiert <10ms Latenz für Lesevorgänge bzw. <15ms Latenz für die (indizierten) Schreibvorgänge im 99. Perzentil. 

## <a name="why-we-use-request-units-rus"></a>Gründe für die Verwendung von Anforderungseinheiten (Request Units, RUs)

Die DocumentDB-Leistung basiert auf der Menge der für die Partition bereitgestellten [Anforderungseinheiten](documentdb-request-units.md) (RU). Die Bereitstellung erfolgt mit einer zweiten Granularität und wird in RUs pro Sekunde erworben ([nicht zu verwechseln mit der stündlichen Abrechnung](https://azure.microsoft.com/pricing/details/documentdb/)). Betrachten Sie RUs als eine Währung, die die Bereitstellung des für die Anwendung erforderlichen Durchsatzes vereinfacht. Unsere Kunden müssen nicht zwischen Lese- und Schreibkapazitätseinheiten differenzieren. Das einzelne Währungsmodell der RUs sorgt für die nötige Effizienz, um die bereitgestellte Kapazität zwischen Lese- und Schreibvorgängen aufzuteilen. Dieses bereitgestellte Kapazitätsmodell ermöglicht dem Dienst, einen vorhersagbaren und konsistenten Durchsatz, garantiert niedrige Latenz und hohe Verfügbarkeit zu bieten. Schließlich verwenden wir RUs für Durchsatzmodelle, doch jede bereitgestellte RU verfügt auch über eine definierte Menge von Ressourcen (Arbeitsspeicher, Kern). RU/Sekunde ist nicht nur ein IOPS-Wert.

Als global verteiltes Datenbanksystem ist DocumentDB der einzige Azure-Dienst, der außer zur hohen Verfügbarkeit eine SLA zu Latenz, Durchsatz und Konsistenz bietet. Der Durchsatz, den Sie bereitstellen, wird auf jede der Regionen angewendet, die Ihrem DocumentDB-Datenbankkonto zugeordnet ist. Für Lesevorgänge bietet DocumentDB mehrere klar definierte [Konsistenzebenen](documentdb-consistency-levels.md), zwischen denen Sie wählen können. 

Die folgende Tabelle zeigt, wie viel RUs erforderlich sind, um Lese- und Schreibtransaktionen durchzuführen, basierend auf Dokumentgrößen von 1 bzw. 100 KB.

|Dokumentgröße|1 Lesevorgang|1 Schreibvorgang|
|-------------|------|-------|
|1 KB|1 RU|5 RUs|
|100 KB|10 RUs|50 RUs|

## <a name="cost-of-reads-and-writes"></a>Kosten für Lese- und Schreibvorgänge

Wenn Sie 1.000 RUs/Sekunde bereitstellen, ergibt dies 3,6 Mio. RUs/Stunde und kostet 0,08 US-Dollar pro Stunde (in den USA und Europa). Für ein Dokument von 1KB Größe können Sie demnach mit dem von Ihnen bereitgestellten Durchsatz 3,6 Mio. Lesevorgänge oder 0,72 Mio. Schreibvorgänge (3,6 Mio. RU / 5) durchführen. Normalisiert auf eine Million Lese- und Schreibvorgänge würden die Kosten für Lesevorgänge 0,022 US-Dollar/Million (0,08 US-Dollar / 3,6) und für Schreibvorgänge 0,111 US-Dollar/Million (0,08 US-Dollar / 0,72) betragen. Wie in der folgenden Tabelle gezeigt, werden die Kosten pro Million minimal.

|Dokumentgröße|1 Mio. Lesevorgänge|1 Mio. Schreibvorgänge|
|-------------|-------|--------|
|1 KB|$0.022|$0.111|
|100 KB|$0.222|$1.111|

Die meisten grundlegenden Blob- oder Objektspeicherdienste berechnen Gebühren von 0,40 US-Dollar pro Million Lesetransaktionen und 5 US-Dollar pro Million Schreibtransaktionen. Bei optimaler Nutzung kann DocumentDB bis zu 98% günstiger sein als diese anderen Lösungen (für Transaktionen von 1KB).

## <a name="next-steps"></a>Nächste Schritte

Bleiben Sie auf dem Laufenden, was neue Artikel zum Optimieren der DocumentDB-Ressourcenbereitstellung betrifft. In der Zwischenzeit laden wir Sie ein, unseren [RU-Rechner](https://www.documentdb.com/capacityplanner) zu nutzen.

