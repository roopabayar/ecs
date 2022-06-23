0000: IDP Threat Event Normalization RFC
•	Stage: 0 (strawperson)
•	Date: 2022-06-14

This RFC will provide normalization for fields related to the Versa Networks IDP (Intrusion Detection Prevention) threat log to assure that they are retained primarily in ECS core and in any extended fieldset when needed. These fields are important to normalize into ECS fields in order to maximize effectiveness of cross log utilization. Similar fields are found in other vendor IDP logs so by leveraging this extension to ECS core, the ECS core field set will be more expansive. 

# Fields
# Proposed Field Name	Type|Value | Vendor Field
threat.idp.action|Keyword|idpAction
threat.idp.type|Keyword|Possible values: network/host/application/wireless etc
Versa’s value: network	
threat.idp.signatureId|Keyword|signatureId
threat.idp.severity|Keyword|signaturePriority
threat.idp.signatureMsg|Keyword|signatureMsg
threat.idp.category|Keyword|threatType
threat.idp.eventTime|Keyword|packetTime
threat.idp.hitCount|Long|hitCount
threat.idp.profileName|Keyword|ipsProfile
threat.idp.ruleName|Keyword|ipsProfileRule

# Usage
# Field| Description
threat.idp.action|The action taken by IDP.
threat.idp.type|Recommended values: network, host, application, wireless. Versa's data will be from network
threat.idp.signatureId|Signature matching the traffic
threat.idp.sererity|Priority or severity of the signature
threat.idp.signatureMsg|Message indicating the signature 
threat.idp.category|The category of the triggered signature as defined by vendor, such as spyware.
threat.idp.eventTime|Time when the event occurred
threat.idp.hitCount|How many times signature hit for the flow
threat.idp.profileName|Profile matching the traffic
threat.idp.ruleName|Rule matching the traffic

# Source data
The source data for the Versa Networks IDP data comes from idpLog. 
Here is a copy and example of a rawLog that came from Versa Networks.
2022-06-15T05:06:49+0000 idpLog, applianceName=SanJose-New-DC-Active, tenantName=Corp-Inline-Customer-1, flowId=2182281988, flowCookie=1655269619, signatureId=8010840, groupId=1, signatureRev=1, vsnId=0, applianceId=1, tenantId=1, moduleId=10, signaturePriority=critical, idpAction=reject, signatureMsg="TIQ-MAR-2016: Avast Authenticode Parsing Memory Corruption Attempt", classMsg="Attempted User Privilege Gain", threatType=attempted-user, packetTime=06/15/2022-10:37:00.370939, HitCount=1, ipsProfile=Versa Recommended Profile-versa-support-portal-fp, ipsProfileRule=Attack Severity Rule Filter, ipsDirection=ToClient, ipsProtocol=TCP, ipsApplication=windows_update, sourceIPv4Address=10.145.0.75, destinationIPv4Address=103.53.14.0, sourceTransportPort=62308, destinationTransportPort=80, protocolIdentifier=6, fromUser=abc@versa-networks.com

# Scope of impact
No impact expected as Versa Networks fieldsets are not impacting any existing fields, as these proposed fields are new. Moreover, these fields allow the Versa Networks threat Logs and other security vendor’s IDP logs to be in a greater alignment with the ECS base fields and allow for expanded utilization and wider adoption.

# Concerns 
The concerns that might arise relate to how the nested fields could be broken out into separate fields or that fields that are arrays are numbered. There are additional potential fields that could be implemented, but until they are seen in other vendor information, it makes sense to wait to add them to ECS.
People

The following are the people that consulted on the contents of this RFC.
•	@Roopa Bayar| author
•	@Mr1716 |coauthor
•	{insert name here} | sponsor
References

RFC Pull Requests
•	Stage 0: https://github.com/elastic/ecs/pull/NNN
