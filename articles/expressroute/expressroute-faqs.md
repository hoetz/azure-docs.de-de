---
title: Häufig gestellte Fragen zu Azure ExpressRoute | Microsoft-Dokumentation
description: Die FAQs zu ExpressRoute enthalten Informationen zu unterstützten Azure-Diensten, Kosten, Daten und Verbindungen, SLAs, Anbietern und Standorten, Bandbreite sowie zusätzliche technische Details.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: ''
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2018
ms.author: cherylmc
ms.openlocfilehash: 557c6a75140f399f74d77543de834af086871032
ms.sourcegitcommit: 20d103fb8658b29b48115782fe01f76239b240aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="expressroute-faq"></a>ExpressRoute – FAQ

## <a name="what-is-expressroute"></a>Was ist ExpressRoute?

ExpressRoute ist ein Azure-Dienst, der es Ihnen ermöglicht, private Verbindungen zwischen Microsoft-Datencentern und der Infrastruktur bei Ihnen vor Ort oder in einer Kollokationsumgebung zu erstellen. ExpressRoute-Verbindungen erfolgen nicht über das öffentliche Internet und bieten eine höhere Sicherheit, größere Zuverlässigkeit und schnellere Geschwindigkeit bei weniger Latenz als herkömmliche Verbindungen über das Internet.

### <a name="what-are-the-benefits-of-using-expressroute-and-private-network-connections"></a>Was sind die Vorteile von ExpressRoute und privaten Netzwerkverbindungen?

ExpressRoute-Verbindungen verlaufen nicht über das öffentliche Internet. Sie bieten eine höhere Sicherheit, größere Zuverlässigkeit und höhere Geschwindigkeiten bei konstanter Latenz als herkömmliche Verbindungen über das Internet. In einigen Fällen können durch die Verwendung von ExpressRoute-Verbindungen zum Übertragen von Daten zwischen lokalen Geräten und Azure auch drastische Kosteneinsparungen erzielt werden.

### <a name="where-is-the-service-available"></a>Wo ist der Dienst verfügbar?

Auf der folgenden Seite finden Sie Informationen bezüglich der Dienststandorte und Verfügbarkeit: [ExpressRoute-Partner und -Standorte](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-to-connect-to-microsoft-if-i-dont-have-partnerships-with-one-of-the-expressroute-carrier-partners"></a>Wie kann ich ExpressRoute verwenden, um eine Verbindung mit Microsoft herzustellen, wenn ich keine Partnerschaft mit einem der ExpressRoute-Anbieterpartner habe?

Sie können einen regionalen Netzbetreiber auswählen und Ethernetverbindungen mit einem der unterstützten Exchange-Anbieterstandorte herstellen. Am Anbieterstandort können Sie dann eine Peeringverbindung mit Microsoft herstellen. Überprüfen Sie den letzten Abschnitt von [ExpressRoute-Partner und -Standorte](expressroute-locations.md) , um herauszufinden, ob Ihr Dienstanbieter an einem der Exchange-Standorte vorhanden ist. Sie können dann eine ExpressRoute-Verbindung über den Dienstanbieter anfordern, um eine Verbindung mit Azure herzustellen.

### <a name="how-much-does-expressroute-cost"></a>Wie viel kostet ExpressRoute?

Preisinformationen finden Sie in der [Preisübersicht](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-the-vpn-connection-i-purchase-from-my-network-service-provider-have-to-be-the-same-speed"></a>Wenn ich für eine ExpressRoute-Verbindung mit einer bestimmten Bandbreite bezahle, muss die VPN-Verbindung, die ich von meinem Netzwerkdienstanbieter erworben habe, die gleiche Geschwindigkeit haben?

Nein. Sie können eine VPN-Verbindung beliebiger Geschwindigkeit bei Ihrem Dienstanbieter erwerben. Die Verbindung mit Azure ist jedoch auf die von Ihnen erworbene Bandbreite der ExpressRoute-Verbindung begrenzt.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-the-ability-to-burst-up-to-higher-speeds-if-necessary"></a>Wenn ich für eine ExpressRoute-Verbindung mit einer bestimmten Bandbreite bezahle, habe ich die Möglichkeit, bei Bedarf höhere Geschwindigkeiten zu nutzen?

Ja. ExpressRoute-Verbindungen sind so konfiguriert, dass Sie das erworbene Bandbreitenlimit um das Doppelte überschreiten können, ohne dass zusätzliche Kosten anfallen. Fragen Sie bei Ihrem Dienstanbieter an, ob er diese Funktion unterstützt.

### <a name="can-i-use-the-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>Kann ich dieselbe private Netzwerkverbindung gleichzeitig mit virtuellen Netzwerken und anderen Azure-Diensten verwenden?

Ja. Sobald eine ExpressRoute-Verbindung eingerichtet ist, können Sie gleichzeitig auf Dienste in einem virtuellen Netzwerk und in anderen Azure-Diensten zugreifen. Über einen privaten Peeringpfad können Sie eine Verbindung mit virtuellen Netzwerken herstellen, und über den öffentlichen Peeringpfad stellen Sie die Verbindung mit anderen Diensten her.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>Bietet ExpressRoute eine Service Level Agreement (SLA)?

Weitere Informationen finden Sie auf der Seite [ExpressRoute – SLA](https://azure.microsoft.com/support/legal/sla/).

## <a name="supported-services"></a>Unterstützte Dienste

ExpressRoute unterstützt [drei Routingdomänen](expressroute-circuit-peerings.md) für verschiedene Arten von Diensten.

### <a name="private-peering"></a>Privates Peering

* Virtuelle Netzwerke, einschließlich aller virtuellen Computer und Clouddienste

### <a name="public-peering"></a>Öffentliches Peering

* Power BI
* Dynamics 365 for Finance and Operations (früher als „Dynamics AX Online“ bekannt)
* Die meisten Azure-Dienste werden unterstützt. Überprüfen Sie dies direkt für den Dienst, den Sie verwenden möchten.<br>
  Die folgenden Dienste werden NICHT unterstützt:
    * CDN
    * Visual Studio Team Services-Auslastungstests
    * Multi-Factor Authentication
    * Traffic Manager

### <a name="microsoft-peering"></a>Microsoft-Peering

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Dynamics 365 for Customer Engagement-Anwendungen (früher als „CRM Online“ bekannt)
  * Dynamics 365 for Sales
  * Dynamics 365 for Customer Service
  * Dynamics 365 for Field Service
  * Dynamics 365 for Project Service
* Mit [Routenfiltern](#route-filters-for-microsoft-peering) erhalten Sie Zugriff auf die gleichen öffentlichen Dienste mit Microsoft-Peering:
  * Power BI
  * Dynamics 365 for Finance and Operations
  * Die meisten Azure-Dienste werden unterstützt. Überprüfen Sie dies direkt für den Dienst, den Sie verwenden möchten.<br>
  Die folgenden Dienste werden NICHT unterstützt:
    * CDN
    * Visual Studio Team Services-Auslastungstests
    * Multi-Factor Authentication
    * Traffic Manager

## <a name="data-and-connections"></a>Daten und Verbindungen

### <a name="are-there-limits-on-the-amount-of-data-that-i-can-transfer-using-expressroute"></a>Gibt es Limits hinsichtlich der Datenmenge, die ich mithilfe von ExpressRoute übertragen kann?

Wir haben keine Limits hinsichtlich der übertragenen Datenmenge festgelegt. In der [Preisübersicht](https://azure.microsoft.com/pricing/details/expressroute/) finden Sie Informationen zu Bandbreitentarifen.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Welche Verbindungsgeschwindigkeiten werden von ExpressRoute unterstützt?

Unterstützte Bandbreiten:

50 MBit/s, 100 MBit/s, 200 MBit/s, 500 MBit/s, 1 GBit/s, 2 GBit/s, 5 GBit/s, 10 GBit/s

### <a name="which-service-providers-are-available"></a>Welche Dienstanbieter sind verfügbar?

Eine Liste der Dienstanbieter und Standorte finden Sie unter [ExpressRoute-Partner und -Standorte](expressroute-locations.md) .

## <a name="technical-details"></a>Technische Details

### <a name="what-are-the-technical-requirements-for-connecting-my-on-premises-location-to-azure"></a>Was sind die technischen Voraussetzungen für die Verbindung meines lokalen Standorts mit Azure?

Die Voraussetzungen finden Sie auf der Seite [ExpressRoute-Voraussetzungen](expressroute-prerequisites.md).

### <a name="are-connections-to-expressroute-redundant"></a>Sind Verbindungen mit ExpressRoute redundant?

Ja. Jede ExpressRoute-Verbindung verfügt über ein redundantes Paar von Querverbindungen mit Hochverfügbarkeit.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Geht die Konnektivität verloren, wenn einer meiner ExpressRoute-Links ausfällt?

Wenn eine der Querverbindungen ausfällt, bleibt die Konnektivität bestehen. Es steht eine redundante Verbindung zur Verfügung, um die Last des Netzwerks zu bewältigen und die Hochverfügbarkeit Ihrer ExpressRoute-Verbindung zu gewährleisten. Sie können zudem eine Verbindung an einem anderen Peeringstandort erstellen, um Resilienz auf der Verbindungsebene zu erreichen.

### <a name="how-do-i-ensure-high-availability-on-a-virtual-network-connected-to-expressroute"></a>Wie stelle ich Hochverfügbarkeit in einem mit ExpressRoute verbundenen virtuellen Netzwerk sicher?

Hochverfügbarkeit erreichen Sie, indem Sie ExpressRoute-Verbindungen an verschiedenen Peeringstandorten (beispielsweise Singapur, Singapur2) mit Ihrem virtuellen Netzwerk verbinden. Sollte eine ExpressRoute-Verbindung ausfallen, erfolgt ein Failover auf eine andere ExpressRoute-Verbindung. Standardmäßig wird Datenverkehr, der Ihr virtuelles Netzwerk verlässt, auf der Grundlage von ECMP (Equal Cost Multi-path Routing) weitergeleitet. Mit der Verbindungsgewichtung können Sie einer Verbindung den Vorzug geben. Weitere Details zur Verbindungsgewichtung finden Sie unter [Optimieren von ExpressRoute-Routing](expressroute-optimize-routing.md).

### <a name="onep2plink"></a>Wenn ich mich nicht am selben Standort wie ein Cloud Exchange befinde und mein Dienstanbieter Punkt-zu-Punkt-Verbindungen bereitstellt, muss ich zwei physische Verbindungen zwischen meinem lokalen Netzwerk und Microsoft anfordern?

Wenn Ihr Dienstanbieter zwei virtuelle Ethernetverbindungen über die physische Verbindung herstellen kann, benötigen Sie nur eine einzige physische Verbindung. Die physische Verbindung (z.B. Glasfaser) wird auf einem Layer 1-Gerät (L1) beendet (siehe Abbildung). Die zwei virtuellen Ethernet-Verbindungen werden mit unterschiedlichen VLAN-IDs markiert, eine für die primäre Verbindung und eine für die sekundäre Verbindung. Diese VLAN-IDs befinden sich im äußeren 802.1Q-Ethernet-Header. Der innere 802.1Q-Ethernet-Header (nicht dargestellt) wird einer bestimmten [ExpressRoute-Routingdomäne](expressroute-circuit-peerings.md) zugeordnet.

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-to-azure-using-expressroute"></a>Kann ich eines meiner VLANs mithilfe von ExpressRoute auf Azure erweitern?

Nein. Wir unterstützen keine Schicht-2-Konnektivitätserweiterungen in Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Kann mein Abonnement mehr als eine ExpressRoute-Verbindung umfassen?

Ja. Ihr Abonnement kann mehr als eine ExpressRoute-Verbindung enthalten. Standardmäßig sind nicht mehr als 10 zulässig. Wenden Sie sich an den Microsoft-Support, um das Limit bei Bedarf zu erhöhen.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Kann ich ExpressRoute-Verbindungen von verschiedenen Dienstanbietern haben?

Ja. Sie können ExpressRoute-Verbindungen von verschiedenen Dienstanbietern verwenden. Jede ExpressRoute-Verbindung ist nur einem Dienstanbieter zugeordnet. 

### <a name="i-see-two-expressroute-peering-locations-in-the-same-metro-eg-singapore-and-singapore2-which-peering-location-should-i-choose-to-create-my-expressroute-circuit"></a>Mir werden zwei ExpressRoute-Peeringstandorte in der gleichen Metro angezeigt (beispielweise Singapur und Singapur2). Welchen Peeringstandort sollte ich für die Erstellung meiner ExpressRoute-Verbindung verwenden?
Falls Ihr Dienstanbieter ExpressRoute an beiden Standorten anbietet, können Sie sich bei der Einrichtung von ExpressRoute in Abstimmung mit Ihrem Anbieter für einen beliebigen der beiden Standorte entscheiden. 

### <a name="can-i-have-multiple-expressroute-circuits-in-the-same-metro-can-i-link-them-to-the-same-virtual-network"></a>Kann ich über mehrere ExpressRoute-Verbindungen am gleichen Standort verfügen? Kann ich sie mit dem gleichen virtuellen Netzwerk verknüpfen?

Ja. Sie können über mehrere ExpressRoute-Verbindungen bei den gleichen oder unterschiedlichen Dienstanbietern verfügen. Wenn der Standort über mehrere ExpressRoute-Peeringstandorte verfügt und die Verbindungen an verschiedenen Peeringstandorten erstellt werden, können Sie sie mit dem gleichen virtuellen Netzwerk verknüpfen. Wenn die Verbindungen am gleichen Peeringstandort erstellt werden, können sie nicht mit dem gleichen virtuellen Netzwerk verknüpft werden.

### <a name="how-do-i-connect-my-virtual-networks-to-an-expressroute-circuit"></a>Wie kann ich meine Virtual Networks mit einer ExpressRoute-Verbindung verbinden?

Die grundlegenden Schritte lauten wie folgt:

* Stellen Sie eine ExpressRoute-Verbindung her, und lassen Sie sie vom Dienstanbieter aktivieren.
* Die BGP-Peerings müssen von Ihnen oder vom Anbieter konfiguriert werden.
* Verknüpfen Sie das virtuelle Netzwerk mit der ExpressRoute-Verbindung.

Weitere Informationen finden Sie unter [ExpressRoute-Workflows für die Verbindungsbereitstellung und Verbindungszustände](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Gibt es Konnektivitätsgrenzen für meine ExpressRoute-Verbindung?

Ja. Der Artikel [ExpressRoute-Partner und -Standorte](expressroute-locations.md) bietet eine Übersicht über die Konnektivitätsgrenzen für eine ExpressRoute-Verbindung. Die Konnektivität für eine ExpressRoute-Verbindung ist auf eine einzelne geopolitische Region beschränkt. Die Konnektivität kann auf verschiedene geopolitische Regionen erweitert werden, wenn Sie das ExpressRoute Premium-Feature aktivieren.

### <a name="can-i-link-to-more-than-one-virtual-network-to-an-expressroute-circuit"></a>Kann ich mehr als ein virtuelles Netzwerk mit einer ExpressRoute-Verbindung verknüpfen?

Ja. Bei einer standardmäßigen ExpressRoute-Verbindung sind bis zu 10 Verbindungen mit virtuellen Netzwerken möglich. Bei einer [ExpressRoute Premium-Verbindung](#expressroute-premium) sind es bis zu 100. 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-to-a-single-expressroute-circuit"></a>Ich habe mehrere Azure-Abonnements, die Virtual Networks enthalten. Kann ich Virtual Networks, die sich in unterschiedlichen Abonnements befinden, mit einer ExpressRoute-Verbindung verbinden?

Ja. Sie können bis zu 10 andere Azure-Abonnements autorisieren, eine einzige ExpressRoute-Verbindung zu verwenden. Dieses Limit kann durch das Aktivieren des ExpressRoute Premium-Features erhöht werden.

Weitere Informationen finden Sie unter [Freigeben einer ExpressRoute-Verbindung für mehrere Abonnements](expressroute-howto-linkvnet-arm.md).

### <a name="i-have-multiple-azure-subscriptions-associated-to-different-azure-active-directory-tenants-or-enterprise-agreement-enrollments-can-i-connect-virtual-networks-that-are-in-separate-tenants-and-enrollments-to-a-single-expressroute-circuit-not-in-the-same-tenant-or-enrollment"></a>Ich verfüge über mehrere Azure-Abonnements, die unterschiedlichen Azure Active Directory-Mandanten oder Enterprise Agreement-Registrierungen zugeordnet sind. Kann ich virtuelle Netzwerke in separaten Mandanten und Registrierungen mit einer einzelnen ExpressRoute-Verbindung verbinden, die sich nicht im gleichen Mandanten bzw. nicht in der gleichen Registrierung befindet?

Ja. ExpressRoute-Autorisierungen können ohne zusätzliche Konfigurationsschritte über die Grenzen von Abonnements, Mandanten und Registrierungen hinweg verwendet werden. 

Weitere Informationen finden Sie unter [Freigeben einer ExpressRoute-Verbindung für mehrere Abonnements](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-to-the-same-circuit-isolated-from-each-other"></a>Sind virtuelle Netzwerke, die mit der gleichen Verbindung verbunden sind, voneinander isoliert?

Nr. Aus Routingsicht sind alle virtuellen Netzwerke, die mit derselben ExpressRoute-Verbindung verknüpft sind, Teil derselben Routingdomäne und nicht voneinander isoliert. Wenn Sie eine Isolierung der Routen benötigen, müssen Sie zuerst eine separate ExpressRoute-Verbindung erstellen.

### <a name="can-i-have-one-virtual-network-connected-to-more-than-one-expressroute-circuit"></a>Kann mehr als ein virtuelles Netzwerk mit mehr als einer ExpressRoute-Verbindung verbunden sein?

Ja. Sie können ein einzelnes virtuelles Netzwerk mit bis zu vier ExpressRoute-Verbindungen verknüpfen. Sie müssen über vier unterschiedliche [ExpressRoute-Standorte](expressroute-locations.md) angefordert werden.

### <a name="can-i-access-the-internet-from-my-virtual-networks-connected-to-expressroute-circuits"></a>Kann ich von meinen virtuellen Netzwerken aus, die mit ExpressRoute-Verbindungen verbunden sind, ins Internet gehen?

Ja. Wenn Sie über die BGP-Sitzung keine Standardrouten (0.0.0.0/0) oder Internetroutenpräfixe angekündigt haben, können Sie von einem virtuellen Netzwerk aus, das mit einer ExpressRoute-Verbindung verknüpft ist, eine Internetverbindung herstellen.

### <a name="can-i-block-internet-connectivity-to-virtual-networks-connected-to-expressroute-circuits"></a>Kann ich die Internetkonnektivität für virtuelle Netzwerke blockieren, die mit ExpressRoute-Verbindungen verbunden sind?

Ja. Sie können Standardrouten (0.0.0.0/0) ankündigen, um die Internetkonnektivität von virtuellen Computern in einem virtuellen Netzwerk zu blockieren und den gesamten Datenverkehr über die ExpressRoute-Verbindung zu leiten.

Wenn Sie keine Standardrouten ankündigen, wird der Datenverkehr an Dienste, die über öffentliches Peering (z.B. Azure Storage und SQL-Datenbank) angeboten werden, wieder an Ihren Standort zurückgeleitet. Sie müssen Ihre Router so konfigurieren, dass der Datenverkehr über den öffentlichen Peeringpfad oder über das Internet an Azure zurückgegeben wird. Wenn Sie einen Dienstendpunkt (Vorschauversion) für den Dienst aktiviert haben, wird keine Weiterleitung des für den Dienst bestimmten Datenverkehrs an Ihren lokalen Standort erzwungen. Der Datenverkehr bleibt innerhalb des Azure-Backbonenetzwerks. Weitere Informationen zu Dienstendpunkten finden Sie unter [Dienstendpunkte von virtuellen Netzwerken (Vorschauversion)](../virtual-network/virtual-network-service-endpoints-overview.md?toc=%2fazure%2fexpressroute%2ftoc.json).

### <a name="can-virtual-networks-linked-to-the-same-expressroute-circuit-talk-to-each-other"></a>Können virtuelle Netzwerke mit der gleichen ExpressRoute-Verbindung verknüpft sein und miteinander kommunizieren?

Ja. Virtuelle Maschinen in virtuellen Netzwerken, die mit der gleichen ExpressRoute-Verbindung verbunden sind, können miteinander kommunizieren.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>Kann ich für Virtual Networks Standort-zu-Standort-Konnektivität zusammen mit ExpressRoute verwenden?

Ja. ExpressRoute kann zusammen mit Standort-zu-Standort-VPNs verwendet werden.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-to-use-expressroute"></a>Kann ich ein virtuelles Netzwerk mit einer Standort-zu-Standort-/Punkt-zu-Standort-Konfiguration so konfigurieren, dass es ExpressRoute verwendet?

Ja. Sie müssen in Ihrem virtuellen Netzwerk ein ExpressRoute-Gateway erstellen. Bei diesem Vorgang kommt es zu einer kurzen Dienstunterbrechung.

### <a name="why-is-there-a-public-ip-address-associated-with-the-expressroute-gateway-on-a-virtual-network"></a>Weshalb ist dem ExpressRoute-Gateway in einem virtuellen Netzwerk eine öffentliche IP-Adresse zugeordnet?

Die öffentliche IP-Adresse wird nur zur internen Verwaltung benötigt und stellt für Ihr virtuelles Netzwerk kein Sicherheitsrisiko dar.

### <a name="what-do-i-need-to-connect-to-azure-storage-over-expressroute"></a>Was brauche ich, um über ExpressRoute eine Verbindung mit Azure Storage herzustellen?

Sie müssen eine ExpressRoute-Verbindung einrichten und Routen für öffentliches Peering konfigurieren.

### <a name="are-there-limits-on-the-number-of-routes-i-can-advertise"></a>Gibt es Limits hinsichtlich der Anzahl von Routen, die ich ankündigen kann?

Ja. Wir akzeptieren bis zu 4.000 Routenpräfixe für privates Peering und je 200 für öffentliches Peering und Microsoft-Peering. Sie können diesen Wert auf 10.000 Routen für privates Peering erhöhen, wenn Sie für ExpressRoute das Premium-Feature aktivieren.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-the-bgp-session"></a>Gibt es Einschränkungen hinsichtlich der IP-Adressbereiche, die ich über die BGP-Sitzung ankündigen kann?

Wir akzeptieren keine privaten Präfixe (RFC1918) in der öffentlichen und Microsoft-BGP-Peeringsitzung.

### <a name="what-happens-if-i-exceed-the-bgp-limits"></a>Was geschieht, wenn ich die BGP-Limits überschreite?

BGP-Sitzungen werden abgebrochen. Sie werden zurückgesetzt, sobald die Präfixanzahl unter das Limit fällt.

### <a name="what-is-the-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Wie lang ist die BGP-Haltezeit für ExpressRoute? Kann sie angepasst werden?

Die Haltezeit ist 180. Die Keep-Alive-Nachrichten werden alle 60 Sekunden gesendet. Diese Einstellungen werden auf Microsoft-Seite festgelegt und können nicht geändert werden. Sie haben die Möglichkeit, verschiedene Zeitgeber zu konfigurieren. Die BGP-Sitzungsparameter werden daraufhin entsprechend ausgehandelt.

### <a name="after-i-advertise-the-default-route-00000-to-my-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-to-i-fix-this"></a>Nachdem ich die Standardroute (0.0.0.0/0) für meine Virtual Networks angekündigt habe, kann ich Windows, das auf meinen Azure-VMs ausgeführt wird, nicht mehr aktivieren. Wie kann ich dieses Problem beheben?

Die folgenden Schritte helfen Azure dabei, die Aktivierungsanforderung zu erkennen:

1. Richten Sie für die ExpressRoute-Verbindung öffentliches Peering ein.
2. Führen Sie ein DNS-Lookup durch, und suchen Sie die IP-Adresse von **kms.core.windows.net**
3. Der Schlüsselverwaltungsdienst muss erkennen, dass die Aktivierungsanforderung von Azure stammt, und die Anforderung bedienen. Führen Sie eine der folgenden drei Aufgaben durch:

   * Leiten Sie in Ihrem lokalen Netzwerk den Datenverkehr für die IP-Adresse, die Sie in Schritt 2 abgerufen haben, über das öffentliche Peering zurück an Azure.
   * Fordern Sie Ihren Netzwerkdienstanbieter auf, den Datenverkehr über das öffentliche Peering wieder an Azure zurückzuleiten.
   * Erstellen Sie eine benutzerdefinierte Route, die auf diese IP-Adresse verweist und als nächsten Hop das Internet hat, und wenden Sie sie auf die Subnetze an, in denen sich diese virtuellen Computer befinden.

### <a name="can-i-change-the-bandwidth-of-an-expressroute-circuit"></a>Kann ich die Bandbreite einer ExpressRoute-Verbindung ändern?

Ja, Sie können versuchen, die Bandbreite Ihrer ExpressRoute-Verbindung im Azure-Portal oder mithilfe von PowerShell zu erhöhen. Wenn auf dem physischen Port, auf dem die Verbindung erstellt wurde, Kapazität verfügbar ist, ist die Änderung erfolgreich. 

Wenn bei der Änderung ein Fehler auftritt, bedeutet dies, dass die Kapazität auf dem aktuellen Port nicht ausreicht und dass Sie eine neue ExpressRoute-Verbindung mit der höheren Bandbreite erstellen müssen. Es kann aber auch bedeuten, dass an dem Standort keine zusätzliche Kapazität verfügbar ist. In dem Fall können Sie die Bandbreite nicht erhöhen. 

Wenden Sie sich auch an Ihren Konnektivitätsanbieter, um sicherzustellen, dass er die Drosselungen in seinen Netzwerken aktualisiert, damit die Erhöhung der Bandbreite unterstützt wird. Sie können Bandbreite Ihrer ExpressRoute-Verbindung jedoch nicht verringern. Stattdessen müssen Sie eine neue ExpressRoute-Verbindung mit der geringeren Bandbreite erstellen und die alte Verbindung löschen.

### <a name="how-do-i-change-the-bandwidth-of-an-expressroute-circuit"></a>Wie kann ich die Bandbreite einer ExpressRoute-Verbindung ändern?

Sie können die Bandbreite der ExpressRoute-Verbindung mithilfe der REST-API oder des PowerShell-Cmdlets aktualisieren.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>Was ist ExpressRoute Premium?

ExpressRoute Premium ist eine Sammlung der folgenden Features:

* Erhöhung des Grenzwerts für Routingtabellen von 4.000 auf 10.000 Routen für privates Peering.
* Größere Anzahl an VNets, die mit der ExpressRoute-Verbindung verbunden werden können. Weitere Informationen finden Sie in der Tabelle [ExpressRoute-Grenzwerte](#limits).
* Verbindung mit Office 365 und Dynamics 365
* Globale Konnektivität über das Microsoft-Kernnetzwerk. Jetzt können Sie ein VNET in einer geopolitischen Region mit einer ExpressRoute-Verbindung in einer anderen Region verknüpfen.<br>
    **Beispiele:**

    *  Sie können ein in „Europa, Westen“ erstelltes VNET mit einer ExpressRoute-Verbindung verknüpfen, die in Silicon Valley erstellt wurde. 
    *  Beim öffentlichen Peering werden Präfixe anderer geopolitischer Regionen so angekündigt, dass Sie sich z.B. von einer Verbindung im Silicon Valley ausgehend mit SQL Azure in der Region „Europa, Westen“ verbinden können.


### <a name="limits"></a>Wie viele VNETs kann ich mit einer ExpressRoute-Verbindung verknüpfen, wenn ich ExpressRoute Premium aktiviert habe?

Die folgenden Tabellen enthalten die ExpressRoute-Grenzwerte und die Anzahl von VNETs pro ExpressRoute-Verbindung:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Wie aktiviere ich ExpressRoute Premium?

Die Features von ExpressRoute Premium können aktiviert werden, sobald Sie das Feature selbst aktiviert haben. Durch Aktualisieren des Verbindungszustand können sie beendet werden. Sie können ExpressRoute Premium zum Zeitpunkt der Verbindungserstellung aktivieren, oder Sie können die REST-API oder das PowerShell-Cmdlet aufrufen.

### <a name="how-do-i-disable-expressroute-premium"></a>Wie deaktiviere ich ExpressRoute Premium?

Sie können ExpressRoute Premium deaktivieren, indem Sie die REST-API oder das PowerShell-Cmdlet aufrufen. Stellen Sie sicher, dass Sie eine Skalierung gemäß Ihrer Konnektivitätsanforderungen durchgeführt haben, um die Standardgrenzwerte einzuhalten, bevor Sie ExpressRoute Premium deaktivieren. Wenn Ihre Nutzung über den Standardgrenzwerten liegt, tritt bei der Anforderung zur Deaktivierung von ExpressRoute Premium ein Fehler auf.

### <a name="can-i-pick-and-choose-the-features-i-want-from-the-premium-feature-set"></a>Kann ich die Features der Premium-Features auswählen, die ich nutzen möchte?

Nein. Sie können die Features nicht auswählen. Wenn Sie ExpressRoute Premium aktivieren, werden alle Features aktiviert.

### <a name="how-much-does-expressroute-premium-cost"></a>Wie viel kostet ExpressRoute Premium?

Angaben zu den Preisen finden Sie in der [Preisübersicht](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="do-i-pay-for-expressroute-premium-in-addition-to-standard-expressroute-charges"></a>Fallen für ExpressRoute Premium neben dem standardmäßigen ExpressRoute-Tarif zusätzliche Gebühren an?

Ja. Für ExpressRoute Premium werden neben den ExpressRoute-Verbindungsgebühren und den Gebühren, die vom Konnektivitätsanbieter erhoben werden, zusätzliche Gebühren berechnet.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute für Office 365 und Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-to-connect-to-office-365-services-and-dynamics-365"></a>Wie erstelle ich eine ExpressRoute-Verbindung mit Office 365-Diensten und Dynamics 365?

1. Überprüfen Sie die Anforderungen auf der Seite mit den [ExpressRoute-Voraussetzungen](expressroute-prerequisites.md), um sicherzustellen, dass Sie die Anforderungen erfüllen.
2. Um sicherzustellen, dass Ihre Konnektivitätsanforderungen erfüllt werden, überprüfen Sie die Liste der Dienstanbieter und Standorte im Artikel [ExpressRoute-Partner und -Standorte](expressroute-locations.md).
3. Planen Sie Ihre Kapazitätsanforderungen mithilfe der Informationen unter [Netzwerkplanung und Leistungsoptimierung für Office 365](http://aka.ms/tune/).
4. Befolgen Sie die Schritte in den Workflows zum Einrichten der Konnektivität unter [ExpressRoute-Workflows für die Verbindungsbereitstellung und Verbindungszustände](expressroute-workflows.md).

> [!IMPORTANT]
> Stellen Sie sicher, dass das ExpressRoute Premium-Add-On aktiviert ist, wenn Sie die Konnektivität mit Office 365-Diensten und Dynamics 365 konfigurieren.
> 
> 

### <a name="do-i-need-to-enable-azure-public-peering-to-connect-to-office-365-services-and-dynamics-365"></a>Muss ich das öffentliche Azure-Peering aktivieren, um eine Verbindung mit Office 365-Diensten und Dynamics 365 herzustellen?

Nein, Sie müssen nur Microsoft-Peering aktivieren. Der Authentifizierungsdatenverkehr an Azure AD wird über das Microsoft-Peering gesendet. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-to-office-365-services-and-dynamics-365"></a>Unterstützen meine vorhandenen ExpressRoute-Verbindungen die Konnektivität mit Office 365-Diensten und Dynamics 365?

Ja. Ihre bestehende ExpressRoute-Verbindung kann so konfiguriert werden, dass sie eine Konnektivität mit Office 365-Diensten unterstützt. Stellen Sie sicher, dass Sie über ausreichend Kapazität für die Verbindung mit Office 365-Diensten verfügen, und dass das Premium-Add-On aktiviert ist. Unter [Netzwerkplanung und Leistungsoptimierung für Office 365](http://aka.ms/tune/) finden Sie Hilfe zur Planung Ihrer Konnektivitätsanforderungen. Siehe auch [Erstellen und Ändern einer ExpressRoute-Verbindung](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>Welche Office 365-Dienste sind über eine ExpressRoute-Verbindung zugänglich?

Eine aktuelle Liste der von ExpressRoute unterstützten Dienste finden Sie unter [URLs und IP-Adressbereiche von Office 365](http://aka.ms/o365endpoints) .

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Wie viel kosten ExpressRoute für Office 365-Dienste und Dynamics 365?

Office 365-Dienste und Dynamics 365 erfordern ein aktiviertes Premium-Add-On. Informationen zu den Kosten finden Sie auf der Seite mit den [Preisdetails](https://azure.microsoft.com/pricing/details/expressroute/).

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>In welchen Regionen wird ExpressRoute für Office 365 unterstützt?

Weitere Informationen finden Sie unter [ExpressRoute-Partner und Standorte](expressroute-locations.md).

### <a name="can-i-access-office-365-over-the-internet-even-if-expressroute-was-configured-for-my-organization"></a>Kann ich über das Internet auf Office 365 zugreifen, selbst wenn für meine Organisation ExpressRoute konfiguriert wurde?

Ja. Office 365-Dienstendpunkte sind über das Internet erreichbar, selbst wenn ExpressRoute für Ihr Netzwerk konfiguriert wurde. Erkundigen Sie sich beim Netzwerkteam Ihrer Organisation, ob das Netzwerk an Ihrem Standort für die Herstellung einer ExpressRoute-Verbindung mit Office 365-Diensten konfiguriert ist.

### <a name="how-can-i-plan-for-high-availability-for-office-365-network-traffic-on-azure-expressroute"></a>Wie kann ich bei Office 365-Netzwerkdatenverkehr über Azure ExpressRoute für hohe Verfügbarkeit sorgen?
Lesen Sie die Empfehlung unter [Hohe Verfügbarkeit und Failover mit Azure ExpressRoute](https://aka.ms/erhighavailability).

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Kann ich über eine Azure US Government-ExpressRoute-Verbindung auf Government Community Cloud-Dienste (GCC) von Office 365 US Government zugreifen?

Ja. Office 365 GCC-Dienstendpunkte sind über Azure US Government-ExpressRoute erreichbar. Sie müssen jedoch zunächst im Azure-Portal ein Supportticket öffnen, um die Präfixe bereitzustellen, die Sie Microsoft ankündigen möchten. Nachdem das Support-Ticket erfolgreich bearbeitet wurde, wird die Konnektivität mit den GCC-Diensten von Office 365 hergestellt. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>Kann ich über eine ExpressRoute-Verbindung auf Dynamics 365 for Operations (früher als Dynamics AX Online bekannt) zugreifen?

Ja. [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) wird in Azure gehostet. Sie können das öffentliche Azure-Peering in Ihrer ExpressRoute-Leitung aktivieren, um eine Verbindung mit ExpressRoute herzustellen.

## <a name="route-filters-for-microsoft-peering"></a>Routenfilter für das Microsoft-Peering

### <a name="i-am-turning-on-microsoft-peering-for-the-first-time-what-routes-will-i-see"></a>Ich aktiviere das Microsoft-Peering zum ersten Mal. Welche Routen werden angezeigt?

Es werden keine Routen angezeigt. Sie müssen Ihrer Verbindung einen Routenfilter zuordnen, um Präfixankündigungen zu starten. Weitere Anweisungen finden Sie unter [Konfigurieren von Routenfiltern für das Microsoft-Peering](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-to-select-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-to-do-it"></a>Ich habe das Microsoft-Peering aktiviert und möchte nun Exchange Online aktivieren, allerdings wird die Fehlermeldung angezeigt, dass ich dazu nicht autorisiert bin.

Jeder Kunde kann bei der Verwendung von Routenfiltern das Microsoft-Peering aktivieren. Um Office 365-Dienste nutzen zu können, müssen Sie jedoch nach wie vor von Office 365 autorisiert werden.

### <a name="do-i-need-to-get-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Benötige ich eine Autorisierung, um Dynamics 365 über das Microsoft-Peering zu aktivieren?

Nein, Sie benötigen keine Autorisierung für Dynamics 365. Sie können eine Regel erstellen und die Dynamics 365-Community ohne Autorisierung auswählen.

### <a name="i-enabled-microsoft-peering-prior-to-august-1st-2017-how-can-i-take-advantage-of-route-filters"></a>Ich habe Microsoft-Peering vor dem 1. August 2017 aktiviert. Wie kann ich Routenfilter nutzen?

Ihre vorhandene Verbindung kündigt weiterhin die Präfixe für Office 365 und Dynamics 365 an. Wenn Sie Ankündigungen für öffentliche Azure-Präfixe über das gleiche Microsoft-Peering hinzufügen möchten, können Sie einen Routenfilter erstellen, die anzukündigenden Dienste auswählen (einschließlich der benötigten Office 365-Dienste und Dynamics 365) und den Filter an Ihr Microsoft-Peering anfügen. Weitere Anweisungen finden Sie unter [Konfigurieren von Routenfiltern für das Microsoft-Peering](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-to-enable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>An einem Standort besitze ich die Möglichkeit zum Microsoft-Peering. Nun versuche ich, es an einem anderen Standort zu aktivieren, sehe jedoch keine Präfixe.

* Beim Microsoft-Peering von ExpressRoute-Verbindungen, die vor dem 1. August 2017 konfiguriert wurden, werden alle Dienstpräfixe über das Microsoft-Peering angekündigt, auch wenn keine Routenfilter definiert sind.

* Beim Microsoft-Peering von ExpressRoute-Verbindungen, die am oder nach dem 1. August 2017 konfiguriert wurden, werden Präfixe erst angekündigt, wenn der Verbindung ein Routenfilter hinzugefügt wurde. Standardmäßig werden dabei keine Präfixe angezeigt.
