---
title: "Problembehandlung bei Azure Virtual Network-Gateways und -Verbindungen – PowerShell | Microsoft-Dokumentation"
description: "Auf dieser Seite wird erläutert, wie Azure Network Watcher zur Problembehandlung von PowerShell verwendet wird."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
translationtype: Human Translation
ms.sourcegitcommit: 50d82847fb629880f298f79f9ab791a13836f01c
ms.openlocfilehash: 8b2df558c6793d5dab7dd7cb6d1f19d279cfa153
ms.lasthandoff: 03/31/2017


---

# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Problembehandlung bei Virtual Network-Gateways und -Verbindungen mit Azure Network Watcher und PowerShell

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [BEFEHLSZEILENSCHNITTSTELLE (CLI)](network-watcher-troubleshoot-manage-cli.md)
> - [REST-API](network-watcher-troubleshoot-manage-rest.md)

Network Watcher bietet viele Funktionen zum Erfassen von Informationen über Ihre Netzwerkressourcen in Azure. Zu diesen Funktionen zählt u.a. die Ressourcenproblembehandlung. Die Ressourcenproblembehandlung kann über PowerShell, die CLI oder die REST-API aufgerufen werden. Bei Aufruf untersucht Network Watcher die Integrität von Virtual Network-Gateways oder -Verbindungen und gibt entsprechende Ergebnisse zurück.

## <a name="before-you-begin"></a>Voraussetzungen

Dieses Szenario setzt voraus, dass Sie die Schritte unter [Create an Azure Network Watcher instance](network-watcher-create.md) (Erstellen einer Azure Network Watcher-Instanz) bereits ausgeführt haben, um eine Network Watcher-Instanz zu erstellen.

## <a name="overview"></a>Übersicht

Die Ressourcenproblembehandlung bietet die Möglichkeit zum Behandeln von Problemen, die bei Virtual Network-Gateways und -Verbindungen auftreten können. Wenn eine Anforderung an die Ressourcenproblembehandlung gesendet wird, werden Protokolle abgefragt und untersucht. Nach Abschluss der Untersuchung werden die Ergebnisse zurückgegeben. Anforderungen der Ressourcenproblembehandlung sind Anforderungen mit langer Ausführungszeit. Daher kann es mehrere Minuten dauern, bis ein Ergebnis zurückgegeben wird. Die Protokolle der Problembehandlung werden in einem Container in einem angegebenen Speicherkonto gespeichert.

## <a name="retrieve-network-watcher"></a>Abrufen von Network Watcher

Der erste Schritt besteht im Abrufen der Network Watcher-Instanz. Die Variable `$networkWatcher` wird in Schritt 4 an das Cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` übergeben.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Abrufen einer Virtual Network-Gatewayverbindung

In diesem Beispiel wird die Ressourcenproblembehandlung für eine Verbindung ausgeführt. Sie können auch ein Virtual Network-Gateway übergeben.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a>Erstellen Sie ein Speicherkonto.

Die Ressourcenproblembehandlung gibt Daten zur Integrität der Ressource zurück. Zudem speichert sie Protokolle zur Überprüfung in einem Speicherkonto. In diesem Schritt erstellen wir ein Speicherkonto. Wenn bereits ein Speicherkonto vorhanden ist, können Sie es verwenden.

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
```

## <a name="run-network-watcher-resource-troubleshooting"></a>Ausführen der Network Watcher-Ressourcenproblembehandlung

Die Problembehandlung für Ressourcen wird mithilfe des Cmdlets `Start-AzureRmNetworkWatcherResourceTroubleshooting` durchgeführt. An das Cmdlet werden das Network Watcher-Objekt, die ID der Verbindung oder des Virtual Network-Gateways, die Speicherkonto-ID und der Pfad zum Speichern der Ergebnisse übergeben.

> [!NOTE]
> Das Cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` hat eine lange Ausführungsdauer, daher dauert die Ausführung unter Umständen einige Minuten.

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)logs"
```

Sobald Sie das Cmdlet ausführen, überprüft Network Watcher die Ressource auf ihre Integrität. Die Ergebnisse werden an die Shell zurückgegeben, und Protokolle der Ergebnisse werden im angegebenen Speicherkonto gespeichert.

## <a name="understanding-the-results"></a>Grundlegendes zu den Ergebnissen

Der Aktionstext enthält allgemeine Richtlinien zur Behebung des Problems. Wenn eine Aktion für das Problem ausgeführt werden kann, wird ein Link mit weiteren Anleitungen bereitgestellt. Falls es keine weitere Anleitungen gibt, enthält die Antwort die URL zum Öffnen einer Supportanfrage.  Weitere Informationen zu den Eigenschaften der Antwort und zu deren Inhalt finden Sie unter [Übersicht über die Network Watcher-Problembehandlung](network-watcher-troubleshoot-overview.md).

Anweisungen zum Herunterladen von Dateien von Azure-Speicherkonten finden Sie unter [Erste Schritte mit Azure Blob Storage mit .NET](../storage/storage-dotnet-how-to-use-blobs.md). Ein weiteres Tool, das verwendet werden kann, ist der Speicher-Explorer. Weitere Informationen zum Speicher-Explorer finden Sie unter [Speicher-Explorer](http://storageexplorer.com/).

## <a name="next-steps"></a>Nächste Schritte

Wenn Einstellungen geändert wurden, die die VPN-Konnektivität beenden, finden Sie unter [Verwalten von Netzwerksicherheitsgruppen](../virtual-network/virtual-network-manage-nsg-arm-portal.md) Informationen zum Ermitteln der fraglichen Netzwerksicherheitsgruppe und Sicherheitsregeln.

