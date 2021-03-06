---
title: Verwalten von StorSimple-Sicherungsrichtlinien | Microsoft Docs
description: "Beschreibt, wie Sie den StorSimple Manager-Dienst zum Erstellen und Verwalten von manuellen Sicherungen, Sicherungszeitplänen und zur Sicherungsaufbewahrung verwenden können."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: b43d5d867d6245a807f6eff5ed3a0c3df10c0dd7


---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies"></a>Verwalten von Sicherungsrichtlinien mithilfe des StorSimple Manager-Diensts
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Übersicht
In diesem Tutorial wird erläutert, wie Sie die Seite **Sicherungsrichtlinien** des StorSimple-Manager-Dienstes verwenden, um Sicherungsprozesse und die Sicherungsaufbewahrung für Ihre StorSimple-Volumes zu steuern. Außerdem wird beschrieben, wie eine manuelle Sicherung durchgeführt wird.

Über die Seite **Sicherungsrichtlinien** können Sie Sicherungsrichtlinien verwalten und lokale sowie Cloudmomentaufnahmen zeitlich planen. (Sicherungsrichtlinien werden zum Konfigurieren von Sicherungszeitplänen und der Sicherungsaufbewahrung für eine Sammlung von Volumes verwendet.) Mithilfe von Sicherungsrichtlinien können Sie eine Momentaufnahme mehrerer Volumes gleichzeitig erstellen. Dies bedeutet, dass es sich bei durch Sicherungsrichtlinien erstellten Sicherungen um ausfallsichere Kopien handelt. Auf dieser Seite werden alle Sicherungsrichtlinien, ihre Typen, die zugehörigen Volumes, die Anzahl der aufbewahrten Sicherungen und die Option zum Aktivieren dieser Richtlinien aufgeführt.

Auf der Seite **Sicherungsrichtlinien** können Sie außerdem die vorhandenen Sicherungsrichtlinien anhand von einem oder mehreren der folgenden Felder filtern:

* **Richtlinienname** – Der der Richtlinie zugeordnete Name. Die folgenden verschiedenen Richtlinientypen sind verfügbar:
  
  * Geplante Richtlinien, die explizit vom Benutzer erstellt werden.
  * Automatische Richtlinien, die erstellt werden, wenn die Option "Standardsicherung für dieses Volume" zum Zeitpunkt der Volumeerstellung aktiviert war Diese Richtlinien tragen den Namen "VolumeName_Default". Diese Richtlinien tragen den Namen "VolumeName_Default". Dabei bezieht sich "VolumeName" auf den Namen des StorSimple-Volumes, das vom Benutzer im klassischen Azure-Portal konfiguriert wird.  Die automatischen Richtlinien bewirken tägliche Cloudmomentaufnahmen, die um 22:30 Uhr Gerätezeit beginnen.
  * Importierte Richtlinien, die ursprünglich im StorSimple-Momentaufnahme-Manager erstellt wurden. Diese weisen ein Tag auf, das den StorSimple-Momentaufnahme-Manager-Host beschreibt, von dem die Richtlinien importiert wurden.
* **Volumes** – Die Volumes, die der Richtlinie zugeordnet sind. Alle Volumes, die einer Sicherungsrichtlinie zugeordnet sind, werden beim Erstellen von Sicherungen gruppiert.
* **Letzte erfolgreiche Sicherung** – Das Datum und die Uhrzeit der letzten erfolgreichen Sicherung, die mit dieser Richtlinie erstellt wurde.
* **Nächste Sicherung** – Das Datum und die Uhrzeit der nächsten geplanten Sicherung, die von dieser Richtlinie initiiert wird.
* **Zeitpläne** – Die Anzahl der Zeitpläne, die der Sicherungsrichtlinie zugeordnet sind.

Auf dieser Seite können die folgenden allgemeinen Vorgänge ausgeführt werden:

* Hinzufügen einer Sicherungsrichtlinie 
* Hinzufügen oder Ändern eines Zeitplans 
* Löschen einer Sicherungsrichtlinie 
* Erstellen einer manuellen Sicherung 
* Erstellen einer benutzerdefinierten Sicherungsrichtlinie mit mehreren Volumes und Zeitplänen 

## <a name="add-a-backup-policy"></a>Hinzufügen einer Sicherungsrichtlinie
Fügen Sie eine Sicherungsrichtlinie zum automatischen Planen Ihrer Sicherungen hinzu. Führen Sie die folgenden Schritte im klassischen Azure-Portal aus, um eine Sicherungsrichtlinie für Ihr StorSimple-Gerät hinzuzufügen. Nachdem Sie die Richtlinie hinzugefügt haben, können Sie einen Zeitplan definieren (siehe [Hinzufügen oder Ändern eines Zeitplans](#add-or-modify-a-schedule).

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

![Video verfügbar](./media/storsimple-manage-backup-policies/Video_icon.png) **Video verfügbar**

Sie können sich [hier](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)ein Video anschauen, in dem das Erstellen einer lokalen Sicherungsrichtlinie oder einer Sicherungsrichtlinie in der Cloud demonstriert wird.

## <a name="add-or-modify-a-schedule"></a>Hinzufügen oder Ändern eines Zeitplans
Sie können einen Zeitplan hinzufügen oder ändern, der an eine vorhandene Sicherungsrichtlinie auf Ihrem StorSimple-Gerät angefügt wird. Führen Sie die folgenden Schritte im klassischen Azure-Portal aus, um einen Zeitplan hinzuzufügen oder zu ändern:

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a>Löschen einer Sicherungsrichtlinie
Führen Sie die folgenden Schritte im klassischen Azure-Portal aus, um eine Sicherungsrichtlinie für Ihr StorSimple-Gerät zu löschen.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Erstellen einer manuellen Sicherung
Führen Sie die folgenden Schritte im klassischen Azure-Portal aus, um bei Bedarf eine (manuelle) Sicherung für ein einzelnes Volume zu erstellen.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Erstellen einer benutzerdefinierten Sicherungsrichtlinie mit mehreren Volumes und Zeitplänen
Führen Sie die folgenden Schritte im klassischen Azure-Portal aus, um eine benutzerdefinierte Sicherungsrichtlinie mit mehreren Volumes und Zeitplänen zu erstellen.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zum [Verwenden Ihres StorSimple-Geräts mithilfe des StorSimple Manager-Diensts](storsimple-manager-service-administration.md).




<!--HONumber=Nov16_HO3-->


