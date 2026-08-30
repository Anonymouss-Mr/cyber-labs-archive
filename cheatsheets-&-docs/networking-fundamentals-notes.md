# CCNA 200-301 Topic Extraction and Study Guide

This document presents a structured and comprehensive extraction of key networking topics sourced directly from the **CCNA 200-301 Course Notes (by Mahmoud Tarek)**.

---

## Table of Contents
1. [Network Topologies](#1-network-topologies)
2. [TCP/IP Model](#2-tcpip-model)
3. [OSI Model](#3-osi-model)
4. [UDP (User Datagram Protocol)](#4-udp-user-datagram-protocol)
5. [VLAN (Virtual Local Area Network)](#5-vlan-virtual-local-area-network)
6. [Port Numbers](#6-port-numbers)
7. [Headers and Encapsulation](#7-headers-and-encapsulation)
8. [Application Layer Services](#8-application-layer-services)
9. [Transport Layer](#9-transport-layer)
10. [IPv4 Basics](#10-ipv4-basics)
11. [Fixed Subnetting (FLSM)](#11-fixed-subnetting-flsm)
12. [VLSM & Private IPv4 Addressing](#12-vlsm--private-ipv4-addressing)
13. [IP Header & ARP Protocol](#13-ip-header--arp-protocol)
14. [Router Passwords & Security](#14-router-passwords--security)
15. [Telnet vs. SSH](#15-telnet-vs-ssh)
16. [DHCPv4 and DHCPv6](#16-dhcpv4-and-dhcpv6)
17. [Access Control Lists (ACL)](#17-access-control-lists-acl)
18. [Network Address Translation (NAT)](#18-network-address-translation-nat)
19. [Building the MAC Address Table](#19-building-the-mac-address-table)
20. [VLAN Trunking Protocols (DTP & VTP)](#20-vlan-trunking-protocols-dtp--vtp)
21. [VLAN Hopping Attacks & Voice VLANs](#21-vlan-hopping-attacks--voice-vlans)
22. [Spanning Tree Protocol (STP)](#22-spanning-tree-protocol-stp)
23. [AAA Server (Authentication, Authorization, Accounting)](#23-aaa-server-authentication-authorization-accounting)
24. [IEEE 802.1X (Dot1x) Port-Based Authentication](#24-ieee-8021x-dot1x-port-based-authentication)
25. [Wi-Fi Technology Fundamentals](#25-wi-fi-technology-fundamentals)
26. [Virtual Private Network (VPN) Concepts](#26-virtual-private-network-vpn-concepts)
27. [Syslog Logging System](#27-syslog-logging-system)
28. [References](#28-references)

---

## 1. Network Topologies

Network topology defines the structural arrangement of various elements (links, nodes, etc.) in a computer network. Topologies are analyzed from two perspectives:
* **Physical Topology:** The physical lay of wires, cables, and network equipment.
* **Logical Topology:** The path data travels through the physical setup.

### Core Topologies
1. **Bus Topology:**
   * Nodes are connected to a single central coaxial cable terminated at both ends to prevent signal reflection (loops).
   * **Collision Resolution:** Uses **CSMA/CD** (*Carrier Sense Multiple Access with Collision Detection*):
     * Device performs Carrier Sense (listens to the line).
     * If clear, it transmits; if a collision occurs, devices transmit a **Jam Signal** and pause for a random backoff time.
2. **Star Topology:**
   * All nodes connect to a central device (Hub or Switch).
   * **Hub-based Star:** Physical Star, Logical Bus (floods data to all ports; prone to collisions).
   * **Switch-based Star:** Physical Star, Logical Star (frames are forwarded selectively using a dynamic MAC address table).
3. **Ring Topology:**
   * Devices are connected in a circular loop. Data travels in one direction (or dual ring for redundancy, e.g., FDDI).
4. **Mesh Topology:**
   * Devices are interconnected redundantly.
   * **Full Mesh:** Every device connects to every other device ($N(N-1)/2$ links). Provides high availability and fault tolerance.

---

## 2. TCP/IP Model

The TCP/IP (Transmission Control Protocol/Internet Protocol) suite is the practical framework used across the modern Internet.

### Layer Comparison

| TCP/IP Standard Layer | TCP/IP Updated Layer | Primary Protocol Examples | Data Format (PDU) |
| :--- | :--- | :--- | :--- |
| **Application** | Application | HTTP, HTTPS, FTP, SSH, DNS, DHCP, SMTP | Data |
| **Transport** | Transport | TCP, UDP | Segment / Datagram |
| **Internet** | Network | IPv4, IPv6, ICMP, ARP, OSPF | Packet |
| **Network Access** | Data Link | Ethernet (802.3), Wi-Fi (802.11) | Frame |
| **Network Access** | Physical | Copper (UTP/STP), Fiber Optic, Radio Waves | Bits |

---

## 3. OSI Model

The **Open Systems Interconnection (OSI)** model is a standard conceptual framework created by the ISO (International Organization for Standardization) to enable interoperability across vendors.

### The 7 Layers of OSI

+-------------------------------------------------------+
|  Layer 7: Application  (User Services / Data Format)  |
+-------------------------------------------------------+
|  Layer 6: Presentation (Encoding, Encryption, Compression)
+-------------------------------------------------------+
|  Layer 5: Session      (Dialog Management, Control)   |
+-------------------------------------------------------+
|  Layer 4: Transport    (End-to-End, TCP/UDP, Ports)     |
+-------------------------------------------------------+
|  Layer 3: Network      (Logical Addressing, Routing)   |
+-------------------------------------------------------+
|  Layer 2: Data Link    (Physical Addressing, Switches) |
+-------------------------------------------------------+
|  Layer 1: Physical    (Bits, Cabling, Signals)        |
+-------------------------------------------------------+


1. **Application (Layer 7):** Provides software interfaces for communications (HTTP, FTP, SMTP).
2. **Presentation (Layer 6):** Handles data conversion, formatting, compression, and encryption/decryption (ASCII, JPEG, MP4).
3. **Session (Layer 5):** Establishes, maintains, terminates, and synchronizes active sessions between host applications.
4. **Transport (Layer 4):** End-to-end reliable or unreliable delivery, flow control (windowing), and segmentation.
5. **Network (Layer 3):** Handles logical IP addressing, path determination (routing tables), and packet forwarding.
6. **Data Link (Layer 2):** Physical hardware control, media access control (MAC addressing), frame formatting, split into:
   * **MAC (Media Access Control):** Hardware framing and channel access methods.
   * **LLC (Logical Link Control):** Interface to Layer 3 and multiprotocol identification.
7. **Physical (Layer 1):** Converts frames into physical signals (electrical pulses, optical signals, or RF waves) for transport over media.

---

## 4. UDP (User Datagram Protocol)

UDP is a lightweight, connectionless Transport Layer (Layer 4) protocol defined in RFC 768.

### Key Characteristics
* **Connectionless:** Transmits datagrams without establishing a prior dynamic handshaking state.
* **Unreliable / Best-Effort Delivery:** Does not guarantee delivery, order, or error recovery (retransmission).
* **Low Overhead:** Header size is fixed at **8 bytes** (compared to 20-60 bytes in TCP).
* **Speed:** Used where real-time speed is critical over error checking (e.g., VoIP, Video Streaming, DNS queries, DHCP, TFTP).

### UDP Header Structure (8 Bytes Total)
1. **Source Port** (16 bits)
2. **Destination Port** (16 bits)
3. **Length** (16 bits)
4. **Checksum** (16 bits)

---

## 5. VLAN (Virtual Local Area Network)

A Virtual Local Area Network (VLAN) logically segments a physical Local Area Network into distinct broadcast domains regardless of the physical location of hosts.

### Benefits of VLANs
* **Broadcast Containment:** Reduces broadcast domain boundary size.
* **Enhanced Security:** Isolates sensitive groups/departments at Layer 2.
* **Cost Efficiency:** Reduces unnecessary hardware deployment.

### Port Types
* **Access Port:** Connects end-host systems (PCs, Printers). Belongs to a single tagged/untagged native VLAN.
* **Trunk Port:** Connects switches or routers. Multiplexes traffic for multiple VLANs over a single link using frame tagging (IEEE 802.1Q).

---

## 6. Port Numbers

Port numbers operate at the Transport Layer (Layer 4) to identify specific services or applications on a destination node.

### Port Number Ranges ($0 - 65535$)
* **Well-Known Ports ($0 - 1023$):** Reserved for standard network systems and applications.
* **Registered Ports ($1024 - 49151$):** Assigned by IANA for specific user-installed software/vendor applications.
* **Dynamic/Private Ports ($49152 - 65535$):** Ephemeral ports assigned dynamically by client operating systems for temporary outgoing connections.

### Common Port Map
* **FTP:** Ports 20 (Data), 21 (Control)
* **SSH:** Port 22
* **Telnet:** Port 23
* **SMTP:** Port 25
* **DNS:** Port 53 (UDP/TCP)
* **DHCP:** Ports 67 (Server), 68 (Client)
* **HTTP:** Port 80
* **POP3:** Port 110
* **NTP:** Port 123
* **IMAP:** Port 143
* **SNMP:** Port 161
* **HTTPS:** Port 443

---

## 7. Headers and Encapsulation

**Encapsulation** is the process where upper-layer protocol data units (PDUs) are wrapped in headers and trailers as data travels down the stack.

+-------------------------------------------------------------------------------+
| Layer 4 (Transport)   | [L4 Header (Ports)] + [Data]                         |
+-------------------------------------------------------------------------------+
| Layer 3 (Network)     | [L3 Header (IP Addresses)] + [L4 Segment]            |
+-------------------------------------------------------------------------------+
| Layer 2 (Data Link)   | [L2 Header (MACs)] + [L3 Packet] + [L2 Trailer (FCS)]|
+-------------------------------------------------------------------------------+
| Layer 1 (Physical)    | 011010010101011101... (Bits on the Wire)             |
+-------------------------------------------------------------------------------+


* **Data Unit Terminology:**
  * **Application:** Data
  * **Transport:** Segment (TCP) / Datagram (UDP)
  * **Network:** Packet
  * **Data Link:** Frame
  * **Physical:** Bits

---

## 8. Application Layer Services

1. **DNS (Domain Name System):**
   * Resolves domain names (e.g., `google.com`) into IP addresses (and vice versa).
   * **Lookup Types:** *Recursive* (resolver complete resolution) vs. *Iterative* (referral queries).
2. **HTTP / HTTPS:**
   * Transfers hypermedia documents. HTTPS adds security via SSL/TLS encryption over port 443.
3. **FTP / SFTP / TFTP:**
   * **FTP:** Dual-channel connection (Ports 20/21) for moving files. Unencrypted.
   * **SFTP:** SSH-secured file transfer.
   * **TFTP:** UDP-based (Port 69) connectionless simple file delivery (e.g., Cisco IOS backup).
4. **Email Services (SMTP, POP3, IMAP):**
   * **SMTP:** Sends mail between clients and servers or between servers.
   * **POP3:** Downloads emails from a server to a local client, typically deleting them from the server.
   * **IMAP:** Syncs email folders dynamically between client and server.

---

## 9. Transport Layer

The Transport Layer manages session-oriented end-to-end data delivery control, multiplexing, and windowing.

### TCP vs. UDP Comparison

| Feature | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Connection Type** | Connection-Oriented (3-way handshake) | Connectionless |
| **Reliability** | High (ACKs, retransmissions) | Best-effort |
| **Header Size** | 20–60 Bytes | 8 Bytes |
| **Flow Control** | Yes (Dynamic Sliding Window) | None |
| **Speed** | Lower (due to state maintenance) | High speed / Real-time |

### TCP Three-Way Handshake
Client                      Server
|           SYN             |
|-------------------------->|
|         SYN-ACK           |
|<--------------------------|
|           ACK             |
|-------------------------->|


---

## 10. IPv4 Basics

IPv4 uses a **32-bit** binary address represented in dotted-decimal notation consisting of 4 octets ($8\text{ bits}\times 4 = 32\text{ bits}$).

### Legacy IPv4 Classes

| Class | First Octet Range | Default Subnet Mask | Fixed Bits | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **A** | $1 - 127$ | `255.0.0.0` (/8) | `0` | Very Large Networks |
| **B** | $128 - 191$ | `255.255.0.0` (/16) | `10` | Medium/Large Networks |
| **C** | $192 - 223$ | `255.255.255.0` (/24) | `110` | Small Local Networks |
| **D** | $224 - 239$ | Undefined | `1110` | Multicast Applications |
| **E** | $240 - 255$ | Undefined | `1111` | Experimental / Research |

*Special Note:* Address `127.0.0.1` is universally reserved for local loopback testing.

---

## 11. Fixed Subnetting (FLSM)

Fixed-Length Subnet Masking (FLSM) divides a parent network space into smaller subnets of equal size.

### Calculation Formulae
* **Total Host IPs per Subnet:** $2^n$ ($n = \text{number of host bits}$)
* **Usable Host IPs per Subnet:** $2^n - 2$ (Subtracts 1 for Network ID, 1 for Broadcast ID)
* **Block Size (Increment):** $256 - \text{Interesting Octet Subnet Mask}$

### Example Walkthrough
* **Target:** Divide `192.168.1.0/24` into blocks supporting at least 15 usable hosts each.
* **Equation:** $2^n - 2 \ge 15 \implies 2^5 - 2 = 30 \text{ usable hosts } (n = 5)$.
* **Host Bits ($n$):** 5 bits.
* **Network Prefix:** $32 - 5 = /27$ (`255.255.255.224`).
* **Block Size:** $256 - 224 = 32$.
* **Subnets:**
  1. `192.168.1.0/27` (Usable: `.1` to `.30`, Broadcast: `.31`)
  2. `192.168.1.32/27` (Usable: `.33` to `.62`, Broadcast: `.63`)
  3. `192.168.1.64/27` (Usable: `.65` to `.94`, Broadcast: `.95`)

---

## 12. VLSM & Private IPv4 Addressing

### Variable-Length Subnet Masking (VLSM)
VLSM allows network administrators to customize subnet masks based on differing requirements across subnets, preventing IP address exhaustion.

### RFC 1918 Private Address Ranges
These addresses are non-routable over the public Internet:

| Class | Private Address Range | Total IP Scope |
| :--- | :--- | :--- |
| **A** | `10.0.0.0` to `10.255.255.255` | 1 Class A (`/8`) |
| **B** | `172.16.0.0` to `172.31.255.255` | 16 Class B networks (`/12`) |
| **C** | `192.168.0.0` to `192.168.255.255` | 256 Class C networks (`/16`) |
| **APIPA** | `169.254.0.0` to `169.254.255.255` | Automatic fallback link-local scope |

---

## 13. IP Header & ARP Protocol

### IPv4 Header Structure
Standard IPv4 headers range from **20 to 60 bytes**:
* **Version (4 bits):** Set to `4`.
* **IHL (4 bits):** Internet Header Length.
* **TTL (Time to Live - 8 bits):** Prevents packets from looping infinitely across routers by decrementing at each hop.
* **Protocol (8 bits):** Indicates upper-layer payload (e.g., 6 = TCP, 17 = UDP, 1 = ICMP).
* **Source & Destination IP Addresses:** 32 bits each.

### ARP (Address Resolution Protocol)
ARP dynamically resolves a known Layer 3 IPv4 address to a Layer 2 MAC address.

Host A (10.0.0.1)                                   Host B (10.0.0.2)
|  ARP Request (Broadcast: FF:FF:FF:FF:FF:FF)      |
|------------------------------------------------->|
|  ARP Reply (Unicast: Host B MAC)                 |
|<-------------------------------------------------|


* **GARP (Gratuitous ARP):** Unsolicited broadcast ARP used to update neighbor ARP caches or detect IP conflicts.

---

## 14. Router Passwords & Security

Securing device access on Cisco routers and switches:

### Passwords Configuration
* **Console Security:**
  ```text
  Router(config)# line console 0
  Router(config-line)# password SecretConsolePass
  Router(config-line)# login
Privileged EXEC Mode (Secret vs. Password):

enable password sets plaintext fallback (insecure).

enable secret secures access with an MD5/scrypt hash.

Router(config)# enable secret StronglyEncryptedPass

Service Password Encryption:
Converts all plain text stored passwords into weak type-7 reversible encryptions:

Router(config)# service password-encryption

15. Telnet vs. SSHFeatureTelnetSSH (Secure Shell)Port23 (TCP)22 (TCP)SecurityPlaintext transmission (Insecure)Strong cryptographic encryptionAuthenticationBasic credentialsCryptographic key pairs / PasswordSSH Setup WalkthroughPlaintextRouter(config)# hostname R1
R1(config)# ip domain-name lab.local
R1(config)# crypto key generate rsa modulus 2048
R1(config)# username admin privilege 15 secret AdminPass123
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local

## 16. DHCPv4 and DHCPv6

Dynamic Host Configuration Protocol automates network parameter distribution (IP, Subnet Mask, Gateway, DNS).

### DHCPv4 DORA Process
1. **Discover:** Client sends a broadcast request to locate a server.
2. **Offer:** DHCP Server offers configuration parameters.
3. **Request:** Client accepts and requests the offered IP parameter set.
4. **Acknowledge (ACK):** Server confirms lease allocation.

### DHCPv6 Variations
* **SLAAC (Stateless Address Autoconfiguration):** Routers supply network prefixes via Router Advertisements (RA); hosts self-generate interface IDs.
* **Stateless DHCPv6:** SLAAC provides IP prefix/gateway; DHCPv6 provides supplemental parameters (DNS list).
* **Stateful DHCPv6:** DHCPv6 handles IP address distribution directly (similar to DHCPv4).

---

## 17. Access Control Lists (ACL)

ACLs are sequential rule tables used by routers to permit or deny network traffic based on addresses, protocols, or ports.

### ACL Categories

| Type | Range | Evaluation Scope | Ideal Placement |
| :--- | :--- | :--- | :--- |
| **Standard ACL** | 1–99 & 1300–1999 | Inspects Source IP Address only | Closest to Destination |
| **Extended ACL** | 100–199 & 2000–2699 | Source/Dest IP, Protocol, Port Numbers | Closest to Source |

### Implementation Commands
```text
! Standard ACL Example
Router(config)# access-list 10 permit 192.168.1.0 0.0.0.255
Router(config)# interface g0/0/0
Router(config-if)# ip access-group 10 in

! Extended ACL Example
Router(config)# ip access-list extended BLOCK_HTTP
Router(config-ext-nacl)# deny tcp 192.168.1.0 0.0.0.255 host 10.0.0.5 eq 80
Router(config-ext-nacl)# permit ip any any

## 16. DHCPv4 and DHCPv6

Dynamic Host Configuration Protocol automates network parameter distribution (IP, Subnet Mask, Gateway, DNS).

### DHCPv4 DORA Process
1. **Discover:** Client sends a broadcast request to locate a server.
2. **Offer:** DHCP Server offers configuration parameters.
3. **Request:** Client accepts and requests the offered IP parameter set.
4. **Acknowledge (ACK):** Server confirms lease allocation.

### DHCPv6 Variations
* **SLAAC (Stateless Address Autoconfiguration):** Routers supply network prefixes via Router Advertisements (RA); hosts self-generate interface IDs.
* **Stateless DHCPv6:** SLAAC provides IP prefix/gateway; DHCPv6 provides supplemental parameters (DNS list).
* **Stateful DHCPv6:** DHCPv6 handles IP address distribution directly (similar to DHCPv4).

---

## 17. Access Control Lists (ACL)

ACLs are sequential rule tables used by routers to permit or deny network traffic based on addresses, protocols, or ports.

### ACL Categories

| Type | Range | Evaluation Scope | Ideal Placement |
| :--- | :--- | :--- | :--- |
| **Standard ACL** | 1–99 & 1300–1999 | Inspects Source IP Address only | Closest to Destination |
| **Extended ACL** | 100–199 & 2000–2699 | Source/Dest IP, Protocol, Port Numbers | Closest to Source |

### Implementation Commands
```text
! Standard ACL Example
Router(config)# access-list 10 permit 192.168.1.0 0.0.0.255
Router(config)# interface g0/0/0
Router(config-if)# ip access-group 10 in

! Extended ACL Example
Router(config)# ip access-list extended BLOCK_HTTP
Router(config-ext-nacl)# deny tcp 192.168.1.0 0.0.0.255 host 10.0.0.5 eq 80
Router(config-ext-nacl)# permit ip any any

18. Network Address Translation (NAT)
NAT maps private, non-routable IP addresses to public IPs, helping conserve IPv4 space and securing internal topologies.

Primary NAT Types
Static NAT: 1-to-1 permanent mapping between an internal private IP and an external public IP.

Dynamic NAT: Dynamic many-to-many allocation from an assigned pool of public IPs.

PAT (Port Address Translation / NAT Overload): Maps multiple internal private IPs to a single public IP using unique source port numbers.

19. Building the MAC Address Table
Switches maintain a CAM (Content Addressable Memory) Table or MAC Address Table to map physical switch ports to connected MAC addresses.

Learning and Forwarding Logic
Frame Arrival: Inspects incoming Frame Source MAC Address:

If not listed, the switch maps the Source MAC to the receiving Port with a standard 300-second aging timer.

Forwarding Lookup: Inspects Frame Destination MAC Address:

Unicast Known: Forwards directly out the associated port.

Unicast Unknown / Broadcast / Multicast: Floods the frame out all active switch interfaces except the ingress interface.

20. VLAN Trunking Protocols (DTP & VTP)
Dynamic Trunking Protocol (DTP)
Cisco proprietary point-to-point protocol that automatically negotiates dynamic trunk links between switches.

Modes: Access, Trunk, Dynamic Auto (listens, defaults to access), Dynamic Desirable (actively negotiates trunk).

VLAN Trunking Protocol (VTP)
Centralizes VLAN database management across connected Cisco switches.

VTP Modes:

Server: Creates, edits, deletes, and advertises VLAN configurations.

Client: Receives and applies VLAN updates from servers; cannot modify VLANs locally.

Transparent: Does not synchronize its local database with advertisements, but forwards updates to downstream switches.

21. VLAN Hopping Attacks & Voice VLANs
VLAN Hopping Attack Types
Switch Spoofing: An attacker auto-negotiates a trunk link with a switch port set to Dynamic Auto or Dynamic Desirable using rogue DTP frames.

Mitigation: Explicitly set user ports to access mode (switchport mode access) and disable DTP (switchport nonegotiate).

Double Tagging: An attacker crafts a frame with two 802.1Q tags matching the native VLAN to bypass switch tagging restrictions.

Mitigation: Change the default native VLAN (VLAN 1) to an unused VLAN ID across all trunk interfaces.

Voice VLAN Configuration
Separates real-time IP phone media traffic onto an isolated high-priority VLAN.

Switch(config)# vlan 10
Switch(config-vlan)# name DATA_VLAN
Switch(config)# vlan 20
Switch(config-vlan)# name VOICE_VLAN
Switch(config)# interface FastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# switchport voice vlan 20

22. Spanning Tree Protocol (STP)IEEE 802.1D Spanning Tree Protocol eliminates Layer 2 switching loops in redundant topologies by blocking redundant paths.STP Port Roles and StatesBridge Protocol Data Units (BPDUs): Control frames exchanged to elect the Root Bridge (lowest Bridge ID = Priority + MAC Address).Port Roles: Root Port (RP), Designated Port (DP), Alternate/Blocked Port (AP).Port States: Blocking $\rightarrow$ Listening $\rightarrow$ Learning $\rightarrow$ Forwarding.PortFast EnhancementConfigured on edge access ports to bypass listening/learning states and immediately transition ports to forwarding, preventing DHCP timeouts on connected hosts.23. AAA Server (Authentication, Authorization, Accounting)AAA provides a centralized framework for securing network access control across infrastructure devices:

[ User/Admin ] <---> [ Network Access Device (NAD) ] <---> [ AAA Server (ISE/RADIUS) ]

Authentication: Verifies user identity credentials ("Who are you?").

Authorization: Defines permitted commands and execution privileges ("What are you allowed to do?").

Accounting: Logs user sessions, commands, and activity duration ("What did you do and when?").

Protocols: TACACS+ (Cisco proprietary, encrypts full packet payload, TCP port 49) vs. RADIUS (Open standard, encrypts password only, UDP ports 1812/1813).

24. IEEE 802.1X (Dot1x) Port-Based Authentication
IEEE 802.1X is a network access control protocol that prevents unauthorized devices from accessing a LAN until authentication is completed.

Key Roles
Supplicant: The client endpoint requesting access (e.g., a PC running 802.1X software).

Authenticator: The network device (Switch/WLC) controlling physical access to the network.

Authentication Server: Centralized database server (e.g., RADIUS/Cisco ISE) that validates user credentials.

25. Wi-Fi Technology Fundamentals
Wireless local area networking (WLAN) based on IEEE 802.11 standards.

Wireless Frequencies
2.4 GHz Band: Longer range, better wall penetration, but high congestion (Channels 1, 6, and 11 are non-overlapping).

5 GHz Band: Higher throughput, shorter range, larger non-overlapping channel availability.

Architecture Components
Autonomous AP: Standalone access point managing its own security and radio policies.

Lightweight AP (LAP) & WLC: LAPs offload management processing to a centralized Wireless LAN Controller (WLC) via CAPWAP tunnels.

26. Virtual Private Network (VPN) Concepts
VPN technology creates encrypted communication channels (tunnels) across public networks such as the Internet.

Security Objectives
Confidentiality: Encrypts data payload (AES, 3DES).

Data Integrity: Ensures packet payload remains unaltered in transit (HMAC, SHA).

Authentication: Verifies endpoint identities (Pre-Shared Keys, Digital Certificates).

Anti-Replay: Uses packet sequence tracking to block intercepted data retransmissions.

Implementation Methods
Site-to-Site VPN: Connects static branch offices over IPsec tunnels.

Remote Access VPN: Connects individual mobile users using software clients (e.g., Cisco AnyConnect over SSL/IPsec).

GRE over IPsec: Wraps multiprotocol or multicast traffic (like routing updates) in a Generic Routing Encapsulation (GRE) header before passing through an IPsec tunnel.

27. Syslog Logging System
Syslog is a standard protocol (UDP port 514) used to send log messages to a centralized monitoring server.

Severity Levels (0 - 7)
Memory mnemonic: "Every Alert System Can Always Give Increased Debugging"

------- ------------- ---------------------------------------
   0    Emergency     System is unusable
   1    Alert         Action must be taken immediately
   2    Critical      Critical conditions
   3    Error         Error conditions
   4    Warning       Warning conditions
   5    Notice        Normal but significant condition
   6    Informational Informational messages
   7    Debugging     Detailed output for troubleshooting
Basic ConfigurationPlaintextRouter(config)# logging host 192.168.1.100
Router(config)# logging trap warning
Router(config)# logging source-interface g0/0
28. References Ahmed Adel. CCNA 200-301 Full Course Notes (V1).Cisco Systems, Inc. CCNA 200-301 Official Cert Guide, Volume 1 & Volume 2.
