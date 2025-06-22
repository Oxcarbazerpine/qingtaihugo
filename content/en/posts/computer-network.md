---
title: "Computer Networks"
date: 2024-06-01
draft: false
tags: ["Network"]
---

- Wangdao Postgraduate Exam
## Chapter 1: Computer Network Architecture
Can communicate with each other, but do not control each other  
Components: hardware, software, protocol  
Working mode:  
- Edge part: directly used by users  
- Core part: supports the edge  
Functions: data communication, resource sharing

### Classification
- Scope: WAN (Wide Area Network), MAN (Metropolitan Area Network), LAN (Local Area Network), PAN (Personal Area Network)
- Users: Public network, Private network
- Switching technology: Circuit switching, Message switching, Packet switching
- Transmission technology: Broadcast, Point-to-point

---

## Cisco Packet Tracer Simulation
### TCP/IP Four-Layer Protocol Architecture
- Data Link Layer: Physical data transmission and network card driver reading data
- Network Layer: Controls routing and forwarding of data packets
- Transport Layer: Controls end-to-end communication between computers
- Application Layer: Logic of various applications

Hub: A type of bus network, indiscriminate broadcasting and collisions  
Concepts: IP address, MAC address  
ARP Protocol: Address Resolution Protocol  
Belongs to the network layer. Maintains an ARP table recording IP addresses, MAC numbers, and network interfaces. When other protocols do not know the destination MAC address, they first send an ARP broadcast to inquire, update the table, and then try to send the original packet again.

---

## Top-Down Approach
### Intro
Broadband access:
- DSL (Digital Subscriber Line): multiplexing telephone lines
- Cable TV lines: fiber + coaxial cable
- FTTH: Fiber to the home
- Satellite link access
- WiFi: Wireless LAN access - modem - ISP
- Wide-area wireless access: 3G

Physical media:
- Twisted pair: two twisted copper wires, telephone lines, 10M~10G, high-speed LAN
- Coaxial cable: two concentric copper conductors, tens of MB
- Optical fiber: hundreds of GB, immune to electromagnetic interference, no attenuation over long distances, high cost
- Radio channel
- Satellite radio: 280ms delay, hundreds of Mbps

Packet switching:
- Store-and-forward in routers: cache the entire packet before forwarding, delay is 2L/R
- Queue delay: limited router cache causes packet loss
- Forwarding table: port IP and physical number

Circuit switching: reserve resources, circuit switching structure  
Sender and receiver first establish a direct circuit to ensure constant rate transmission.  
Each circuit switch reserves constant bandwidth for communication.
- FDM: Frequency-Division Multiplexing, fixed frequency bands
- TDM: Time-Division Multiplexing, each circuit is assigned a dedicated time slot in a TDM frame

Internet: network of networks
1. Tier 1 ISP - dozens
2. Regional ISPs - hundreds of thousands
3. Access ISPs

Delays: 1. Processing delay 2. Queueing delay 3. Transmission delay 4. Propagation delay  
Throughput: amount of bits transmitted per unit time, determined by the bottleneck link

---

## Five-Layer Protocol
1. Application Layer: HTTP, SMTP, FTP
2. Transport Layer: TCP, UDP
3. Network Layer: IP
4. Link Layer: Frame
5. Physical Layer

---

## Network Attacks
- DDoS: Distributed denial of service, massive requests from multiple sources occupy server resources
- SSL: Secure Sockets Layer, application-layer encryption enhancement for TCP, uses SSL library API

Protocol: reliable transmission, throughput, timing, security

---

## Application Layer
- HTTP
    - Persistent and non-persistent connections (default is persistent)
    - Round-Trip Time (RTT): TCP connection requires two RTTs + file transfer time
    - Request message: request line (method, URL, version), header lines, entity body (for POST)
    - Response message: similar structure, status codes (301, 400, 505, etc.), set-cookie, web cache, conditional GET (If-Modified-Since, 304 Not Modified)
- FTP
    - Two parallel TCP connections: control (port 21, out-of-band), data (port 20, new for each transfer)
    - Commands: USER, PASS, LIST, RETR, STOR
    - Responses: 331, 125, 425, 452
- SMTP: TCP-based, persistent connection, only PUSH
    - User agent, SMTP, sender server (port 25), SMTP, receiver server, {POP3, IMAP, HTTP}, receiver user agent
    - Commands: HELO, MAIL FROM, RCPT TO, DATA, QUIT
    - ASCII only, multimedia must be encoded
- Pulling mail
    - POP3: port 110, three phases (authorization, transaction, update), commands: user, pass, list, retr, dele, quit
    - IMAP: supports folders, query
    - HTTP
- DNS: Domain Name System, port 53, UDP-based
    - Distributed database + application-layer protocol
    - Functions: hostname to canonical name mapping, load balancing
    - Hierarchy: root, TLD, authoritative servers
    - Local DNS server: acts as proxy, forwards requests
    - Query process: recursive and iterative
    - DNS cache, records (A, NS, CNAME, MX), TTL

---

## P2P (Peer to Peer)
- File distribution: BitTorrent, tracker, rarest first, unchoked peers, periodic optimization
- Distributed Hash Table (DHT): key is hash of resource name, value is peer IP, ring structure, shortcuts, handling churn

---

## Transport Layer
- Extends host-to-host delivery to process-to-process (sockets)
- Multiplexing/demultiplexing
- UDP: minimal work, port numbers, error checking
- Reliable communication protocols: stop-and-wait, pipelining (Go-Back-N, Selective Repeat)
- TCP: three-way handshake, MSS, segment structure, cumulative ACK, timeout/retransmission, fast retransmit, flow control (rwnd), connection establishment/termination, SYN flood attack and SYN cookie, RST flag, congestion control (slow start, congestion avoidance, fast recovery), AIMD, fairness

---

## Network Layer
- Router functions: forwarding, routing
- IP protocol: best-effort
- Connection-oriented (Virtual Circuit) vs. connectionless (Datagram)
- Router architecture: input/output ports, switching fabric (memory, bus, crossbar), output buffering, HOL blocking
- IPv4 format, fragmentation, MTU, addressing (dotted-decimal, subnet mask, CIDR, address aggregation), DHCP, NAT, UPnP
- ICMP: ping, traceroute
- IPv6: format, flow label, no header checksum, no fragmentation in routers, dual-stack, tunneling, IPsec

---

## Routing Algorithms
- Global (Link State) vs. decentralized (Distance Vector)
- Dijkstra, distance vector, count-to-infinity, poison reverse
- Autonomous Systems (AS), intra-AS (RIP, OSPF), inter-AS (BGP), AS-PATH, NEXT-HOP, route selection, policy-based routing
- Broadcast and multicast routing: flooding, spanning tree, RPF, pruning, DVMRP, PIM, IGMP

---

## Link Layer
- Services: framing, MAC, reliable delivery, error detection/correction (parity, checksum, CRC)
- Multiple access: point-to-point (PPP, HDLC), broadcast (TDM, FDM, CDMA, random access, CSMA/CD, token passing)
- DOCSIS: cable access, CMTS, FDM/TDM, MAP messages

---

## Switched LANs
- Link-layer addressing (MAC), ARP, Ethernet (frame structure, preamble, CRC), standards (10BASE-T, etc.), CSMA/CD
- Switches: plug-and-play, switch table, self-learning, filtering/forwarding, aging, collision elimination, link isolation, switch sniffing, poisoning
- Switch vs. router: layer 2 vs. layer 3, plug-and-play, efficiency, broadcast storms, spanning tree

---

## VLANs
- Port-to-VLAN mapping, inter-VLAN communication (router), trunking, VLAN tags (TPID, VLAN ID, priority)

---

## Link Layer Virtualization
- MPLS: label switching, between layer 2 and 3, label-switched routers, traffic engineering, VPN

---

## Data Center Networks
- Blades, racks, TOR switches, border routers, load balancing, multi-level topology, MDC (modular data center)

---

## Wireless and Mobile Networks
- Concepts: base station, handoff, infrastructure-based/ad-hoc, single/multi-hop
- Wireless link characteristics: path loss, interference, multipath, SNR, BER, hidden terminal, fading
- CDMA: chipping rate, encoding/decoding
- WiFi (802.11): BSS, AP, SSID, channels, association, authentication, MAC protocol (CSMA/CA, ACK, RTS/CTS), frame structure, mobility within subnet, rate adaptation, power management
- Bluetooth (802.15.1): WPAN, piconet, master/slave, FHSS
- ZigBee (802.15.4): low power, master/slave
- Cellular networks: licensed bands, 1G/2G/3G/4G, BTS, FDM/TDM, MSC, GPRS, LTE, OFDM

---

## Mobility Management
- Home/visited network, COA, indirect/direct routing, Mobile IP, agent advertisement/solicitation, registration
- Cellular mobility: HLR, GMSC, VLR, call routing, handoff, TCP over wireless

---

## Multimedia Networking
- Applications: video, audio, streaming, VoIP
- Streaming: client buffering, UDP/TCP, DASH, CDN, cluster selection
- VoIP: delay jitter, playback strategies, FEC, interleaving, error concealment, relaying
- RTP: header, timestamp, SSRC
- SIP: session initiation, registration

---

## Network Support for Multimedia
- Best-effort, differentiated services, per-connection QoS
- Scheduling: FIFO, priority, round robin, WFQ
- Policing: leaky bucket, token bucket
- Diffserv, QoS, call admission

---

## Network Security
- Confidentiality, integrity, authentication, operational security, attacks
- Cryptography: symmetric (Caesar, substitution, polyalphabetic, stream/block ciphers, CBC), public key (RSA), hash functions (MD5, SHA-1), MAC, digital signature, public key certification (CA)
- Endpoint authentication: nonce, replay attack prevention
- Secure email: confidentiality, authentication, integrity, PGP
- SSL/TLS: handshake, key derivation, record, truncation attack
- IPsec/VPN: AH, ESP, SA, transport/tunnel mode, IKE
- Wireless LAN security: WEP, 802.11i, EAP, PMK, TK
- Firewalls: packet filter, stateful, application gateway, proxy, IDS/IPS (signature/anomaly-based)

---

## Network Management
- Object identifier