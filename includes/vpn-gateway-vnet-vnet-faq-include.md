###<a name="does-azure-charge-for-traffic-between-vnets"></a>Fallen bei Azure Kosten für den Datenverkehr zwischen VNets an?
VNet-zu-VNet-Datenverkehr innerhalb einer Region ist in beiden Richtungen kostenlos. Für regionsübergreifenden VNet-zu-VNet-Datenverkehr in ausgehender Richtung werden Gebühren für ausgehende Datenübertragungen zwischen VNets basierend auf den Quellregionen berechnet. Angaben zu den Preisen finden Sie in der [Preisübersicht](https://azure.microsoft.com/pricing/details/vpn-gateway/).

###<a name="does-vnet-to-vnet-traffic-travel-across-the-internet"></a>Wird VNet-zu-VNet-Datenverkehr über das Internet übertragen?
Nein. VNet-zu-VNet-Datenverkehr wird über den Microsoft Azure-Backbone übertragen, nicht über das Internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Ist VNet-zu-VNet-Datenverkehr sicher?
Ja, er wird mittels IPsec-/IKE-Verschlüsselung geschützt.

###<a name="do-i-need-a-vpn-device-to-connect-vnets-together"></a>Benötige ich ein VPN-Gerät, umVNets miteinander zu verbinden?
Nein. Für das Verbinden mehrerer virtueller Azure-Netzwerke sind keine VPN-Geräte erforderlich. Diese werden nur benötigt, wenn standortübergreifende Konnektivität erforderlich ist.

###<a name="do-my-vnets-need-to-be-in-the-same-region"></a>Müssen sich meine VNets in der gleichen Region befinden?
Nein. Die virtuellen Netzwerke können sich in der gleichen Azure-Region oder in verschiedenen Azure-Regionen (Standorte) befinden.

###<a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Kann ich VNet-zu-VNet zusammen mit Verbindungen mit mehreren Standorten verwenden?
Ja. Virtuelle Netzwerkverbindungen können simultan mit VPNs mit mehreren Standorten verwendet werden.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>Mit wie vielen lokalen Standorten und virtuellen Netzwerken kann ein virtuelles Netzwerk verbunden werden?
Informationen dazu finden Sie in der Tabelle mit [Gatewayanforderungen](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

###<a name="can-i-use-vnet-to-vnet-to-connect-vms-or-cloud-services-outside-of-a-vnet"></a>Kann ich VNet-zu-VNet für die Verbindung von virtuellen Computern oder Clouddiensten außerhalb eines VNet verwenden?
Nein. VNet-zu-VNet unterstützt das Verbinden virtueller Netzwerke. Nicht unterstützt hingegen werden Verbindungen virtueller Computer oder Clouddienste, die sich nicht in einem virtuellen Netzwerk befinden.

###<a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Kann sich ein Clouddienst oder eine Lastenausgleichs-Endpunkt über mehrere VNets erstrecken?
Nein. Ein Clouddienst oder Endpunkt mit Lastenausgleich darf auch dann nicht mehrere virtuelle Netzwerke umfassen, wenn diese verbunden sind.

###<a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Kann ich den VPN-Typ „PolicyBased“ für VNet-zu-VNet oder standortübergreifende Verbindungen verwenden?
Nein. VNet-zu-VNet- und standortübergreifende Verbindungen erfordern Azure-VPN Gateways mit routenbasierten VPN-Typen (früher als „dynamisches Routing“ bezeichnet).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a>Kann ich ein VNet mit einem routenbasierten VPN-Typ (RouteBased) mit einem anderen VNet mit einem richtlinienbasierten VPN (PolicyBased) verbinden?
Nein. Beide virtuellen Netzwerke müssen routenbasierte VPNs (früher als „dynamisches Routing“ bezeichnet) verwenden.

###<a name="do-vpn-tunnels-share-bandwidth"></a>Verwenden VPN-Tunnel Bandbreite gemeinsam?
Ja. Alle VPN-Tunnel des virtuellen Netzwerks verwenden die verfügbare Bandbreite auf dem Azure-VPN-Gateway und die gleiche SLA für die Verfügbarkeit des VPN-Gateways in Azure gemeinsam.

###<a name="are-redundant-tunnels-supported"></a>Werden redundante Tunnel unterstützt?
Redundante Tunnel zwischen einem Paar virtueller Netzwerke werden unterstützt, wenn ein virtuelles Netzwerkgateway als „Aktiv-Aktiv“ konfiguriert ist.

###<a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Kann ich für VNet-zu-VNet-Konfigurationen Adressräume verwenden, die sich überschneiden?
Nein. IP-Adressbereiche dürfen sich nicht überschneiden.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Dürfen sich die Adressräume der verbundenen virtuellen Netzwerke und der lokalen Standorte überschneiden?
Nein. IP-Adressbereiche dürfen sich nicht überschneiden.





<!--HONumber=Feb17_HO3-->


