# Incident Response: TCP SYN Flood Denial of Service (DoS)

## Objective
To analyze network logs to identify the root cause of a network interruption, document the type of attack, and explain the impact of the attack.

### Skills Demonstrated
* Analyzing network logs to identify malicious traffic patterns.
* Documenting incident response findings for SOC ticketing workflows.
* Explaining fundamental TCP protocol mechanics (Three-way Handshake).
* Identifying the attack techniques and their impact on server resources.

## Incident Summary
A severe network interruption caused website visitors to experience widespread connection timeouts. Initial analysis of the network logs revealed a massive influx of TCP SYN packets occurring over a 30-second span, all originating from a single source IP address (`203.0.113.0`). 

## Technical Analysis
Base on the packet recorded through Wireshark, the incident was identified as a **TCP SYN Flooding Denial of Service (DoS) attack**.

### The Standard TCP Three-Way Handshake
Under normal network operations, a connection is established using the following sequence:
1. **SYN:** The client sends a synchronization request to the server.
2. **SYN/ACK:** The server acknowledges the request and sends a synchronization response back to the client.
3. **ACK:** The client sends a final acknowledgement, establishing the TCP connection.
*(Upon completion of data transfer, a FIN/ACK sequence terminates the connection).*

### The Attack Mechanism
During this incident, a malicious actor intentionally sent a massive volume of initial SYN requests all at once. 
* The server attempted to process these by allocating resources and keeping ports open while waiting for the final `ACK` from the client.
* Because the attacker never completed the handshake, the server was left with a backlog of half-open connections.
* This flood of incomplete requests exhausted the server's available ports and memory, rendering it unable to process legitimate traffic and ultimately causing the server to crash.
