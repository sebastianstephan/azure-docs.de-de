---
title: "Problembehandlung bei einem bereitgestellten StorSimple-Gerät | Microsoft Docs"
description: "Beschreibt die Diagnose und Behebung von Fehlern auf einem StorSimple-Gerät, das bereitgestellt und betriebsbereit ist."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 8d1b4905d0a24c8df9eb2c986459286909fd20dc


---
# <a name="troubleshoot-an-operational-storsimple-device"></a>Problembehandlung bei einem betriebsbereiten StorSimple-Gerät
## <a name="overview"></a>Übersicht
Dieser Artikel enthält Anleitungen zum Beheben von Konfigurationsproblemen, die bei einem bereitgestellten und betriebsbereiten StorSimple-Gerät auftreten können. Es werden allgemeine Probleme, mögliche Ursachen und empfohlene Schritte zum Beheben von Problemen bei der Ausführung von Microsoft Azure StorSimple beschrieben. Diese Informationen gelten sowohl für lokale physische als auch für virtuelle StorSimple-Geräte.

Am Ende dieses Artikels finden Sie eine Liste der Fehlercodes, die bei einem Microsoft Azure StorSimple-Vorgang möglicherweise ausgegeben werden. Zudem enthält der Artikel Informationen zum Beheben dieser Fehler. 

## <a name="setup-wizard-process-for-operational-devices"></a>Verfahren des Setup-Assistenten für betriebsbereite Geräte
Mithilfe des Setup-Assistenten ([Invoke-HcsSetupWizard][1]) überprüfen Sie die Gerätekonfiguration und nehmen bei Bedarf Korrekturmaßnahmen vor.

Die Verfahren im Setup-Assistenten unterscheiden sich bei einem bereits konfigurierten und betriebsbereiten Gerät. Sie können nur die folgenden Einträge ändern:

* IP-Adresse, Subnetzmaske und Gateway
* Primärer DNS-Server
* Primärer NTP-Server
* Optionale Webproxy-Konfiguration

Der Setup-Assistent führt keine Vorgänge im Zusammenhang mit der Kennworterfassung und Geräteregistrierung durch.

## <a name="errors-that-occur-during-subsequent-runs-of-the-setup-wizard"></a>Fehler, die bei nachfolgenden Ausführungen des Setup-Assistenten auftreten
In der folgenden Tabelle sind die Fehler, die beim Ausführen des Setup-Assistenten auf einem betriebsbereiten Gerät auftreten können, mögliche Ursachen für diese Fehler sowie empfohlene Maßnahmen zur Problembehebung beschrieben. 

| Nr. | Fehlermeldung oder -bedingung | Mögliche Ursachen | Empfohlene Maßnahme |
|:--- |:--- |:--- |:--- |
| 1 |Fehler 350032: Dieses Gerät wurde bereits deaktiviert. |Dieser Fehler wird angezeigt, wenn Sie den Setup-Assistenten auf einem deaktivierten Gerät ausführen. |[Wenden Sie sich an den Microsoft Support](storsimple-contact-microsoft-support.md) für weitere Schritte. Ein deaktiviertes Gerät kann nicht in Betrieb genommen werden. Sie müssen das Gerät möglicherweise auf die Werkseinstellungen zurücksetzen, bevor es erneut aktiviert werden kann. |
| 2 |Invoke-HcsSetupWizard : ERROR_INVALID_FUNCTION(Ausnahme von HRESULT: 0x80070001) |Das Update des DNS-Servers ist fehlgeschlagen. DNS-Einstellungen sind globale Einstellungen und gelten für alle aktivierten Netzwerkschnittstellen. |Aktivieren Sie die Schnittstelle, und wenden Sie die DNS-Einstellungen erneut an. Dies kann das Netzwerk für andere aktivierten Schnittstellen beeinträchtigen, da es sich um globale Einstellungen handelt. |
| 3 |Das Gerät wird im StorSimple-Manager-Dienstportal als online aufgeführt. Wenn Sie jedoch versuchen, die Mindestinstallation abzuschließen und die Konfiguration speichern, schlägt der Vorgang fehl. |Der Webproxy wurde während der ersten Installation nicht konfiguriert, obwohl ein Proxyserver tatsächlich vorhanden war. |Verwenden Sie das Cmdlet [Test-HcsmConnection][2] , um den Fehler zu suchen. [Wenden Sie sich an den Microsoft Support](storsimple-contact-microsoft-support.md) , wenn Sie das Problem nicht beheben können. |
| 4 |Invoke-HcsSetupWizard: Der Wert liegt nicht innerhalb des erwarteten Bereichs. |Dieser Fehler wird durch eine falsche Subnetzmaske erzeugt. Mögliche Ursachen sind:  <ul><li> Die Subnetzmaske ist nicht vorhanden oder leer.</li><li>Das Format des Ipv6-Präfixes ist falsch.</li><li>Die Schnittstelle ist für die Cloud aktiviert, aber das Gateway ist nicht vorhanden oder ungültig.</li></ul>Beachten Sie, dass die DATA 0-Schnittstelle automatisch über Cloudfunktionalität verfügt, wenn sie über den Setup-Assistenten konfiguriert wird. |Um das Problem zu bestimmen, verwenden Sie die Subnetzmaske 0.0.0.0 oder 256.256.256.256 und überprüfen die Ausgabe. Geben Sie ggf. die korrekten Werte für Subnetzmaske, Gateway und IPv6-Präfix ein. |

## <a name="error-codes"></a>Fehlercodes
Die Fehler sind in numerischer Reihenfolge aufgeführt.

| Fehlernummer | Fehlertext oder Beschreibung | Empfohlene Benutzeraktion |
|:--- |:--- |:--- |
| 10502 |Fehler beim Zugriff auf Ihr Speicherkonto. |Warten Sie einige Minuten, und versuchen Sie es dann erneut. Wenn das Problem weiterhin auftritt, erkundigen Sie sich beim Support von Microsoft nach den weiteren Schritten. |
| 40017 |Beim Sicherungsvorgang ist ein Fehler aufgetreten, da ein in der Sicherungsrichtlinie angegebenes Volume auf dem Gerät nicht gefunden wurde. |Wiederholen Sie den Sicherungsvorgang. Wenn das Problem weiterhin besteht, wenden Sie sich an den Microsoft Support, um Informationen zu den nächsten Schritten zu erhalten. |
| 40018 |Beim Sicherungsvorgang ist ein Fehler aufgetreten, da keines der in der Sicherungsrichtlinie angegebenen Volumes auf dem Gerät gefunden wurde. |Wiederholen Sie den Sicherungsvorgang. Wenn das Problem weiterhin besteht, wenden Sie sich an den Microsoft Support, um Informationen zu den nächsten Schritten zu erhalten. |
| 390061 |Das System ist ausgelastet oder nicht verfügbar. |Warten Sie einige Minuten, und versuchen Sie es dann erneut. Wenn das Problem weiterhin auftritt, erkundigen Sie sich beim Support von Microsoft nach den weiteren Schritten. |
| 390143 |Ein Fehler mit dem Fehlercode 390143 ist aufgetreten. (Unbekannter Fehler) |Wenn das Problem weiterhin auftritt, erkundigen Sie sich beim Support von Microsoft nach den weiteren Schritten. |

## <a name="next-steps"></a>Nächste Schritte
Wenn das Problem nicht behoben werden kann, [wenden Sie sich an den Support von Microsoft](storsimple-contact-microsoft-support.md) , um Unterstützung zu erhalten. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx



<!--HONumber=Nov16_HO3-->


