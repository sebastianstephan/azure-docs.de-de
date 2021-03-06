---
title: "Verwenden der PM2-Konfiguration für Node.js in Web-Apps unter Linux | Microsoft-Dokumentation"
description: "Verwenden der PM2-Konfiguration für Node.js in Web-Apps unter Linux"
keywords: Azure App Service, Web-App, Nodejs, PM2, Linux, OSS
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
translationtype: Human Translation
ms.sourcegitcommit: bb4c7ea7adfe1326ae8259782b5de2762c8c2bf5
ms.openlocfilehash: c4af07e79ae066f916c15aa239cb5dfdd3fef2a8
ms.lasthandoff: 02/17/2017


---
# <a name="use-pm2-configuration-for-nodejs-in-web-apps-on-linux"></a>Verwenden der PM2-Konfiguration für Node.js in Web-Apps unter Linux
Wenn Sie für Web-Apps unter Linux als Anwendungsstapel „Node.js“ festlegen, haben Sie die Option, eine Node.js-Startdatei anzugeben, wie in der folgenden Abbildung gezeigt:

![Festlegen einer Node.js-Startdatei][1]

Mithilfe dieser Option können Sie eine der folgenden Aufgaben ausführen:

* Angeben des Startskripts für Ihre Node.js-App (Beispiel: /bin/server.js)
* Angeben der PM2-Konfigurationsdatei, die für Ihre Node.js-App verwendet werden soll (Beispiel: /foo/process.json)
  
  > [!NOTE]
  > Verwenden Sie die PM2-Konfiguration, wenn die Node.js-Prozesse bei der Änderung bestimmter Dateien automatisch neu gestartet werden sollen. Andernfalls wird Ihre Anwendung nicht neu gestartet, wenn sie Änderungsbenachrichtigungen erhält (beispielsweise bei Änderungen des Anwendungscodes).
  > 
  > 

Die [Dokumentation zur Prozessdatei](http://pm2.keymetrics.io/docs/usage/application-declaration/) für Node.js enthält alle Optionen. Nachfolgend ist jedoch ein Beispiel für eine Konfiguration aufgeführt, die Sie in Ihrer Datei „process.json“ verwenden können:

        {
          "name"        : "worker",
          "script"      : "/bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["/bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

Wichtige Hinweise zu dieser Konfiguration:

* Die Eigenschaft „script“ gibt das Startskript Ihrer Anwendung an.
* Die Eigenschaft „instances“ gibt an, wie viele Instanzen des Knotenprozesses gestartet werden sollen. Wenn Ihre Anwendung auf größeren virtuellen Computern mit mehreren Kernen ausgeführt wird, wird empfohlen, die Ressourcen zu maximieren, indem Sie hier einen höheren Wert angeben.
* Das Array „watch“ gibt alle Dateien an, für die der Knotenprozess bei einer Änderung neu gestartet werden soll.
* Bei „watch_options“ müssen Sie aufgrund der Bereitstellung des Anwendungsinhalts für „usePolling“ derzeit „true“ angeben.

## <a name="next-steps"></a>Nächste Schritte
* [Was ist App Service unter Linux?](app-service-linux-intro.md)
* [Häufig gestellte Fragen zu Azure App Service-Web-Apps unter Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png

