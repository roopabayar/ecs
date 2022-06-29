# 0000: SDWAN Normalization RFC
•	Stage: 0 (strawperson)
•	Date: 2022-06-13
This RFC will provide normalization for fields related to the Versa Networks SDWAN logs to assure that they are retained primarily in ECS core and in any extended fieldset when needed. These fields are important to normalize into ECS fields in order to maximize effectiveness of cross log utilization. Similar fields are found in other SDWAN vendor logs so by leveraging this extension to ECS core, the ECS core field set will be more expansive. 
Fields

# Proposed Field Name |	Type	| Value |	Vendor Field
sdwan.localSiteName|Keyword|	   | applianceName, localSiteName
sdwan.localAccCktName|Keyword|  |accCktName, accCkt, localAccCktName
sdwan.remoteSiteName|Keyword|		|remoteSiteName
sdwan.remoteAccCktName|Keyword|	 |remoteAccCktName
sdwan.fwdEgrSiteName|Keyword|  |fwdEgrSiteName
sdwan.fwdEgrAccCktPairName|Keyword|  |fwdEgrAccCktName
sdwan.revIngSiteName|Keyword|		|revIngSiteName
sdwan.revIngAccCktPairName|Keyword|		|revIngAccCktName
sdwan.fwdIngSiteName|Keyword|		|fwdIngSiteName
sdwan.fwdIngAccCktPairName|Keyword|		|fwdIngAccCktName
sdwan.revEgrSiteName|Keyword|		|revEgrSiteName
sdwan.revEgrAccCktPairName|Keyword|		|revEgrAccCktName
sdwan.fwdClass|Keyword|		|fwdClass
sdwan.vrfName|Keyword|	|VRF
sdwan.interfaceName|Keyword|	|vni
sdwan.ruleName|Keyword|	|ruleName, rule
sdwan.ruleType|Keyword|	|ruleType
sdwan.trafficType|Keyword|0-Native, 1-SDWAN|	sdwan
sdwan.metrics.sentOctets|Long|		|sentOctets, mstatsTotSentOctets
sdwan.metrics.recvdOctets|Long|		|recvdOctets, mstatsTotRecvdOctets
sdwan.metrics.sessCnt|Long|		|sessCnt, mstatsTotSessCount
sdwan.pathMetrics.delay|Long|		|delay
sdwan.pathMetrics.fwdDelayVar|Long|		|fwdDelayVar
sdwan.pathMetrics.revDelayVar|Long|		|revDelayVar
sdwan.pathMetrics.fwdLoss|Long|		|fwdLoss
sdwan.pathMetrics.revLoss|Long|		|revLoss
sdwan.pathMetrics.fwdSent|Long|		|fwdSent
sdwan.pathMetrics.revSent|Long|		|revSent
sdwan.pathMetrics.fwdLossRatio|Long|	|fwdLossRatio
sdwan.pathMetrics.revLossRatio|Long|	|revLossRatio
sdwan.pathMetrics.pduLossRatio|Long|	|pduLossRatio


# Usage – SDWAN fields
# Field	Description
sdwan.localSiteName|Device name of the device that is generating the event 
sdwan.remoteSiteName|Device name of the remote device towards which a SDWAN overlay tunnel is established.
sdwan.localAccCktName|WAN link or access circuit name used on the device generating the event 
sdwan.remoteAccCktName|WAN link or access circuit name of the remote device towards which a SDWAN overlay tunnel is established.
sdwan.fwdEgrSiteName|SDWAN remote site towards which the source to destination traffic is sent from the local site.
sdwan.fwdEgrAccCktPairName|If Forward Egress Site is a SDWAN site, this field shows the local and remote wan link on which the traffic is sent. If there is no Forward Egress Site and the traffic is sent directly to internet, this field shows the local WAN link or the interface on which the traffic is sent.
sdwan.revIngSiteName|SDWAN remote site from which the destination to source traffic is received by this site.
sdwan.revIngAccCktPairName|If Reverse Egress Site is a SDWAN site, this field shows the local and remote wan link on which the traffic is received. If there is no Reverse Ingress Site and the traffic is received directly from internet, this field shows the local WAN link or the interface on which the traffic is received
sdwan.fwdIngSiteName|SDWAN remote site from which the source to destination traffic is received by this site.
sdwan.fwdIngAccCktPairName|If Forward Ingress Site is a SDWAN site, this field shows the local and remote wan link on which the traffic is received. If there is no Forward Ingress Site and the traffic is received directly from internet or LAN, this field shows the local interface on which the traffic is received.
sdwan.revEgrSiteName| SDWAN remote site to which the destination to source traffic is sent by this site
sdwan.revEgrAccCktPairName|If Reverse Egress Site is a SDWAN site, this field shows the local and remote wan link on which the traffic is sent. If there is no Reverse Egress Site and the traffic is sent directly to LAN, this field shows the local interface on which the traffic is sent.
sdwan.ruleName|SDWAN rule that was used for traffic steering decisions
sdwan.ruleType|SDWAN rule type (L2 or L3)
sdwan.fwdClass|Class of Service, forwarding class which is used by the application

# Usage – SDWAN Metrics
# Field	| Description
sdwan.metrics.sentOctets|Bytes sent in the last measurement interval
sdwan.metrics.recvdOctets|Bytes received in the last measurement interval
sdwan.metrics.sessCnt|Sessions created in the last measurement interval
sdwan.metrics.sentPackets|Packets sent
sdwan.metrics.recvdPackets|Packets received
sdwan.pathMetrics.delay|2-way delay measured on the SLA path in msec

sdwan.pathMetrics.fwdDelayVar|Forward delay variation in msec
sdwan.pathMetrics.revDelayVar|Reverse delay variation in msec
sdwan.pathMetrics.fwdLoss|Forward loss in bytes. Indicates actual traffic loss in the forward direction.
sdwan.pathMetrics.revLoss|Reverse loss in bytes. Indicates actual traffic loss in the reverse direction.
sdwan.pathMetrics.fwdSent|Number of data PDUs sent in the forward direction
sdwan.pathMetrics.revSent|Number of data PDUs sent in the forward direction
sdwan.pathMetrics.fwdLossRatio|Percentage of actual traffic lost in the forward direction.
sdwan.pathMetrics.revLossRatio|Percentage of actual traffic lost in the reverse direction.
sdwan.pathMetrics.pduLossRatio|Percentage of SLA PDUs (synthetic PDUs) lost


# Source data
The source data for the Versa Networks SDWAN solution comes from logs such as bwMonLog, monStatsLog, sdwanB2BSlamLog and flowMonLog . 
Example rawLog are as follows.

1)	SDWAN link usage
2022-06-14T00:09:57+0000 bwMonLog, applianceName=SDWAN-Branch1, tenantName=Tenant9, generateTime=1655165400, tenantId=11, vsnId=0, sentOctets=91453, recvdOctets=77728, sessCnt=0, mstatsType=sdwan-acc-ckt-bw-mon-stats, duration=300000, siteName=SDWAN-Branch1, accCktName=WAN1, siteId=106, accCktId=1

2)	WAN Link usage by application traffic sent/received on SDWAN overlay
2022-06-14T00:04:35+0000 monStatsLog, applianceName=SDWAN-Branch2, tenantName=Tenant1, mstatsTimeBlock=1655165700, tenantId=1, vsnId=0, mstatsTotSentOctets=611654, mstatsTotRecvdOctets=328959, mstatsTotSessDuration=300000, mstatsTotSessCount=604, mstatsType=sdwan-acc-ckt-stats, site=SDWAN-Branch2, accCkt=WAN1, siteId=104, accCktId=1, accessType=SDWAN, mstatsAttribs=

3)	WAN Link usage by application traffic sent using Direct Internet Access (DIA)
2022-06-14T00:14:33+0000 monStatsLog, applianceName=SDWAN-Branch5, tenantName=Tenant1, mstatsTimeBlock=1655166300, tenantId=1, vsnId=0, mstatsTotSentOctets=9398, mstatsTotRecvdOctets=0, mstatsTotSessDuration=300000, mstatsTotSessCount=79, mstatsType=sdwan-acc-ckt-stats, site=SDWAN-Branch5, accCkt=WAN2, siteId=101, accCktId=2, accessType=DIA, mstatsAttribs=

4)	WAN Link usage by LAN VRF
2022-06-14T00:04:57+0000 monStatsLog, applianceName=SDWAN-Branch1, tenantName=Tenant1, mstatsTimeBlock=1655165100, tenantId=2, vsnId=0, mstatsTotSentOctets=125920, mstatsTotRecvdOctets=71345, mstatsTotSessDuration=300000, mstatsTotSessCount=187, mstatsType=sdwan-vrf-stats, vrf=Tenant1-LAN-VR, vni=vni-0/3.101, sdwan=1, site=SDWAN-Branch1, accCkt=WAN3, siteId=106, accCktId=3, mstatsAttribs=

5)	Application Usage
2022-06-14T00:04:57+0000 monStatsLog, applianceName=SDWAN-Branch1, tenantName=Tenant1, mstatsTimeBlock=1655165100, tenantId=2, vsnId=0, mstatsTotSentOctets=0, mstatsTotRecvdOctets=416, mstatsTotSessDuration=300000, mstatsTotSessCount=1, mstatsType=sdwan-acc-ckt-app-stats, appId=linkedin, site=SDWAN-Branch1, accCkt=WAN3, siteId=106, accCktId=3, user=172.16.11.109, networkPrefix=172.16.0.0/16, traffType=SDWAN, fc=fc_be, risk=3, productivity=4, family=collaboration, subFamily=forum, bzTag=Non-Business
6)	SDWAN Path SLA Metrics
2022-06-14T00:15:19+0000 sdwanB2BSlamLog, applianceName=SDWAN-Controller1, tenantName=Tenant9, localAccCktName=WAN3, remoteAccCktName=WAN3, localSiteId=1, localSiteName=SDWAN-Controller1, remoteSiteId=106, remoteSiteName=SDWAN-Branch1, fwdClass=fc_nc, tenantId=10, delay=2, fwdDelayVar=0, revDelayVar=0, fwdLoss=0, revLoss=0, fwdLossRatio=0.00, revLossRatio=0.00, pduLossRatio=0.00, fwdSent=170, revSent=65, generateTime=1655166347
7)	SDWAN Path Usage
022-06-14T00:24:33+0000 monStatsLog, applianceName=SDWAN-Controller1, tenantName=Tenant1, mstatsTimeBlock=1655166900, tenantId=2, vsnId=0, mstatsTotSentOctets=0, mstatsTotRecvdOctets=1944559, mstatsTotSessDuration=300000, mstatsTotSessCount=40, mstatsType=sdwan-site2site-stats, localSite=SDWAN-Controller1, localAccCkt=WAN1, remoteSite=SDWAN-Branch3, remoteAccCkt=WAN1, localSiteId=1, localAccCktId=102, remoteSiteId=1, remoteAccCktId=1, mstatsAttribs=
8)	SDWAN Rule Usage
2022-06-14T00:24:32+0000 bwMonLog, applianceName=SDWAN-Branch2, tenantName=Tenant1, generateTime=1655166900, tenantId=1, vsnId=0, sentOctets=270504, recvdOctets=121502, sessCnt=273, mstatsType=sdwan-rule-bw-mon-stats, duration=300000, siteName=SDWAN-Branch2, accCktName=WAN3, ruleName=Business-Critical, ruleType=L3
9)	SDWAN Rule Path Usage
2022-06-14T00:14:34+0000 bwMonLog, applianceName=SDWAN-Branch2, tenantName=Tenant1, generateTime=1655166300, tenantId=1, vsnId=0, sentOctets=167676, recvdOctets=73481, sessCnt=166, mstatsType=sdwan-rule-path-bw-mon-stats, duration=300000, localSiteName=SDWAN-Branch2, localAccCktName=WAN3, remoteSiteName=SDWAN-Branch1, remoteAccCktName=WAN3, ruleName=Business-Critical, ruleType=L3
10)	SDWAN Traffic Monitoring Log
2022-06-14T00:16:51+0000 flowMonLog, applianceName=SDWAN-Branch1, tenantName=Tenant1, flowId=1107309510, flowCookie=1655165837, flowStartMilliseconds=327266164, flowEndMilliseconds=327266165, sentOctets=118, sentPackets=2, recvdOctets=0, recvdPackets=0, vsnId=0, applianceId=1, tenantId=2, appRisk=2, appProductivity=3, appIdStr=dns, appFamily=, appSubFamily=, urlCategory=, rule=DEFAULT-RULE, localSiteName=SDWAN-Branch1, fwdEgrSiteName=SDWAN-Branch5, fwdEgrAccCktName=WAN1:WAN2, revIngAccCktName=-, revIngSiteName=, fwdIngSiteName=, fwdIngAccCktName=vni-0/3.101, revEgrSiteName=, revEgrAccCktName=vni-0/3.101, deviceKey=Unknown, forwardForwardingClass=fc_be, reverseForwardingClass=fc_be, deviceName=Unknown, sourceIPv4Address=172.16.11.101, destinationIPv4Address=8.8.8.8, sourceTransportPort=42015, destinationTransportPort=53, protocolIdentifier=17, fromUser=abc@versa-networks.com

# Scope of impact
No impact expected as Versa Networks fieldsets are not impacting any existing fields, as these proposed fields are new. Moreover, these fields allow the Versa Networks SDWAN Logs and other SDWAN vendor logs to be in a greater alignment with the ECS base fields and allow for expanded utilization and wider adoption.
Concerns
The concerns that might arise relate to how the nested fields could be broken out into separate fields or that fields that are arrays are numbered. There are additional potential fields that could be implemented, but until they are seen in other vendor information, it makes sense to wait to add them to ECS.
People
The following are the people that consulted on the contents of this RFC.
•	@roopabayar| author
•	@ [USA] |coauthor
•	{insert name here} | sponsor
References

# RFC Pull Requests
•	Stage 0: https://github.com/elastic/ecs/pull/NNN

