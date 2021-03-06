﻿---
title: 'Lync Server 2013: Zertifikatzusammenfassung für einen einzelnen konsolidierten Edgeserver mit privaten IP-Adressen und NAT'
TOCTitle: Zertifikatzusammenfassung für einen einzelnen konsolidierten Edgeserver mit privaten IP-Adressen und NAT
ms:assetid: 6de6680e-5f47-48e6-8e06-4994d710ea6d
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398519(v=OCS.15)
ms:contentKeyID: 49294339
ms.date: 12/16/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Zertifikatzusammenfassung für einen einzelnen konsolidierten Edgeserver mit privaten IP-Adressen und NAT in Lync Server 2013

 

_**Letztes Änderungsdatum des Themas:** 2016-12-15_

Microsoft Lync Server 2013 verwendet Zertifikate zum gegenseitigen Authentifizieren von Servern und zum Verschlüsseln von Daten zwischen Servern sowie zwischen Server und Client. Bei Zertifikaten müssen die Namen der DNS-Einträge (Domain Name System), die den Servern zugeordnet sind, sowie der Antragstellername (Subject Name, SN) und der alternative Antragstellername (Subject Alternative Name, SAN) im Zertifikat übereinstimmen. Für die erfolgreiche Zuordnung von Servern, DNS-Einträgen und Zertifikateinträgen müssen Sie die vollqualifizierten Domänennamen des vorgesehenen Servers wie im DNS und in den SN- und SAN-Einträgen im Zertifikat registriert sorgfältig planen.

Das Zertifikat, das den externen Schnittstellen des Edgeservers zugeordnet ist, wird von einer öffentlichen Zertifizierungsstelle angefordert. Öffentliche Zertifizierungsstellen, die bereits erfolgreich Zertifikate für Unified Communications bereitgestellt haben, sind in folgendem Artikel aufgelistet: <http://go.microsoft.com/fwlink/?linkid=3052>. Wenn Sie das Zertifikat anfordern, können Sie die vom Lync Server-Bereitstellungs-Assistent generierte Zertifikatanforderung verwenden oder die Anforderung manuell mithilfe der Lync Server-Verwaltungsshell-Cmdlets oder nach dem von einer öffentlichen Zertifizierungsstelle angebotenen Verfahren generieren. Ausführliche Informationen zur Verwendung der Lync Server-Verwaltungsshell-Cmdlets für die Zertifikatverwaltung erhalten Sie im Abschnitt [Cmdlets für Zertifikate und Authentifizierung](lync-server-2013-certificate-and-authentication-cmdlets.md). Bei der Zuweisung des Zertifikats wird das Zertifikat der Zugriffs-Edgedienst-Schnittstelle, der Webkonferenz-Edgedienst-Schnittstelle und dem Audio-Video-Authentifizierungsdienst zugewiesen. Der Audio-Video-Authentifizierungsdienst ist nicht zu verwechseln mit dem A/V-Edgedienst, bei dem für die Verschlüsselung der Audio- und Videostreams kein Zertifikat verwendet wird. Die interne Edgeserver-Schnittstelle kann ein Zertifikat einer internen (innerhalb Ihres Unternehmens) Zertifizierungsstelle oder einer öffentlichen Zertifizierungsstelle verwenden. Das interne Schnittstellenzertifikat verwendet nur den SN und benötigt bzw. verwendet keine SAN-Einträge.


> [!TIP]
> Die folgende Tabelle zeigt zu Referenzzwecken einen sekundären SIP-Eintrag ( sip.fabrikam.com ) in der Liste für alternative Antragstellernamen. Für jede SIP-Domäne in Ihrer Organisation müssen Sie einen entsprechenden FQDN in der Liste der alternativen Antragstellernamen des Zertifikats hinzufügen.



## Erforderliche Zertifikate für einen einzelnen konsolidierten Edgeserver mit privaten IP-Adressen bei Verwendung von NAT


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Komponente</th>
<th>Antragstellername</th>
<th>Alternative Antragstellernamen (SAN)/Reihenfolge</th>
<th>Kommentare</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Einzelner konsolidierter Edgeserver (externer Edge)</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Das Zertifikat muss von einer öffentlichen Zertifizierungsstelle stammen und benötigt die erweiterte Schlüsselverwendung (Enhanced Key Usage, EKU) für den Server und den Client, falls die Verbindung mit den öffentlichen Chatdiensten von AOL bereitgestellt werden soll. Das Zertifikat wird den externen Edgeschnittstellen zugewiesen für:</p>
<ul>
<li><p>Zugriffsedgedienst</p></li>
<li><p>Konferenz-Edgedienst</p></li>
<li><p>A/V-Edgedienst</p></li>
</ul>
<p>Beachten Sie, dass SANs basierend auf Ihren Definitionen im Topologie-Generator automatisch dem Zertifikat hinzugefügt werden. Sie fügen SAN-Einträge bei Bedarf für zusätzliche SIP-Domänen und sonstige Einträge, die unterstützt werden müssen, hinzu. Der Antragstellername wird im SAN repliziert und muss für den ordnungsgemäßen Betrieb vorhanden sein.</p></td>
</tr>
<tr class="even">
<td><p>Einzelner konsolidierter Edgeserver (interner Edge)</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>Kein SAN erforderlich</p></td>
<td><p>Das Zertifikat kann von einer öffentlichen oder privaten Zertifizierungsstelle ausgestellt werden und muss die erweiterte Schlüsselverwendung (Enhanced Key Usage, EKU) für den Server enthalten. Das Zertifikat wird der internen Edgeschnittstelle zugewiesen.</p></td>
</tr>
</tbody>
</table>


## Zertifikatszusammenfassung - Verbindung mit öffentlichen Chatdiensten


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Komponente</th>
<th>Antragstellername</th>
<th>Alternative Antragstellernamen (SAN)/Reihenfolge</th>
<th>Kommentare</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Extern/Zugriffsedge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Das Zertifikat muss von einer öffentlichen Zertifizierungsstelle stammen und benötigt die erweiterte Schlüsselverwendung (Enhanced Key Usage, EKU) für den Server und den Client, falls die Verbindung mit den öffentlichen Chatdiensten von AOL bereitgestellt werden soll. Das Zertifikat wird den externen Edgeschnittstellen zugewiesen für:</p>
<ul>
<li><p>Zugriffsedgedienst</p></li>
<li><p>Konferenz-Edgedienst</p></li>
<li><p>A/V-Edgedienst</p></li>
</ul>
<p>Beachten Sie, dass SANs basierend auf Ihren Definitionen im Topologie-Generator automatisch dem Zertifikat hinzugefügt werden. Sie fügen SAN-Einträge bei Bedarf für zusätzliche SIP-Domänen und sonstige Einträge, die unterstützt werden müssen, hinzu. Der Antragstellername wird im SAN repliziert und muss für den ordnungsgemäßen Betrieb vorhanden sein.</p></td>
</tr>
</tbody>
</table>


## Zertifikatszusammenfassung für XMPP (Extensible Messaging and Presence Protocol)


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Komponente</th>
<th>Antragstellername</th>
<th>Alternative Antragstellernamen (SAN)/Reihenfolge</th>
<th>Kommentare</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Zuweisung zu Zugriffs-Edgedienst von Edgeserver oder Edgepool</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p>
<p>xmpp.contoso.com</p>
<p><strong>*.contoso.com</strong></p></td>
<td><p>Die ersten drei SAN-Einträge sind die regulären SAN-Einträge für einen vollständigen Edgeserver. contoso.com ist der für den Partnerverbund mit dem XMPP-Partner auf der Stammdomänenebene erforderliche Eintrag. Dieser Eintrag ermöglicht XMPP für alle Domänen mit dem Suffix *.contoso.com .</p></td>
</tr>
</tbody>
</table>

