---
title: "Zugriff und Sicherheit in Azure-Vorlagen für Windows-VMs | Microsoft-Dokumentation"
description: ".NET Core-Tutorial für virtuelle Azure-Computer"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: nepeters
ms.custom: H1Hack27Feb2017
translationtype: Human Translation
ms.sourcegitcommit: 8eeeef0bb33b5b8ed265532d160829c076190fc4
ms.openlocfilehash: 91c4550f9caadc790d1b6aea8f037e2089ebec3c
ms.lasthandoff: 03/01/2017

---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Zugriff und Sicherheit in Azure Resource Manager-Vorlagen für Windows-VMs

Auf in Azure gehostete Anwendungen muss in der Regel über das Internet oder über eine VPN-/ExpressRoute-Verbindung mit Azure zugegriffen werden. Im Rahmen des Music Store-Anwendungsbeispiels wird die Website im Internet mit einer öffentlichen IP-Adresse verfügbar gemacht. Nach Einrichtung des Zugriffs müssen die Verbindungen mit der Anwendung sowie der Zugriff auf die Ressourcen des virtuellen Computers geschützt werden. Diese Zugriffssicherheit wird mithilfe einer Netzwerksicherheitsgruppe erreicht. 

In diesem Dokument erfahren Sie, wie die Music Store-Anwendung in der Azure Resource Manager-Beispielvorlage geschützt wird. Alle Abhängigkeiten und individuellen Konfigurationen werden hervorgehoben. Stellen Sie am besten vorab eine Instanz der Lösung in Ihrem Azure-Abonnement bereit, und orientieren Sie sich an der Azure Resource Manager-Vorlage. Die vollständige Vorlage finden Sie hier – [Music Store Deployment on Windows (Music Store-Bereitstellung unter Windows)](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Öffentliche IP-Adresse
Eine Azure-Ressource kann mithilfe einer öffentlichen IP-Adressressource öffentlich zugänglich gemacht werden. Eine öffentliche IP-Adresse kann mit einer statischen oder mit einer dynamischen IP-Adresse konfiguriert werden. Dynamische Adressen werden entfernt, wenn der virtuelle Computer beendet und seine Zuordnung aufgehoben wird. Wenn der Computer wieder gestartet wird, erhält er unter Umständen eine andere öffentliche IP-Adresse. Um die Änderung einer IP-Adresse zu verhindern, können Sie eine reservierte IP-Adresse verwenden. 

Eine öffentliche IP-Adresse kann einer Azure Resource Manager-Vorlage mithilfe des Visual Studio-Assistenten zum Hinzufügen neuer Ressourcen oder durch Einfügen von gültigem JSON-Code in eine Vorlage hinzugefügt werden. 

Das entsprechende JSON-Beispiel in der Resource Manager-Vorlage finden Sie [hier](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Eine öffentliche IP-Adresse kann einem virtuellen Netzwerkadapter oder einem Lastenausgleich zugeordnet werden. Da bei der Music Store-Website ein Lastenausgleich mit mehreren virtuellen Computern verwendet wird, ist die öffentliche IP-Adresse in diesem Beispiel mit dem Lastenausgleich verknüpft.

Das entsprechende JSON-Beispiel in der Resource Manager-Vorlage finden Sie [hier](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Hier sehen Sie die öffentliche IP-Adresse im Azure-Portal. Beachten Sie, dass die öffentliche IP-Adresse einem Lastenausgleich (und keinem virtuellen Computer) zugeordnet ist. Module für den Netzwerklastenausgleich werden im nächsten Dokument dieser Reihe behandelt.

![Öffentliche IP-Adresse](./media/virtual-machines-windows-dotnet-core/pubip-win.png)

Weitere Informationen zu öffentlichen Azure-IP-Adressen finden Sie unter [IP-Adressen in Azure](../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Netzwerksicherheitsgruppen (NSG)
Es empfiehlt sich, nach der Einrichtung den Zugriff auf Azure-Ressourcen einzuschränken. Bei virtuellen Azure-Computern wird ein sicherer Zugriff mithilfe einer Netzwerksicherheitsgruppe erreicht. Im Music Store-Anwendungsbeispiel ist mit Ausnahme von Port 80 (HTTP-Zugriff) und Port 3389 (RDP-Zugriff) jeglicher Zugriff auf den virtuellen Computer eingeschränkt. Eine Netzwerksicherheitsgruppe kann einer Azure Resource Manager-Vorlage mithilfe des Visual Studio-Assistenten zum Hinzufügen neuer Ressourcen oder durch Einfügen von gültigem JSON-Code in eine Vorlage hinzugefügt werden.

Das entsprechende JSON-Beispiel in der Resource Manager-Vorlage finden Sie [hier](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

In diesem Beispiel ist die Netzwerksicherheitsgruppe dem in der Virtual Network-Ressource deklarierten Subnetz zugeordnet. 

Das entsprechende JSON-Beispiel in der Resource Manager-Vorlage finden Sie [hier](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

Hier sehen Sie die Netzwerksicherheitsgruppe im Azure-Portal. Eine NSG kann einem Subnetz und/oder einer Netzwerkschnittstelle zugeordnet werden. In diesem Fall ist die NSG einem Subnetz zugeordnet. In dieser Konfiguration gelten die eingehenden Regeln für alle virtuellen Computer, die mit dem Subnetz verbunden sind.

![Netzwerksicherheitsgruppen (NSG)](./media/virtual-machines-windows-dotnet-core/nsg-win.png)

Ausführliche Informationen zu Netzwerksicherheitsgruppen finden Sie unter [Was ist eine Netzwerksicherheitsgruppe (NSG)?](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Nächster Schritt
<hr>

[Schritt 3: Verfügbarkeit und Skalierung in Azure Resource Manager-Vorlagen](virtual-machines-windows-dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)


