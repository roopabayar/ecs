0000: Traffic Flow Fields Normalization RFC
•	Stage: 0 (strawperson)
•	Date: 2022-06-14
This RFC will provide normalization for fields related to the Versa Networks flow logs to assure that they are retained primarily in ECS core and in any extended fieldset when needed. These fields are important to normalize into ECS fields in order to maximize effectiveness of cross log utilization. Similar fields are found in other vendor flow logs so by leveraging this extension to ECS core, the ECS core field set will be more expansive. 
Fields

# Proposed Field Name|Type|Value|	Vendor Field
flow.id|Keyword|Unique value to identify all related flows.|flowId/flowCookie
flow.startTime|Long|Time since epoch value in milliseconds| flowStartMilliSeconds
flow.endTime|Long|Time since epoch value in milliseconds|flowEndMilliSeconds
flow.fwdForwardingClass|Keyword|Values could be BE (Best Effort), EF (Expedited Forwarding), AF (Assured Forwarding), NC (Network control) etc |forwardForwardingClass 
flow.revForwardingClass|Keyword|	Values could be BE (Best Effort), EF (Expedited Forwarding), AF (Assured Forwarding), NC (Network control) etc|reverseForwardingClass
flow.sentOctets|Long|sentOctets
flow.recvdOctets|Long|recvdOctets
flow.sentPackets|Long|sentPackets
flow.recvdPackets|Long|recvdPackters


# Usage
# Field|Description
flow.id|String which uniquely identifies a traffic flow (having same sourceIP/destinationIP/sourcePort/destinationPort for a tenant/device) and can be used to correlate related flows.
flow.startTime|Time since epoch in msec when the flow was created
flow.endTime|Time since epoch in msec when the flow was terminated
flow.fwdForwardingClass|Forwarding class for the flow in the forward direction.
flow.revForwardingClass|Forwarding class for the flow in the reverse direction.
flow.sentOctets|Number of octets sent by the flow
flow.recvdOctets|Number of octets received by the flow
flow.sentPackets|Number of packets sent by the flow
flow.recvdPackets|Number of packets received by the flow


# Source data
The source data for the Versa Networks flow logs such as flowMonLog, accessLog, idpLog etc 
Here is a copy and example of a rawLog that came from Versa Networks.
2022-06-21T22:05:27+0000 accessLog, applianceName=Bangalore-ECT-DC-Active, tenantName=Corp-Inline-Customer-1, flowId=37383299, flowCookie=1655849135, flowStartMilliseconds=832317571, flowEndMilliseconds=832317571, sentOctets=180, sentPackets=3, recvdOctets=0, recvdPackets=0, appId=1, eventType=end, tenantId=2, urlCategory=, action=allow, vsnId=0, applianceId=1, appRisk=2, appProductivity=2, appIdStr=unknown_tcp, appFamily=networking, appSubFamily=unknown, rule=Allow_From_Trust, forwardForwardingClass=fc_be, reverseForwardingClass=fc_be, host=, deviceKey=Unknown, deviceName=Unknown, sourceIPv4Address=192.168.95.2, destinationIPv4Address=192.168.75.2, sourceTransportPort=52829, destinationTransportPort=20514, protocolIdentifier=6, fromUser=Unknown, srcSGT=Unknown, destSGT=
2022-06-21T22:03:29+0000 flowMonLog, applianceName=SDWAN-Branch1, tenantName=Tenant1, flowId=1107361187, flowCookie=1655849056, flowStartMilliseconds=86829587, flowEndMilliseconds=86829622, sentOctets=565, sentPackets=6, recvdOctets=1074, recvdPackets=4, vsnId=0, applianceId=1, tenantId=2, appRisk=2, appProductivity=3, appIdStr=office365, appFamily=, appSubFamily=, urlCategory=computer_and_internet_info, rule=DEFAULT-RULE, localSiteName=SDWAN-Branch1, fwdEgrSiteName=SDWAN-Branch3, fwdEgrAccCktName=WAN3:WAN3, revIngAccCktName=WAN3:WAN3, revIngSiteName=SDWAN-Branch3, fwdIngSiteName=, fwdIngAccCktName=vni-0/3.101, revEgrSiteName=, revEgrAccCktName=vni-0/3.101, deviceKey=Unknown, forwardForwardingClass=fc_be, reverseForwardingClass=fc_be, deviceName=Unknown, sourceIPv4Address=172.16.11.102, destinationIPv4Address=172.16.31.10, sourceTransportPort=50386, destinationTransportPort=80, protocolIdentifier=6, fromUser=Unknown
2022-06-15T05:06:49+0000 idpLog, applianceName=SanJose-New-DC-Active, tenantName=Corp-Inline-Customer-1, flowId=2182281988, flowCookie=1655269619, signatureId=8010840, groupId=1, signatureRev=1, vsnId=0, applianceId=1, tenantId=1, moduleId=10, signaturePriority=critical, idpAction=reject, signatureMsg="TIQ-MAR-2016: Avast Authenticode Parsing Memory Corruption Attempt", classMsg="Attempted User Privilege Gain", threatType=attempted-user, packetTime=06/15/2022-10:37:00.370939, HitCount=1, ipsProfile=Versa Recommended Profile-versa-support-portal-fp, ipsProfileRule=Attack Severity Rule Filter, ipsDirection=ToClient, ipsProtocol=TCP, ipsApplication=windows_update, sourceIPv4Address=10.145.0.75, destinationIPv4Address=103.53.14.0, sourceTransportPort=62308, destinationTransportPort=80, protocolIdentifier=6, fromUser=abc@versa-networks.com

# Scope of impact
No impact expected as Versa Networks fieldsets are not impacting any existing fields, as these proposed fields are new.  Moreover, these fields allow the Versa Networks flow Logs and other networking/security vendor’s flow logs to be in a greater alignment with the ECS base fields and allow for expanded utilization and wider adoption. Other modules will need to map their fields to these new fieldsets, which will bring these other modules closer into ECS alignment. 

# Concerns
The concerns that might arise relate to how the nested fields could be broken out into separate fields or that fields that are arrays are numbered. There are additional potential fields that could be implemented, but until they are seen in other vendor information, it makes sense to wait to add them to ECS.
People

The following are the people that consulted on the contents of this RFC.
•	@roopabayar| author
•	@Mr1716 |coauthor
•	{insert name here} | sponsor
References

RFC Pull Requests
•	Stage 0: https://github.com/elastic/ecs/pull/NNN
