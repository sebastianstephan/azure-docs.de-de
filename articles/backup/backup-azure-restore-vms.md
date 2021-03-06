---
title: Wiederherstellen eines virtuellen Computers aus einer Sicherung | Microsoft Docs
description: Erfahren Sie, wie ein virtueller Azure-Computer mithilfe eines Wiederherstellungspunkts wiederhergestellt wird.
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: Sicherung wiederherstellen; Wiederherstellungsschritte; Wiederherstellungspunkt;
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: trinadhk; jimpark;
translationtype: Human Translation
ms.sourcegitcommit: 356de369ec5409e8e6e51a286a20af70a9420193
ms.openlocfilehash: 64557a71f30762befe07616c3d274a621f22e235
ms.lasthandoff: 03/27/2017


---
# <a name="restore-virtual-machines-in-azure"></a>Wiederherstellen virtueller Computer in Azure
> [!div class="op_single_selector"]
> * [Wiederherstellen virtueller Computer im Azure-Portal](backup-azure-arm-restore-vms.md)
> * [Wiederherstellen virtueller Computer im klassischen Portal](backup-azure-restore-vms.md)
> 
> 

Führen Sie die folgenden Schritte aus, um einen virtuellen Computer aus den Sicherungen im Azure-Sicherungstresor in einem neuen virtuellen Computer wiederherzustellen.

## <a name="restore-workflow"></a>Wiederherstellen von Workflows
### <a name="step-1-choose-an-item-to-restore"></a>Schritt 1: Auswählen eines wiederherzustellenden Elements
1. Navigieren Sie zur Registerkarte **Geschützte Elemente** , und wählen Sie den virtuellen Computer aus, den Sie in einem neuen virtuellen Computer wiederherstellen möchten.
   
    ![Geschützte Elemente](./media/backup-azure-restore-vms/protected-items.png)
   
    Die Spalte **Wiederherstellungspunkt** auf der Seite **Geschützte Elemente** teilt Ihnen die Anzahl der Wiederherstellungspunkte für einen virtuellen Computer mit. Die Spalte **Neuester Wiederherstellungspunkt** enthält den Zeitpunkt der letzten Sicherung, aus der ein virtueller Computer wiederhergestellt werden kann.
2. Klicken Sie auf **Wiederherstellen**, um den Assistenten **Element wiederherstellen** zu öffnen.
   
    ![Element wiederherstellen](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Schritt 2: Auswählen eines Wiederherstellungspunkts
1. Auf dem Bildschirm **Wählen Sie einen Wiederherstellungspunkt** können Sie eine Wiederherstellung vom neuesten Wiederherstellungspunkt oder von einem früheren Zeitpunkt durchführen. Die ausgewählte Standardoption beim Öffnen des Assistenten ist *Neuester Wiederherstellungspunkt*.
   
    ![Wählen Sie einen Wiederherstellungspunkt](./media/backup-azure-restore-vms/select-recovery-point.png)
2. Um einen früheren Zeitpunkt auszuwählen, wählen Sie in der Dropdownliste die Option **Datum auswählen**. Wählen Sie dann durch Klicken auf das **Kalendersymbol** ein Datum im Kalendersteuerelement aus. Im Steuerelement enthalten alle Datumsangaben mit Wiederherstellungspunkten eine hellgraue Schattierung und können vom Benutzer ausgewählt werden.
   
    ![Auswählen eines Datums](./media/backup-azure-restore-vms/select-date.png)
   
    Nachdem Sie im Kalendersteuerelement auf ein Datum geklickt haben, werden die an diesem Datum verfügbaren Wiederherstellungspunkte in der folgenden Tabelle mit Wiederherstellungspunkten angezeigt. Die Spalte **Zeit** gibt die Zeit an, zu der die Momentaufnahme erstellt wurde. Die Spalte **Typ** zeigt die [Konsistenz](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) des Wiederherstellungspunkts an. Die Tabellenüberschrift zeigt in Klammern die Anzahl der Wiederherstellungspunkte an, die an diesem Tag verfügbar sind.
   
    ![Wiederherstellungspunkte](./media/backup-azure-restore-vms/recovery-points.png)
3. Wählen Sie den Wiederherstellungspunkt in der Tabelle **Wiederherstellungspunkte** aus, und klicken Sie auf den Pfeil „Weiter“, um zum nächsten Bildschirm zu gelangen.

### <a name="step-3-specify-a-destination-location"></a>Schritt 3: Angeben eines Zielspeicherorts
1. Geben Sie im Bildschirm **Wiederherstellungsinstanz auswählen** Details an, wo der virtuelle Computer wiederhergestellt werden soll.
   
   * Geben Sie den Namen des virtuellen Computers an: In einem bestimmten Clouddienst sollte der Name des virtuellen Computers eindeutig sein. Das Überschreiben vorhandener VMs wird nicht unterstützt. 
   * Wählen Sie einen Clouddienst für den virtuellen Computer aus: Dies ist für das Erstellen eines virtuellen Computers erforderlich. Sie können entweder einen vorhandenen Clouddienst verwenden oder einen neuen Clouddienst erstellen.
     
        Der ausgewählte Clouddienstname sollte global eindeutig sein. In der Regel wird der Name des Clouddiensts einer öffentlich zugänglichen URL in dieser Form zugeordnet: [cloudservice].cloudapp.net. In Azure können Sie keinen neuen Clouddienst erstellen, wenn der Name bereits verwendet wurde. Wenn Sie einen neuen Clouddienst erstellen möchten, erhält dieser denselben Namen wie der virtuelle Computer. In diesem Fall sollte der Name des virtuellen Computers eindeutig genug sein, um auf den zugeordneten Clouddienst angewendet werden zu können.
     
        Es werden nur Clouddienste und virtuelle Netzwerke angezeigt, die keiner Affinitätsgruppe in den Details zur Instanzenwiederherstellung zugeordnet sind. [Weitere Informationen](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Wählen Sie ein Speicherkonto für den virtuellen Computer aus: Dies ist für das Erstellen des virtuellen Computers erforderlich. Sie können aus vorhandenen Speicherkonten in der gleichen Region auswählen, in der sich auch der Azure Backup-Tresor befindet. Wir unterstützen keine Speicherkonten, die zonenredundant sind oder dem Premium-Speichertyp entsprechen.
   
    Wenn es keine Speicherkonten mit unterstützter Konfiguration gibt, erstellen Sie ein Speicherkonto mit unterstützter Konfiguration, bevor Sie mit dem Wiederherstellungsvorgang beginnen.
   
    ![Auswählen eines virtuellen Netzwerks](./media/backup-azure-restore-vms/restore-sa.png)
3. Wählen Sie ein virtuelles Netzwerk aus: Das virtuelle Netzwerk (VNET) für den virtuellen Computer muss zum Zeitpunkt der Erstellung des virtuellen Computers ausgewählt werden. Die Wiederherstellungsoberfläche zeigt alle VNETs innerhalb dieses Abonnements, die verwendet werden können. Es ist nicht notwendig, ein VNET für die wiederhergestellte VM auszuwählen – Sie können mit dem wiederhergestellten virtuellen Computer auch dann eine Verbindung über das Internet herstellen, wenn das VNET nicht angewendet wird.
   
    Wenn der Clouddienst einem virtuellen Netzwerk zugeordnet wird, können Sie das virtuelle Netzwerk nicht ändern.
   
    ![Auswählen eines virtuellen Netzwerks](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Wählen Sie ein Subnetz: Für den Fall, dass das VNET über Subnetze verfügt, wird standardmäßig das erste Subnetz ausgewählt. Wählen Sie in den Dropdownoptionen das Subnetz Ihrer Wahl aus. Rufen Sie Details zu Subnetzen auf, indem Sie auf der [Portal-Startseite](https://manage.windowsazure.com/)unter „Netzwerkerweiterungen“ die Option **Virtual Networks** und anschließend das virtuelle Netzwerk auswählen und einen Drilldown für „Konfigurieren“ ausführen.
   
    ![Auswählen eines Subnetzes](./media/backup-azure-restore-vms/select-subnet.png)
5. Klicken Sie im Assistenten auf das Symbol **Senden** , um die Details zu übermitteln und einen Wiederherstellungsauftrag zu erstellen.

## <a name="track-the-restore-operation"></a>Nachverfolgen des Wiederherstellungsvorgangs
Nachdem Sie alle Informationen in den Wiederherstellungs-Assistenten eingegeben und übermittelt haben, versucht Azure Backup einen Auftrag zur Nachverfolgung des Wiederherstellungsvorgangs zu erstellen.

![Erstellen eines Wiederherstellungsauftrags](./media/backup-azure-restore-vms/create-restore-job.png)

Wenn die Auftragserstellung erfolgreich ist, wird in einer Popupbenachrichtigung angezeigt, dass der Auftrag erstellt wird. Sie können weitere Details abrufen, indem Sie auf die Schaltfläche **Auftrag anzeigen** klicken. So gelangen Sie zur Registerkarte **Aufträge**.

![Wiederherstellungsauftrag erstellt](./media/backup-azure-restore-vms/restore-job-created.png)

Nach dem Abschluss des Wiederherstellungsvorgangs wird dieser auf der Registerkarte **Aufträge** als "Abgeschlossen" markiert.

![Wiederherstellungsauftrag abgeschlossen](./media/backup-azure-restore-vms/restore-job-complete.png)

Nach dem Wiederherstellen des virtuellen Computers müssen Sie möglicherweise die auf dem ursprünglichen virtuellen Computer vorhandenen Erweiterungen neu installieren und für den virtuellen Computer im Azure-Portal [die Endpunkte ändern](../virtual-machines/windows/classic/setup-endpoints.md) .

## <a name="post-restore-steps"></a>Schritte nach der Wiederherstellung
Bei Verwendung einer Cloud-Init-basierten Linux-Verteilung wie etwa Ubuntu wird das Kennwort aus Sicherheitsgründen nach der Wiederherstellung blockiert. Verwenden Sie zum [Zurücksetzen des Kennworts](../virtual-machines/linux/classic/reset-access.md)die VMAccess-Erweiterung auf dem wiederhergestellten virtuellen Computer. Es wird empfohlen, SSH-Schlüssel für diese Verteilungen zu verwenden, um das Zurücksetzen des Kennworts nach der Wiederherstellung zu vermeiden. 

## <a name="backup-for-restored-vms"></a>Sicherung für wiederhergestellte virtuelle Computer
Wenn Sie den virtuellen Computer unter dem gleichen Clouddienst mit dem gleichen Namen wie die ursprünglich gesicherte VM wiederhergestellt haben, wird die VM nach der Wiederherstellung weiterhin gesichert. Wenn Sie entweder die VM unter einem anderen Clouddienst wiederhergestellt oder einen anderen Namen für die wiederhergestellte VM angegeben haben, wird sie als neue VM behandelt, und Sie müssen die Sicherung für die wiederhergestellte VM einrichten.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Wiederherstellen eines virtuellen Computers während einer Azure-Datencenter-Notfallwiederherstellung
Mit Azure Backup können gesicherte virtuelle Computer im gekoppelten Datencenter wiederhergestellt werden, falls in dem primären Datencenter, in dem VMs ausgeführt werden, ein Notfall eingetreten ist, und Sie den Sicherungstresor als georedundant konfiguriert haben. Bei solchen Szenarien müssen Sie ein Speicherkonto auswählen, das im gekoppelten Datencenter vorhanden ist – ansonsten ändert sich am Wiederherstellungsprozess nichts. Azure Backup verwendet den Computedienst des gekoppelten georedundanten Datencenters, um den wiederhergestellten virtuellen Computer zu erstellen. Erfahren Sie mehr über die [Resilienz der Azure-Rechenzentren](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md).

## <a name="restoring-domain-controller-vms"></a>Wiederherstellen von virtuellen Computern des Domänencontrollers
Die Sicherung von virtuellen Computern des Domänencontrollers wird in Azure Backup unterstützt. Der Wiederherstellungsvorgang erfordert jedoch besondere Sorgfalt. Der Wiederherstellungsvorgang für virtuelle Computer eines Domänencontrollers in einer Konfiguration mit einem einzelnen Domänencontroller unterscheidet sich stark von der Wiederherstellung von virtuellen Computern in einer Konfiguration mit mehreren Domänencontrollern.

### <a name="single-dc"></a>Einzelner Domänencontroller
Der virtuelle Computer kann (wie alle anderen virtuellen Computer) über das Azure-Portal oder mithilfe von PowerShell wiederhergestellt werden.

### <a name="multiple-dcs"></a>Mehrere Domänencontroller
In einer Umgebung mit mehreren Domänencontrollern synchronisieren die Domänencontroller Daten mit einer eigenen Methode. Wenn ein älterer Sicherungspunkt *ohne entsprechende Vorsichtsmaßnahmen*wiederhergestellt wird, kann das USN-Rollback eine Umgebung mit mehreren Domänencontrollern durcheinanderbringen. Die richtige Methode zum Wiederherstellen eines solchen virtuellen Computers besteht im Starten im DSRM-Modus.

Das Problem tritt auf, weil der DSRM-Modus in Azure nicht vorhanden ist. Zum Wiederherstellen eines virtuellen Computers können Sie also nicht das Azure-Portal verwenden. Der einzige unterstützte Wiederherstellungsmechanismus ist die datenträgerbasierte Wiederherstellung mithilfe von PowerShell.

> [!WARNING]
> Verwenden Sie für virtuelle Computer des Domänencontrollers in einer Umgebung mit mehreren Domänencontrollern nicht das Azure-Portal für die Wiederherstellung. Nur die PowerShell-basierte Wiederherstellung wird unterstützt.
> 
> 

Hier finden Sie weitere Informationen zum [USN-Rollback-Problem](https://technet.microsoft.com/library/dd363553) und den vorgeschlagenen Strategien zum Beheben des Problems.

## <a name="restoring-vms-with-special-network-configurations"></a>Wiederherstellen von VMs mit speziellen Netzwerkkonfigurationen
Azure Backup unterstützt die Sicherung für die folgenden speziellen Netzwerkkonfigurationen virtueller Computer.

* VMs unter Lastenausgleich (intern und extern)
* VMs mit mehreren reservierten IP-Adressen
* VMs mit mehreren Netzwerkkarten (NICs)

Bei diesen Konfigurationen müssen bei ihrer Wiederherstellung die folgende Aspekte berücksichtigt werden.

> [!TIP]
> Verwenden Sie den PowerShell-basierten Wiederherstellungsprozess zum erneuten Erstellen der speziellen Netzwerkkonfiguration von VMs im Anschluss an die Wiederherstellung.
> 
> 

### <a name="restoring-from-the-ui"></a>Wiederherstellung über die Benutzeroberfläche:
Beim Wiederherstellen über die Benutzeroberfläche **müssen Sie stets einen neuen Clouddienst wählen**. Da das Portal während des Wiederherstellungsprozesses nur Pflichtparameter verwendet, geht bei VMs, die über die Benutzeroberfläche wiederhergestellt werden, die spezielle Netzwerkkonfiguration verloren. Dies bedeutet, dass wiederhergestellte VMs herkömmliche VMs sind, die ohne Load Balancer bzw. mehrere NICs oder reservierte IP-Adressen konfiguriert sind.

### <a name="restoring-from-powershell"></a>Wiederherstellung über PowerShell:
PowerShell bietet die Möglichkeit, nur die VM-Datenträger aus einer Sicherung wiederherzustellen, ohne den virtuellen Computer zu erstellen. Dies ist hilfreich, wenn virtuelle Computer wiederhergestellt werden, die die oben erwähnten speziellen Konfigurationen erfordern.

Zum vollständigen Wiederherstellen des virtuellen Computers im Anschluss an die Wiederherstellung von Datenträgern gehen Sie so vor:

1. Stellen Sie die Datenträger aus dem Sicherungstresor mithilfe von [Azure Backup PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm) wieder her.
2. Erstellen mithilfe der PowerShell-Cmdlets die für Load Balancer/mehrere NICs/mehrere reservierte IP-Adressen erforderliche VM-Konfiguration, und verwenden Sie sie zum Erstellen der VM mit der gewünschten Konfiguration.
   
   * Erstellen Sie die VM im Clouddienst mit [internem Load Balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Erstellen Sie die VM zum Herstellen einer Verbindung mit dem [Load Balancer mit Internetzugriff](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/).
   * Erstellen Sie die VM mit [mehreren NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Erstellen Sie die VM mit [mehreren reservierten IP-Adressen](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Nächste Schritte
* [Problembehandlung](backup-azure-vms-troubleshoot.md#restore)
* [Verwalten virtueller Computer](backup-azure-manage-vms.md)


