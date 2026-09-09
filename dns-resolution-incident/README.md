# Network Traffic Analysis: DNS Resolution Incident

## Objective
To analyze network traffic logs using TCPDump to investigate and document a disruption in web service availability, mirroring a standard SOC incident response workflow.

### Skills Demonstrated
- Network traffic analysis and packet inspection
- Incident response documentation and reporting
- Protocol analysis (DNS, ICMP, UDP)

### Tools Used
- TCPDump (Packet Analyzer)

## Scenario
At 1:24 PM, multiple clients reported an inability to access the corporate website, `www.yummyrecipesforme.com`. Users experienced a "destination port unreachable" error upon attempting to load the page. 

## Incident Analysis & Findings
During the initial investigation, packet analysis revealed the following:
* **Protocol Failure:** The network analyzer received an ICMP error code "Unreachable" on UDP Port 53.
* **Root Cause Identification:** UDP Port 53 is dedicated to handling DNS requests. The unreachable status indicates that the DNS server is failing to resolve the domain name to an IP address because there are no services responding on the receiving DNS server
* **Potential Factors:** This failure could stem from a downed DNS server, misconfigured firewall rules blocking UDP Port 53, or a broader server configuration error.

## Recommended Next Steps
To resolve the incident and restore service, the following actions are required:
1. **Investigate DNS Server Status:** Verify the connection and services on the primary DNS server.
2. **Review Firewall Configurations:** Audit current firewall rules to ensure traffic on UDP Port 53 is explicitly allowed.
3. **Collaborate with Administration:** Coordinate with system administrator to check for misconfigurations or potential indicators of compromise (IoCs) associated with an attack.
