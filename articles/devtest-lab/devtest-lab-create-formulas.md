---
title: Erstellen von Formeln in Azure DevTest Labs | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Azure DevTest Labs-Formeln erstellen und zum Erstellen neuer virtueller Computer verwenden.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
translationtype: Human Translation
ms.sourcegitcommit: afe143848fae473d08dd33a3df4ab4ed92b731fa
ms.openlocfilehash: 4f9f86c2cc106aa96f27293a43cd784e2fb6fe76
ms.lasthandoff: 03/17/2017


---
# <a name="create-azure-devtest-labs-formulas"></a>Erstellen von Azure DevTest Labs-Formeln

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

Dieser Artikel veranschaulicht, wie Sie eine Formel anhand einer Basis (benutzerdefiniertes Image, Marketplace-Image oder eine andere Formel) oder aus einem vorhandenen virtuellen Computer erstellen. 

## <a name="create-a-formula"></a>Erstellen einer Formel
Jeder Benutzer mit der Berechtigung *Benutzer* in DevTest Labs kann virtuelle Computer auf Basis einer Formel erstellen. Es gibt zwei Möglichkeiten, um Formeln zu erstellen: 

* Anhand einer Basis: Entscheiden Sie sich für diese Option, wenn Sie alle Merkmale der Formel definieren möchten.
* Aus einem vorhandenen virtuellen Labcomputer: Entscheiden Sie sich für diese Option, wenn Sie eine Formel basierend auf den Einstellungen eines vorhandenen virtuellen Computers erstellen möchten.

Weitere Informationen zum Hinzufügen von Benutzern und Berechtigungen finden Sie unter [Hinzufügen von Besitzern und Benutzern in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Erstellen einer Formel anhand einer Basis
In den folgenden Schritten wird beschrieben, wie Sie eine Formel auf der Basis eines benutzerdefinierten Images, eines Marketplace-Images oder auf Grundlage einer anderen Formel erstellen.

1. Melden Sie sich beim [Azure-Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)an.

2. Wählen Sie **Weitere Dienste** und dann in der Liste **DevTest Labs** aus.

3. Wählen Sie in der Liste der Labs das gewünschte Lab aus.  

4. Wählen Sie auf dem Blatt für das Lab die Option **Formulas (reusable bases)**(Formeln (wiederverwendbare Basis)) aus.
   
    ![Menü „Formel“](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. Wählen Sie auf dem Blatt **Formeln** die Option **+ Hinzufügen**.
   
    ![Formel hinzufügen](./media/devtest-lab-create-formulas/add-formula.png)

6. Wählen Sie auf dem Blatt **Choose a base** (Basis auswählen) die Grundlage aus, anhand derer Sie die Formel erstellen möchten (also das benutzerdefinierte Image, das Marketplace-Image oder die Formel).
   
    ![Basisliste](./media/devtest-lab-create-formulas/base-list.png)

7. Geben Sie auf dem Blatt **Formel erstellen** folgende Werte an:
   
    * **Formelname**: Geben Sie einen Namen für die Formel ein. Dieser Wert wird in der Liste der Basisimages angezeigt, wenn Sie einen virtuellen Computer erstellen. Der Name wird während der Eingabe überprüft. Falls er nicht gültig ist, werden Sie in einer Meldung über die Anforderungen für einen gültigen Namen informiert.
    * **Beschreibung** : Geben Sie eine aussagekräftige Beschreibung für Ihre Formel ein. Dieser Wert steht über das Kontextmenü der Formel zur Verfügung, wenn Sie einen virtuellen Computer erstellen.
    * **Benutzername**: Geben Sie einen Benutzernamen ein, dem Administratorrechte erteilt wurden.
    * **Kennwort**: Geben Sie einen Wert ein, der dem geheimen Schlüssel bzw. dem Kennwort zugeordnet ist, das für den angegebenen Benutzer verwendet werden soll, oder wählen Sie diesen Wert aus der Dropdownliste aus. Weitere Informationen zu den Geheimnissen finden Sie unter [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/) (Azure DevTest Labs: Persönlicher Geheimnisspeicher).
    * **Datenträgertyp des virtuellen Computers**: Geben Sie entweder HDD (Festplattenlaufwerk) oder SSD (Solid-State Drive) als den Speichertyp an, der für die mit diesem Basisimage bereitgestellten virtuellen Computer zulässig ist.
    * **Größe des virtuellen Computers**: Wählen Sie eines der vordefinierten Elemente aus, die die Prozessorkerne, die RAM-Größe und die Größe der Festplatte für den zu erstellenden virtuellen Computer angeben. 
    * **Artefakte**: Wählen Sie diese Option aus, um das Blatt **Artefakte hinzufügen** zu öffnen, auf dem Sie die Artefakte auswählen und konfigurieren, die Sie dem Basisimage hinzufügen möchten. Weitere Informationen zu Artefakten finden Sie unter [Verwalten von VM-Artefakten in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Erweiterte Einstellungen**: Wählen Sie diese Option aus, um das Blatt **Erweitert** zu öffnen, auf dem Sie die folgenden Einstellungen konfigurieren:
        * **Virtuelles Netzwerk** : Geben Sie das gewünschte virtuelle Netzwerk an.
        * **Subnetz** : Geben Sie das gewünschte Subnetz an.    
        * **IP-Adresskonfiguration**: Geben Sie an, ob Sie öffentliche, private oder freigegebene IP-Adressen verwenden möchten. Weitere Informationen zu freigegebenen IP-Adressen finden Sie unter [Grundlegendes zu freigegebenen IP-Adressen in Azure DevTest Labs](./devtest-lab-shared-ip.md).
        * **Diesen Computer als anforderbar festlegen**: Wenn Sie einen Computer als „anforderbar“ festlegen, bedeutet dies, dass dem Computer zum Zeitpunkt der Erstellung kein Besitz zugewiesen wird. Auf dem Blatt des Labs können Labbenutzer den Besitz des Computers übernehmen (den Computer „anfordern“).     
    * **Image** : Dieses Feld zeigt den Namen des Basisimage an, das Sie auf dem vorherigen Blatt ausgewählt haben. 
     
       ![Formel erstellen](./media/devtest-lab-create-formulas/create-formula.png)

8. Wählen Sie **Erstellen** , um die Formel zu erstellen.

9. Wenn die Formel erstellt wurde, wird sie in der Liste auf dem Blatt **Formeln** angezeigt.

### <a name="create-a-formula-from-a-vm"></a>Erstellen einer Formel aus einem virtuellen Computer
Die folgenden Schritte führen Sie durch den Prozess der Erstellung einer neuen Formel aus einem vorhandenen virtuellen Labcomputer. 

> [!NOTE]
> Damit Sie anhand eines virtuellen Computers eine Formel erstellen können, muss dieser virtuelle Computer nach dem 30. März 2016 erstellt worden sein. 
> 
> 

1. Melden Sie sich beim [Azure-Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)an.
2. Wählen Sie **Weitere Dienste** und dann in der Liste **DevTest Labs** aus.
3. Wählen Sie in der Liste der Labs das gewünschte Lab aus.  
4. Wählen Sie auf dem Blatt **Übersicht** des Labs den virtuellen Computer aus, aus dem Sie die Formel erstellen möchten.
   
    ![Virtuelle Labs-Computer](./media/devtest-lab-create-formulas/my-vms.png)
5. Wählen Sie auf dem Blatt für den virtuellen Computer die Option **Create formula (reusable base)**(Formel erstellen (wiederverwendbare Basis)) aus.
   
    ![Formel erstellen](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. Geben Sie auf dem Blatt **Create Formula** (Formel erstellen) einen **Namen** und eine **Beschreibung** für die neue Formel ein.
   
    ![Blatt „Formel erstellen“](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Wählen Sie **OK** , um die Formel zu erstellen.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Verwandte Blogbeiträge
* [Custom images or formulas? (Benutzerdefinierte Images oder Formeln?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Nächste Schritte
- [Hinzufügen eines virtuellen Computers zu einem Lab in Azure DevTest Labs](devtest-lab-add-vm.md)
- [Verwalten von Azure DevTest Labs-Formeln](devtest-lab-manage-formulas.md)
