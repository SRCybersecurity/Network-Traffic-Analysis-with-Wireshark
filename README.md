# Network Traffic Analysis Using Wireshark

A hands-on network traffic analysis project focused on capturing live packets, identifying common network protocols, examining packet-level communication, and documenting network activity using Wireshark. This exercise demonstrates fundamental network monitoring, protocol analysis, and traffic investigation techniques relevant to cybersecurity, SOC operations, and network troubleshooting.

### 🎯 Objective

Capture and analyze live network traffic to identify common protocols, examine source and destination addresses, inspect packet metadata, and document observed communication patterns.

### 🛠️ Tools Used

| Attribute | Details |
|---|---|
| Project Name | Network Traffic Analysis Using Wireshark |
| Assessment Type | Network packet capture and protocol analysis |
| Primary Tool | [Wireshark](https://www.wireshark.org/) |
| Traffic Generation | Web browsing and ICMP ping |
| Protocols Investigated | DNS, TCP, HTTP, TLS, and ICMP |
| Reported Packet Count | 287 packets |
| Reported Capture Duration | Approximately 317.611 seconds |
| Packet Loss | Reported as 0% during the exercise; measurement method not specified |
| Deliverables | Packet capture file (`.pcap` or `.pcapng`), analysis report, and screenshots |

**Note:** The reported packet counts, IP addresses, timestamps, and packet sizes should be validated against the original packet capture before being treated as independently verified results.

### 📋 Project Overview

| Attribute | Details |
|---|---|
| Project Name | Network Traffic Analysis Using Wireshark |
| Assessment Type | Network packet capture and protocol analysis |
| Primary Tool | [Wireshark](https://www.wireshark.org/) |
| Traffic Generation | Web browsing and ICMP ping |
| Protocols Investigated | DNS, TCP, HTTP, TLS, and ICMP |
| Reported Packet Count | 287 packets |
| Reported Capture Duration | Approximately 317.611 seconds |
| Packet Loss | Reported as 0% during the exercise; measurement method not specified |
| Deliverables | Packet capture file (`.pcap` or `.pcapng`), analysis report, and screenshots |

**Note:** The reported packet counts, IP addresses, timestamps, and packet sizes should be validated against the original packet capture before being treated as independently verified results.

### 🔬 Methodology

**1. Start Wireshark**

1. Open Wireshark.
2. Select the active network interface, such as Wi-Fi or Ethernet.
3. Start capturing packets using the blue shark-fin icon.
4. Confirm that packets are appearing in the capture window.

**2. Generate Network Traffic**

Generate normal network traffic to observe different protocols.

Web browsing: Visit a website to generate DNS queries, TCP connections, and encrypted TLS traffic where applicable.

ICMP traffic: Open a terminal and execute:

``` bash
ping google.com

```
Allow the capture to run for approximately 60 seconds, or for the duration required by the exercise.

Only generate traffic against systems you own or are authorized to access.

**3. Stop and Inspect the Capture**

1. Return to Wireshark.
2. Stop the capture using the red square button.
3. Review the packet list and protocol hierarchy. 
4. Apply display filters to isolate relevant traffic.
5. Inspect packet details, timestamps, source and destination addresses, and protocol fields.
   
**4. Apply Display Filters**

Use the following Wireshark display filters to investigate individual protocols.

| Protocol | Display Filter | Purpose |
|---|---|---|
| DNS | `dns` | Displays recognized DNS queries and responses. |
| TCP | `tcp` | Displays TCP packets and connection activity. |
| HTTP | `http` | Displays recognized HTTP traffic. |
| TLS | `tls` | Displays recognized TLS handshake and encrypted-session packets. |
| ICMP | `icmp` | Displays IPv4 ICMP messages, including ping requests and replies. |
| HTTPS-Related TCP Traffic | `tcp.port == 443` | Displays TCP traffic using port 443; this does not independently confirm that every packet contains HTTPS. |
| Specific Host | `ip.addr == 10.10.10.128` | Displays IPv4 packets where the specified address is the source or destination. |

**Protocol Analysis Note:** HTTPS uses HTTP over a secure transport, commonly TLS. Wireshark can identify TLS traffic and expose certain connection metadata, but encrypted application content is generally not readable without the appropriate decryption material.

### 📊 Reported Capture Summary

| Metric | Reported Result |
|---|---|
| Total Packets | 287 |
| Received Packets | 287 |
| Capture Duration | 317.611 seconds |
| Packet Loss | 0% reported; measurement method not specified |
| Traffic Generation | Website browsing and ping to `google.com` |
| Protocols Observed | DNS, TCP, TLS, HTTP-related traffic, and ICMP |

**Note:** These values reflect the reported exercise results. Verify them against the original Wireshark capture before treating them as confirmed measurements. A capture showing 287 packets does not, by itself, establish that no packets were lost on the network.

**Interpretation:** The reported capture contains examples of name resolution, transport-layer communication, encrypted web traffic, and ICMP connectivity testing. The packet count and loss figures describe the supplied exercise results and should not be interpreted as proof that no packets were lost on the network.

### 🔎 Observed Protocols

**1. Domain Name System (DNS)**

DNS resolves domain names into IP addresses and may also return other record types.

| Attribute | Reported Observation |
|---|---|
| Protocol | DNS |
| Source IP | `10.10.10.2` |
| Destination IP | `10.10.10.128` |
| Source Port | `53` |
| Reported Information | AAAA-related DNS query/response involving `detectportal.firefox.com` |

**Security relevance:** DNS analysis helps identify name-resolution activity, unexpected domains, suspicious DNS patterns, and potential communication with untrusted infrastructure.

**2. Transmission Control Protocol (TCP)**

TCP provides reliable, connection-oriented transport for applications such as HTTP and HTTPS.

| Attribute | Reported Observation |
|---|---|
| Protocol | TCP |
| Source IP | `23.38.59.250` |
| Destination IP | `10.10.10.128` |
| Reported Information | TCP acknowledgment and connection-related activity |
| Example Connection Sequence | SYN, SYN-ACK, ACK |

**Security Relevance:** TCP analysis helps investigate connection establishment, retransmissions, connection resets, unusual communication patterns, and unexpected service activity.

**3. Transport Layer Security (TLS)**

TLS protects application data in transit and is commonly used for HTTPS connections.

| Attribute | Reported Observation |
|---|---|
| Protocol | TLS |
| Source IP | `10.10.10.128` |
| Destination IP | `172.64.41.4` |
| Destination Port | `443` |
| Reported TLS Version | TLS 1.2 |
| Reported Packet Size | 213 bytes, according to the supplied observation |

**Security relevance:** TLS inspection can reveal handshake metadata, negotiated protocol details, and certificate-related information when available. Encrypted application payloads generally remain unreadable without the required decryption information.

**4. HTTP and HTTPS-Related Traffic**

HTTP carries web requests and responses. HTTPS protects HTTP communication using TLS.

| Attribute | Reported Observation |
|---|---|
| Protocol | HTTP / HTTPS-related traffic |
| Reported Source IP | `10.10.10.128` |
| Reported Destination IP | `23.38.59.250` |

**Security relevance:** Plain HTTP can expose application data in transit. HTTPS helps protect confidentiality and integrity, subject to correct TLS configuration and certificate validation.

**Validation note:** The reported HTTP/1.1 description alone does not establish whether the traffic was encrypted. Confirm the relevant packet details and protocol layers in the original capture.

**5. Internet Control Message Protocol (ICMP)**

ICMP supports network diagnostics and connectivity testing, including the ping utility.

| Attribute | Reported Observation |
|---|---|
| Protocol | ICMP |
| Source IP | `142.251.222.110` |
| Destination IP | `10.10.10.128` |
| Reported Information | Echo request and reply activity |
| Associated Command | `ping google.com` |

**Security Relevance:** ICMP analysis can help identify connectivity issues, host discovery activity, and unusual diagnostic traffic. ICMP activity alone does not establish malicious behavior.

### 📦 Packet Details

The following table consolidates the packet observations supplied for the exercise.

| Protocol | Source IP | Destination IP | Reported Information |
|---|---|---|---|
| DNS | `10.10.10.2` | `10.10.10.128` | AAAA-related DNS activity involving `detectportal.firefox.com` |
| TLS | `10.10.10.128` | `172.64.41.1` | TLS 1.2 reported |
| TCP | `23.38.59.250` | `10.10.10.128` | TCP acknowledgment and connection-related activity |
| HTTP / HTTPS-related | `10.10.10.128` | `23.38.59.250` | HTTP/1.1-related traffic reported |
| ICMP | `142.251.222.110` | `10.10.10.128` | Echo request and reply activity |


### 🛡️ Security Analysis and Key Learnings

| Analysis Area | Observation | Security Relevance |
|---|---|---|
| DNS Resolution | DNS activity was reported during normal network use. | Demonstrates the role of DNS in resolving domain names into IP addresses. |
| TCP Communication | TCP connection-related packets were reported. | Illustrates connection establishment and transport-layer communication. |
| Encrypted Traffic | TLS 1.2 was reported in the capture. | Demonstrates encrypted communication and the connection metadata visible to packet analyzers. |
| Web Traffic | HTTP/1.1-related traffic was reported. | Highlights the importance of distinguishing encrypted HTTPS traffic from unencrypted HTTP traffic. |
| ICMP Diagnostics | Ping-related echo traffic was reported. | Demonstrates basic connectivity testing and ICMP packet analysis. |
| Capture Evidence | A packet capture file and screenshots are required deliverables. | Supports reproducibility, investigation, evidence validation, and technical reporting. |

### 📸 Screenshots and Evidence

Include screenshots of the actual Wireshark capture to demonstrate the analysis.

| Screenshot | Required Evidence |
|---|---|
| Capture Overview | Packet list, capture duration, total packet count, and capture statistics. |
| DNS Analysis | A selected DNS packet showing query or response details, source and destination IP addresses, and DNS records. |
| TCP Analysis | A selected TCP packet or connection sequence, including SYN, SYN-ACK, and ACK flags where available. |
| TLS Analysis | A selected TLS handshake or encrypted-session packet showing protocol details and connection endpoints. |
| ICMP Analysis | A ping echo request and its corresponding reply, where available. |
| Protocol Hierarchy | Wireshark's protocol distribution summary, if available. |

**Example project structure:**

``` text
Network-Traffic-Analysis-Wireshark/
├── README.md
├── network-traffic-analysis.pcapng   
├── pckt_strt.png
├── pckt_ends.png
├── dns.png
├── tcp.png
├── tls.png
└── icmp.png
└── network-traffic-analysis-report.pdf
```

**💾 Export the Packet Capture**

To save the capture:

Select File → Save As in Wireshark.
- Choose the appropriate destination.
- Save the capture as .pcapng or .pcap.
- Reopen the saved file to verify that it contains the expected packets.
- Preserve the corresponding screenshots and analysis report.
- The .pcapng format is Wireshark's modern capture format and can preserve additional metadata. Use .pcap when compatibility with other tools requires it.

### ⚠️ Limitations

- The reported observations do not independently establish that every listed protocol or packet detail has been verified against the original capture.
- Encrypted TLS payloads generally cannot be inspected as readable application data without appropriate decryption material.
- Packet capture visibility depends on the network interface, capture permissions, network topology, and traffic path.
- IP addresses and service endpoints may change between capture sessions.
- A short capture provides only a limited view of network activity and cannot establish that a network is secure.
- The reported 0% packet loss requires clarification of how it was measured; a packet capture alone does not prove that no network packets were lost.
- Captured traffic may contain sensitive information. Handle and share packet captures according to organizational security and privacy requirements.

### ⚖️ Responsible Use
This project is intended for cybersecurity education, network troubleshooting, and authorized defensive analysis.

- Capture traffic only on networks and devices you own or are explicitly authorized to monitor.
- Avoid collecting unnecessary personal or confidential information.
- Protect packet captures and screenshots as potentially sensitive evidence.
- Do not use packet analysis to intercept or disclose other people's communications without authorization.

### 🏁 Conclusion

This project demonstrates a foundational Wireshark workflow for capturing network traffic, identifying common protocols, inspecting packet metadata, and documenting findings. By analyzing DNS, TCP, TLS, HTTP-related traffic, and ICMP, the exercise builds practical skills relevant to network troubleshooting, security monitoring, and SOC investigations.

Capture the traffic. Analyze the protocols. Validate the evidence. Document the findings.
