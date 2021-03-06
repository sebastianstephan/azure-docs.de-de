---
title: "Kaufen eines benutzerdefinierten Domänennamens für Azure App Service-Web-Apps"
description: "Erfahren Sie, wie Sie einen benutzerdefinierten Domänennamen für eine Web-App in Azure App Service kaufen."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 9c5c0b40d796130d93111545c93bedf86c374fd9


---
# <a name="buy-and-configure-a-custom-domain-name-in-azure-app-service"></a>Kaufen und Konfigurieren eines benutzerdefinierten Domänennamens in Azure App Service
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

Wenn Sie eine Web-App erstellen, weist Azure dieser eine Unterdomäne von "azurewebsites.NET" zu. Wenn Ihre Web-App beispielsweise **contoso** heißt, lautet die URL **contoso.azurewebsites.net**. Darüber hinaus weist Azure eine virtuelle IP-Adresse zu.

Bei einer Produktions-Web-App sollten Sie Benutzern einen benutzerdefinierten Domänennamen anzeigen. In diesem Artikel wird erläutert, wie Sie eine benutzerdefinierte Domäne für [App Service-Web-Apps](http://go.microsoft.com/fwlink/?LinkId=529714) kaufen und konfigurieren. 

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

## <a name="overview"></a>Übersicht
Wenn Sie keinen Domänennamen für Ihre Web-App haben, können Sie diesen im [Azure-Portal](https://portal.azure.com/) auf einfache Weise erwerben. Während des Einkaufsprozesses können Sie festlegen, dass die DNS-Einträge für WWW und die Stammdomäne automatisch Ihrer Web-App zugeordnet werden. Sie können Ihre Domäne auch direkt im Azure-Portal verwalten.

Gehen Sie folgendermaßen vor, um Domänennamen zu erwerben und Ihrer Web-App zuzuweisen.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com/)in Ihrem Browser.
2. Klicken Sie auf der Registerkarte **Web-Apps** auf den Namen der Web-App, wählen Sie **Einstellungen** aus, und wählen Sie anschließend **Benutzerdefinierte Domänen** aus.
   
    ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)
3. Klicken Sie auf dem Blatt **Benutzerdefinierte Domänen** auf **Domänen erwerben**.
   
    ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)
4. Geben Sie auf dem Blatt **Domänen erwerben** im Textfeld den Domänennamen ein, den Sie kaufen möchten, und drücken Sie die EINGABETASTE. Die vorgeschlagenen verfügbaren Domänen werden direkt unter dem Textfeld angezeigt. Wählen Sie die Domäne aus, die Sie kaufen möchten. Sie können auch mehrere Domänen auf einmal kaufen. 
   
   ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)
5. Klicken Sie auf **Kontaktinformationen**, und füllen Sie das Formular mit den Kontaktinformationen für die Domäne aus.
   
   ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-3.png)
   
   > [!NOTE]
   > Es ist sehr wichtig, dass Sie alle erforderlichen Felder so genau wie möglich ausfüllen, insbesondere das Feld für die E-Mail-Adresse. Bei Erwerb der Domäne ohne Datenschutz werden Sie möglicherweise dazu aufgefordert, Ihre E-Mail-Adresse zu überprüfen, bevor die Domäne aktiviert wird. In einigen Fällen führen fehlerhafte Daten in den Kontaktinformationen dazu, dass der Domänenkauf fehlschlägt. 
   > 
   > 
6. Nun stehen folgende Optionen zur Auswahl:
   
    a) "Auto renew", um die Domäne jedes Jahr automatisch zu verlängern
   
    b) „Datenschutz“, um den KOSTENLOS im Kaufpreis enthaltenen Datenschutz zu aktivieren (mit Ausnahme von TLDs, deren Registrierung den Datenschutz nicht unterstützt. Beispiel: .co.in, .co.uk usw.)  
   
    c) "Assign default hostnames", um der aktuellen Web-App Standardhostnamen für WWW und Stammdomäne zuzuweisen 
   
   ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.5.png)
   
   > [!NOTE]
   > Bei Option C werden DNS- und Hostnamenbindungen automatisch für Sie konfiguriert.  Auf diese Weise kann über die benutzerdefinierte Domäne auf die Web-App zugegriffen werden, sobald der Kauf abgeschlossen ist (in einigen Fällen können Verzögerungen bei der DNS-Übertragung auftreten). Falls die Verwaltung der Web-App über Azure Traffic Manager erfolgt, wird keine Option zum Zuweisen der Stammdomäne angezeigt, da A-Einträge nicht mit Traffic Manager funktionieren. Sie können die für eine Web-App erworbenen Domänen/Unterdomänen jederzeit einer anderen Web-App zuweisen und umgekehrt. Weitere Informationen finden Sie in Schritt 8. 
   > 
   > 
7. Klicken Sie auf dem Blatt **Domänen erwerben** auf **Auswählen**. Daraufhin wird das Blatt **Kaufbestätigung** mit den Informationen zum Kauf angezeigt. Wenn Sie den rechtlichen Bedingungen zustimmen und auf **Kaufen** klicken, wird Ihre Bestellung gesendet und Sie können den Einkaufsprozess unter **Benachrichtigung** überwachen. Der Domänenkauf kann einige Minuten dauern. 
   
   ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-4.png)
   
   ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-5.png)
8. Wenn Sie erfolgreich eine Domäne bestellt haben, können Sie die Domäne verwalten und Ihrer Web-App zuweisen. Klicken Sie rechts neben Ihrer Domäne auf **„...“**. Anschließend können Sie entweder **Kauf abbrechen** oder **Domäne verwalten** auswählen. Klicken Sie auf **Domäne verwalten**, damit auf dem Blatt **Domäne verwalten** die **Unterdomäne** an die Web-App gebunden werden kann. Wenn Sie eine **Unterdomäne** an eine andere Web-App binden möchten, führen Sie diesen Schritt aus dem Kontext der entsprechenden Web-App heraus durch. Hier können Sie die Domäne einem Traffic Manager-Endpunkt zuweisen (sofern die Web-App über Traffic Manager verwaltet wird), indem Sie einfach im Dropdownmenü den Traffic Manager-Namen auswählen. Auf diese Weise wird die Domäne/Unterdomäne automatisch allen Web-Apps hinter diesem Traffic Manager-Endpunkt zugewiesen. 
   
    ![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-6.png)
   
   > [!NOTE]
   > Sie können innerhalb von 5 Tagen auf "Cancel purchase" klicken, um den Kauf unter vollständiger Rückerstattung der Kosten zu stornieren. Nach 5 Tagen wird anstelle von "Cancel purchase" eine Option zum Löschen der Domäne angezeigt. Wenn Sie die Domäne löschen, wird diese ohne Erstattung aus dem Abonnement entfernt und wieder als verfügbare Domäne aufgeführt. 
   > 
   > 

Sobald die Konfiguration abgeschlossen ist, wird der benutzerdefinierte Domänenname im Abschnitt **Hostnamenbindungen** Ihrer Web-App aufgeführt.

Jetzt sollten Sie den benutzerdefinierten Domänennamen in Ihren Browser eingeben können und und auf diese Weise erfolgreich zu Ihrer Web-App gelangen.

## <a name="what-happens-to-the-custom-domain-you-bought"></a>Was geschieht mit der benutzerdefinierten Domäne, die Sie gekauft haben?
Die benutzerdefinierte Domäne, die Sie auf dem Blatt **Benutzerdefinierte Domänen und SSL** gekauft haben, ist an das Azure-Abonnement gebunden. Als Azure-Ressource ist diese benutzerdefinierte Domäne getrennt und unabhängig von der App Service-App, für die Sie die Domäne zuerst gekauft haben. Dies bedeutet Folgendes:

* Im Azure-Portal können Sie die benutzerdefinierte Domäne, die Sie gekauft haben, für mehrere App Service-Apps verwenden, und nicht nur für die App, für die Sie die benutzerdefinierte Domäne zuerst gekauft haben. 
* Um alle benutzerdefinierten Domänen, die Sie gekauft haben, im Azure-Abonnement zu verwalten, können Sie das Blatt **Benutzerdefinierte Domänen und SSL** einer *beliebigen* App Service-App in diesem Abonnement aufrufen.
* Sie können jede App Service-App aus dem gleichen Azure-Abonnement einer Unterdomäne innerhalb der benutzerdefinierten Domäne zuweisen.
* Wenn Sie eine App Service-App löschen möchten, können Sie wahlweise darauf verzichten, die benutzerdefinierte Domäne zu löschen, an die sie gebunden ist, wenn Sie sie für andere Apps weiterhin verwenden möchten.

## <a name="if-you-cant-see-the-custom-domain-you-bought"></a>Was ist, wenn die benutzerdefinierte Domäne, die Sie gekauft haben, nicht angezeigt wird?
Wenn Sie die benutzerdefinierte Domäne über das Blatt **Benutzerdefinierte Domänen und SSL** gekauft haben, unter **Verwaltete Domänen** jedoch keine benutzerdefinierte Domäne angezeigt wird, überprüfen Sie Folgendes:

* Die Erstellung der benutzerdefinierten Domäne wurde möglicherweise noch nicht abgeschlossen. Überprüfen Sie die Anzeige der Benachrichtigungsglocke am oberen Rand des Azure-Portals für den Verlauf.
* Die Erstellung der benutzerdefinierten Domäne ist möglicherweise aus irgendeinem Grund fehlgeschlagen. Überprüfen Sie die Anzeige der Benachrichtigungsglocke am oberen Rand des Azure-Portals für den Verlauf.
* Die benutzerdefinierte Domäne wurde möglicherweise erfolgreich erstellt, aber das Blatt möglicherweise noch nicht aktualisiert. Versuchen Sie, das Blatt **Benutzerdefinierte Domänen und SSL** erneut zu öffnen.
* Möglicherweise haben Sie die benutzerdefinierte Domäne zu einem bestimmten Zeitpunkt gelöscht. Überprüfen Sie die Überwachungsprotokolle durch Klicken auf **Einstellungen** > **Überwachungsprotokolle** auf dem Hauptblatt Ihrer App. 
* Das Blatt **Benutzerdefinierte Domänen und SSL**, auf dem Sie suchen, gehört vielleicht zu einer App, die in einem anderen Azure-Abonnement erstellt wurde. Wechseln Sie zu einer anderen App in einem anderen Abonnement, und überprüfen Sie das Blatt **Benutzerdefinierte Domänen und SSL**.  
    Innerhalb des Portals können Sie keine benutzerdefinierten Domänen anzeigen oder verwalten, die in einem anderen Azure-Abonnement erstellt wurden als die App. Wenn Sie jedoch auf dem zu der Domäne gehörenden Blatt **Domäne verwalten** auf **Erweiterte Verwaltung** klicken, werden Sie zur der Website des Domänennamenanbieters weitergeleitet, wo Sie für Apps, die in einem anderen Azure-Abonnement erstellt wurden,   [Ihre benutzerdefinierte Domäne wie alle externen Domänen manuell konfigurieren](web-sites-custom-domain-name.md) 
   können. 




<!--HONumber=Nov16_HO3-->


