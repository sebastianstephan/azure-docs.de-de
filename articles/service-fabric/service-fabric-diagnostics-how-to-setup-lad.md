---
title: Sammeln von Protokollen mit der Linux-Azure-Diagnose | Microsoft Docs
description: In diesem Artikel erfahren Sie, wie Sie die Azure-Diagnose so konfigurieren, dass Protokolle aus einem Linux-basierten Service Fabric-Cluster unter Azure gesammelt werden.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar
translationtype: Human Translation
ms.sourcegitcommit: 356de369ec5409e8e6e51a286a20af70a9420193
ms.openlocfilehash: 46b62b0ebc5b81241815e3b5b4fa3fe275b88af1
ms.lasthandoff: 03/27/2017


---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Sammeln von Protokollen mit der Azure-Diagnose
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Bei Verwendung eines Azure Service Fabric-Clusters empfiehlt es sich, die Protokolle aller Knoten an einem zentralen Ort zu sammeln. Das Sammeln der Protokolle an einem zentralen Ort vereinfacht die Analyse und Behandlung von Problemen, die ggf. in Ihren Diensten, in Ihrer Anwendung oder im Cluster auftreten. Eine Möglichkeit zum Hochladen und Sammeln von Protokollen ist die Verwendung der Erweiterung Azure-Diagnose, mit der Protokolle an Azure Storage, Azure Application Insights oder Azure Event Hubs hochgeladen werden. Die Ereignisse können auch aus dem Speicher oder aus Event Hubs gelesen und in einem Produkt wie [Log Analytics](../log-analytics/log-analytics-service-fabric.md) oder in einer anderen Protokollanalyselösung verwendet werden. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) bietet einen umfassenden Dienst zur Suche und Analyse von Protokollen.

## <a name="log-sources-that-you-might-want-to-collect"></a>Protokollquellen, die gesammelt werden können
* **Service Fabric-Protokolle**: Werden von der Plattform mittels [LTTng](http://lttng.org) ausgegeben und in Ihr Speicherkonto hochgeladen. Bei Protokollen kann es sich um Betriebs- oder Laufzeitereignisse handeln, die von der Plattform ausgegeben werden. Diese Protokolle werden an dem vom Clustermanifest angegebenen Speicherort gespeichert. (Um Informationen zum Speicherkonto zu erhalten, suchen Sie nach dem Tag **AzureTableWinFabETWQueryable** und dort nach **StoreConnectionString**.)
* **Anwendungsereignisse**: Werden von Ihrem Dienstcode ausgegeben. Sie können eine beliebige Protokollierungslösung verwenden, die textbasierte Protokolldateien schreibt (beispielsweise LTTng). Weitere Informationen finden Sie in der LTTng-Dokumentation zur Ablaufverfolgung für Ihre Anwendung.  

## <a name="deploy-the-diagnostics-extension"></a>Bereitstellen der Diagnoseerweiterung
Zum Sammeln von Protokollen muss zunächst die Diagnoseerweiterung auf allen VMs des Service Fabric-Clusters bereitgestellt werden. Die Diagnoseerweiterung sammelt Protokolle auf allen VMs und lädt sie in das angegebene Speicherkonto hoch. Die auszuführenden Schritte hängen davon ab, ob Sie das Azure-Portal oder Azure Resource Manager verwenden.

Wenn Sie die Diagnoseerweiterung im Rahmen der Clustererstellung für die im Cluster enthaltenen virtuellen Computer bereitstellen möchten, legen Sie **Diagnose** auf **Ein** fest. Nach der Erstellung des Clusters können Sie diese Einstellung nicht im Portal ändern.

Konfigurieren Sie dann die Linux-Azure-Diagnose (LAD) so, dass sie die Dateien erfasst und in Ihrem Speicherkonto ablegt. Dieser Prozess wird im Artikel [Verwenden der Linux-Diagnoseerweiterung zur Überwachung der Leistungs- und Diagnosedaten einer Linux-VM](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) als drittes Szenario („Hochladen eigener Protokolldateien“) beschrieben. Befolgen Sie diesen Prozess, um Zugriff auf die Ablaufverfolgungen zu erhalten. Sie können die Ablaufverfolgungsdaten in ein Visualisierungstool Ihrer Wahl hochladen.

Die Diagnoseerweiterung kann auch mithilfe von Azure Resource Manager bereitgestellt werden. Die Dokumentation für Windows-Cluster finden Sie unter [Sammeln von Protokollen mit Azure-Diagnose](service-fabric-diagnostics-how-to-setup-wad.md). Für Linux wird ein ähnlicher Prozess verwendet.

Sie können auch die Operations Management Suite verwenden, wie unter [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) (Operations Management Suite-Protokollanalyse mit Linux) beschrieben.

Nach Abschluss der Konfiguration überwacht der LAD-Agent die angegebenen Protokolldateien. Sobald bei einer Datei eine neue Zeile hinzukommt, erstellt der Agent einen Syslog-Eintrag, der an den von Ihnen angegebenen Speicher gesendet wird.

## <a name="next-steps"></a>Nächste Schritte
Ausführlichere Informationen zu relevanten Ereignissen für die Problembehandlung finden Sie in der [LTTng-Dokumentation](http://lttng.org/docs) sowie unter [Verwenden der Linux-Diagnoseerweiterung zur Überwachung der Leistungs- und Diagnosedaten einer Linux-VM](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).


