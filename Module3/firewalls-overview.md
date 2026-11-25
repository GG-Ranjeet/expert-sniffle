# 9. Firewalls: Definition, Purpose, and Types

## Introduction

A **Firewall** is a network security system—implemented as hardware, software, or a cloud service—that monitors, filters, and controls incoming and outgoing network traffic based on a predetermined set of security rules.

It acts as a protective **gatekeeper/barrier** placed between a **trusted internal network** (e.g., a corporate LAN or home device) and an **untrusted external network** (e.g., the public Internet).

```text
+--------------------+         +-----------------+         +--------------------+
|  Trusted Internal  | <-----> |    FIREWALL     | <-----> | Untrusted External |
|   Network (LAN)    |         | (Allow / Deny   |         | Network (Internet) |
|                    |         |  by Rule Set)   |         |                    |
+--------------------+         +-----------------+         +--------------------+
```

---

## Why Are Firewalls Used? (Purpose & Benefits)

1. **Blocking Unauthorized Access:** Prevents hackers, port scanners, and unauthorized external users from reaching internal servers and workstations.
2. **Preventing Malware & Exploits:** Blocks suspicious traffic patterns, malicious payloads, and known attack vectors before they reach endpoints.
3. **Controlling Outbound Traffic (Data Leakage Prevention):** Prevents compromised internal machines (e.g., bots or spyware) from phoning home or exfiltrating sensitive data.
4. **Content & Application Filtering:** Allows organizations to restrict access to unauthorized websites, non-work applications, or risky ports.
5. **Traffic Logging & Auditing:** Records allowed and blocked connection attempts, providing visibility for threat detection and compliance audits.
6. **Network Segmentation:** Separates internal zones (e.g., isolating a public-facing **DMZ** from the internal corporate database network).

---

## Types of Firewalls (Based on Filtering Mechanism)

| Type | OSI Layer | How It Works | Pros & Cons |
| :--- | :--- | :--- | :--- |
| **1. Packet Filtering Firewall (Stateless)** | Network (Layer 3) & Transport (Layer 4) | Inspects individual packet headers (Source/Dest IP, Port, Protocol) against static Access Control Lists (ACLs). | **Pro:** Very fast, low overhead.<br>**Con:** Cannot track connection state or inspect payload. |
| **2. Stateful Inspection Firewall** | Network (L3) & Transport (L4) | Maintains a **State Table** of active connections (e.g., TCP handshakes) and allows incoming packets only if they belong to an established session. | **Pro:** Much more secure than stateless filters.<br>**Con:** Higher memory/CPU usage; vulnerable to app-layer attacks. |
| **3. Circuit-Level Gateway** | Session (Layer 5) | Validates TCP/UDP session establishment (handshake) without inspecting packet contents; hides internal IP addresses. | **Pro:** Lightweight session validation.<br>**Con:** Does not inspect application data. |
| **4. Application-Level Gateway (Proxy Firewall)** | Application (Layer 7) | Acts as an intermediary proxy; terminates the client connection, inspects the full application payload (HTTP, FTP), and opens a new connection to the server. | **Pro:** Deepest visibility, hides internal topology.<br>**Con:** Higher latency and processing overhead. |
| **5. Next-Generation Firewall (NGFW)** | Layers 3–7 | Combines stateful inspection with **Deep Packet Inspection (DPI)**, Intrusion Prevention (IPS), application awareness, and TLS inspection. | **Pro:** Comprehensive modern threat defense.<br>**Con:** Expensive and complex to tune. |
| **6. Web Application Firewall (WAF)** | Application (Layer 7) | Specialized firewall protecting web apps/APIs from HTTP attacks like **SQL Injection**, **XSS**, and **CSRF**. | **Pro:** Stops web exploits.<br>**Con:** Specific to HTTP/HTTPS traffic. |

---

## Deployment Form Factors

* **Hardware Firewall:** Dedicated appliance or router-integrated device protecting an entire LAN perimeter.
* **Software (Host-Based) Firewall:** Installed on individual OS endpoints (e.g., Windows Defender Firewall, Linux `iptables`/`nftables`) to protect a single host.
* **Cloud / SaaS Firewall:** Cloud-hosted security edge protecting cloud VPCs, web apps, and remote users (e.g., Cloudflare WAF, AWS Network Firewall).

---

## References & Study Hints

* **GeeksforGeeks — Types of Network Firewall:** [https://www.geeksforgeeks.org/computer-networks/types-of-network-firewall/](https://www.geeksforgeeks.org/computer-networks/types-of-network-firewall/)
* **Exam Tip (5–10 Marks):** Draw the internal-vs-external perimeter diagram, list 4–5 clear reasons *why* firewalls are used, and explain the progression of types from **Packet Filtering** $\rightarrow$ **Stateful Inspection** $\rightarrow$ **Proxy/Application Gateway** $\rightarrow$ **NGFW/WAF**.
