Die virtuellen IaaS-Computer (VMs) und PaaS-Rolleninstanzen in einem virtuellen Netzwerk erhalten automatisch eine private IP-Adresse aus einem von Ihnen angegebenen Bereich, je nach Subnetz, mit dem Sie verbunden sind. Diese Adresse wird von den virtuellen Computern und Rolleninstanzen beibehalten, bis sie außer Betrieb gesetzt werden. Sie setzen einen virtuellen Computer oder eine Rolleninstanz durch Beenden von PowerShell, der Azure-Befehlszeilenschnittstelle oder dem Azure-Portal aus außer Betrieb. Sobald der virtuelle Computer oder die Rolleninstanz erneut gestartet wird, wird in diesen Fällen eine verfügbare IP-Adresse aus der Azure-Infrastruktur bereitgestellt. Möglicherweise ist diese nicht dieselbe wie vorher. Wenn Sie den virtuellen Computer oder die Rolleninstanz aus dem Gastbetriebssystem herunterfahren, behält er die verwendete IP-Adresse bei.  

In bestimmten Fällen sollte ein virtueller Computer oder eine Rolleninstanz eine statische IP-Adresse besitzen, wenn beispielsweise auf Ihrem virtuellen Computer DNS ausgeführt wird oder der virtuelle Computer als Domänencontroller fungieren soll. Dazu können Sie eine statische private IP-Adresse festlegen.



<!--HONumber=Nov16_HO3-->


