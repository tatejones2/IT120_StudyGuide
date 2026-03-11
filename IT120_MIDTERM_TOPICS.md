# IT 120 Midterm Study Guide - Topics by Importance

**This guide is organized by the instructor's list of topics most likely to appear on the midterm.**

---

## 🔴 HIGHEST PRIORITY - Physical & Data Link Layer Focus

### 1. Access Methods: CSMA/CD vs CSMA/CA

#### CSMA/CD (Carrier Sense Multiple Access with Collision Detection)
- **Used in**: Wired Ethernet networks
- **How it works**:
  1. Device listens to medium (carrier sense)
  2. If medium is clear, transmits data
  3. While transmitting, listens for collisions
  4. If collision detected, stops transmission and waits random time before retrying
  5. Exponential backoff: Wait time increases with each retry

#### CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)
- **Used in**: Wireless (802.11) networks
- **Why different**: Can't detect collisions in wireless (hidden node problem)
- **How it works**:
  1. Device listens to medium
  2. If clear, waits a random time (backoff period)
  3. Transmits data
  4. Waits for ACK (acknowledgment) from receiver
  5. If no ACK received, assumes collision and retries
  6. **RTS/CTS**: Optional handshake before transmission to avoid hidden node problem

**Key Difference**: CD detects after collision; CA avoids collision before it happens

---

### 2. Address Resolution Protocol (ARP)

#### Purpose
Maps IP addresses to MAC addresses on local network

#### How ARP Works (4 Steps)
1. **Device A needs to send to Device B** (knows IP, needs MAC)
2. **ARP Request (broadcast)**: "Who has IP 192.168.1.10? Tell 192.168.1.5"
   - Sent to MAC address FF:FF:FF:FF:FF:FF (broadcast)
   - All devices on LAN receive it
3. **Device B recognizes its own IP**
4. **ARP Reply (unicast)**: Device B responds with its MAC address directly to Device A

#### ARP Table/Cache
- Each device maintains ARP table: IP → MAC mappings
- Entries expire after 15-20 minutes
- Can be viewed: `arp -a` (Windows/Mac) or `arp -A` (Linux)

#### ARP Poisoning (Security Risk)
- Attacker sends fake ARP replies
- Can intercept traffic between devices
- Mitigation: Static ARP entries, ARP filtering

---

### 3. Broadband vs Baseband

#### Baseband
- **Definition**: Uses entire bandwidth of cable for single signal
- **Signal Type**: Digital
- **Distance**: Limited (Ethernet ~100 meters)
- **Examples**: Traditional Ethernet (10BaseT, 100BaseT), Local Area Networks
- **Multiple Users**: Time-division (take turns using cable)
- **Bidirectional**: Half-duplex (one direction at a time)

#### Broadband
- **Definition**: Divides bandwidth into multiple channels/frequencies
- **Signal Type**: Analog or digital
- **Distance**: Longer distances possible
- **Examples**: Cable TV, DSL, Cable modems
- **Multiple Users**: Frequency-division (each gets own frequency)
- **Bidirectional**: Can support full-duplex (both directions simultaneously)
- **Requires**: Modem to convert analog ↔ digital

**Key Takeaway**: Baseband = one signal, simple; Broadband = multiple signals, complex but longer distances

---

### 4. Network Topologies - Comprehensive Comparison

| Topology | Physical Layout | Data Flow | Pros | Cons |
|----------|-----------------|-----------|------|------|
| **Point-to-Point** | Two devices directly connected | Direct | Simple, private, secure | Not expandable, limited |
| **Bus** | Single cable line | All on cable | Easy install, low cable | Not fault tolerant, EMI limits, all see traffic |
| **Ring** | Circular cable | Around circle | Easy install/reconfig | Not fault tolerant, all see traffic, no expansion |
| **Star (Hub)** | Central hub | Hub to each | Fault tolerant per device, easy | Central point failure, expensive, harder to redesign |
| **Star-Bus** | Looks star, acts bus | Via hub | Most common, combines benefits | Central hub failure |
| **Star-Ring** | Looks star, acts ring | Via hub ring | Ring benefits in star form | Central hub failure |
| **Mesh (Full)** | Every to every | Direct paths | Most fault tolerant, dedicated links | Expensive, n(n-1)/2 connections |
| **Mesh (Partial)** | At least 2 redundant | Multiple paths | Robust, less expensive than full | Still costly |
| **Point-to-Multipoint** | Hub-spoke with intelligent hub | Through hub | Hub managed, private | Hub capacity limits network |

#### Key Concept: Fault Tolerance
- **Ring & Bus**: One failure breaks network (not fault tolerant)
- **Star**: One link failure = one device down, others fine
- **Mesh**: Multiple redundant paths, most fault tolerant

---

### 5. Media (Mediums) - Comprehensive Comparison

| Medium | Speed | Distance | EMI Proof | Cost | Pros | Cons |
|--------|-------|----------|-----------|------|------|------|
| **Coaxial** | Varies | 100-500m | Shielded | Low-Med | Good shielding, used for video | Limited speeds, bulky |
| **Twisted Pair (UTP)** | 100Mbps-10Gbps | ~100m | No | Low | Most common, cheap, flexible | EMI sensitive, limited distance |
| **Twisted Pair (STP)** | 100Mbps-10Gbps | ~100m | Yes | Med-High | Shielded from EMI | More expensive, harder to work with |
| **Fiber-Optic (MMF)** | 1-10 Gbps | ~2km | Yes | High | Long distance, immune to EMI, secure | Expensive, requires special equipment, fragile |
| **Fiber-Optic (SMF)** | 10+ Gbps | 10+ km | Yes | High | Longest distance, fastest | Very expensive, requires lasers, specialized training |
| **Wireless (WiFi)** | 54Mbps-11Gbps | 30-100m | No | Low | Flexible, mobile, no cabling | Interference, security risk, shared medium |

#### Fiber-Optic Details
- **Multimode (MMF)**: Uses LEDs, good up to 2km, lower cost
- **Single-mode (SMF)**: Uses lasers, 10+ km, higher cost
- **Core/Cladding**: 62.5/125 μm is most common

---

### 6. Broadcast vs Collision Domains

#### Broadcast Domain
- **Definition**: Set of devices that receive same broadcast message
- **Broadcast MAC**: FF:FF:FF:FF:FF:FF
- **Devices That Broadcast**:
  - Hub: Broadcasts frames to all ports (entire network)
  - Switch: Broadcasts only unknown unicast to all ports except source
- **Separated By**: Router (Layer 3 device)
- **Example**: All devices connected to same switch = one broadcast domain

#### Collision Domain
- **Definition**: Set of devices that can collide with each other
- **When Collisions Occur**:
  - Two devices on same medium try to transmit simultaneously
  - Hub: Entire hub = one collision domain
  - Switch: Each port = separate collision domain
- **Separated By**: Switch (Layer 2 device) or repeater
- **Example**: Hub with 5 computers = 1 collision domain, 1 broadcast domain
- **Example**: Switch with 5 computers = 5 collision domains, 1 broadcast domain

#### Key Formulas
- **Hub**: 1 collision domain, 1 broadcast domain
- **Switch**: (# of ports) collision domains, 1 broadcast domain
- **Router**: Separate broadcast domain per port, no collision domains

---

### 7. Ethernet Frames - Structure & Movement

#### Ethernet Frame Structure
```
|Preamble|Dest MAC|Source MAC|EtherType|Data|FCS|
|(7B)   |(6B)    |(6B)      |(2B)     |(46-1500B)|(4B)|
```

- **Preamble**: 7 bytes alternating 1010... for synchronization
- **Dest MAC**: 6 bytes, destination MAC address
- **Source MAC**: 6 bytes, source MAC address
- **EtherType**: 2 bytes, indicates protocol type (e.g., IPv4 = 0x0800)
- **Data**: 46-1500 bytes, actual data (padded if <46 bytes)
- **FCS (Frame Check Sequence)**: 4 bytes, CRC checksum for error detection

#### Frame Minimum Size
- 14 bytes (header) + 46 bytes (minimum data) + 4 bytes (FCS) = 64 bytes minimum
- If data <46 bytes, padding added

#### How Frame Moves Through Hub
1. Hub receives frame on port X
2. Hub **floods/broadcasts** frame to ALL other ports
3. Frame broadcast to all devices connected to hub
4. Destination device recognizes its MAC and receives
5. Non-destination devices discard frame

#### How Frame Moves Through Switch
1. Switch receives frame on port X
2. Switch **reads destination MAC address**
3. Looks up MAC address in MAC table (MAC → Port mapping)
4. If found: forwards only to that port (**unicast**)
5. If not found: floods to all ports except source port
6. Source MAC learned: adds to MAC table (learning process)

#### MAC Table Learning
- Switch builds table dynamically
- Entry: MAC Address → Ingress Port → Timestamp
- Entries expire after 5 minutes
- On startup, table is empty (forwards broadcast to all ports)

---

### 8. Hub vs Switch vs Router - Key Differences

| Device | OSI Layer | Function | Broadcast | Collision Domain | MAC Table | Speed |
|--------|-----------|----------|-----------|------------------|-----------|-------|
| **Hub** | Physical (1) | Repeater, multiport | Yes (all ports) | 1 | No | Shared |
| **Switch** | Data Link (2) | Bridge, intelligent hub | No (just unknown) | One per port | Yes | Per port |
| **Router** | Network (3) | Routes packets | Separate networks | N/A | No | Per port |

#### Hub Characteristics
- **Dumb**: Just repeats everything
- **Performance**: All ports share bandwidth (10 devices on 10Mbps hub = 1 Mbps each)
- **Collisions**: Common, hurts performance
- **Broadcast**: All devices get all traffic (security issue)

#### Switch Characteristics
- **Smart**: Reads MAC addresses
- **Performance**: Each port gets full bandwidth (10 devices on 10Mbps switch = 10 Mbps each if connected)
- **Collisions**: Rare (micro-segmentation)
- **MAC Table**: Learns and filters traffic
- **VLAN Support**: Can segment broadcast domains

#### Router Characteristics
- **Network Layer**: Routes based on IP addresses
- **Separates Networks**: Different subnets/networks
- **Default Gateway**: Where packets go when destination not on local network
- **NAT**: Can translate private IPs to public IPs
- **Firewall**: Can filter traffic based on ports and protocols

---

## 🟠 HIGH PRIORITY - Data Link & Network Layer

### 9. IP Addresses, Masks, and CIDR

#### IP Address Basics
- **Format**: 4 octets (32 bits total) in dotted decimal: 192.168.1.100
- **Each octet**: 0-255 (8 bits)
- **IPv4 Classes** (outdated but may be on test):
  - Class A: 1-126 (1 bit = 0) - 16 million hosts each
  - Class B: 128-191 (2 bits = 10) - 65,000 hosts each
  - Class C: 192-223 (3 bits = 110) - 254 hosts each
  - Class D: 224-239 - Multicast
  - Class E: 240-255 - Reserved

#### Subnet Mask
- **Purpose**: Determines which part is network ID (NetID) and which is host ID (HostID)
- **Format**: Also 32 bits in dotted decimal
- **All 1's**: Network portion
- **All 0's**: Host portion
- **Example**: 255.255.255.0 means first 3 octets = NetID, last octet = HostID

#### CIDR Notation
- **Format**: 192.168.1.0/24
- **/24** = 24 bits for network, 8 bits for host
- **Equivalent to**: 255.255.255.0

#### Finding NetID and HostID
1. Convert both IP and mask to binary
2. AND them together
3. Result = NetID

**Example**:
```
IP:   192.168.1.100
Mask: 255.255.255.0
NetID = 192.168.1.0
HostID = 0.0.0.100
```

#### Subnetting (Dividing Network)
- **Goal**: Split one network into multiple smaller networks
- **Method**: Borrow bits from host portion for subnet portion
- **Formula**: 2^(borrowed bits) = number of subnets
- **Hosts per subnet**: 2^(remaining host bits) - 2 (minus network and broadcast)

**Example**: 192.168.1.0/24 with /25 mask (borrow 1 bit)
- Subnet 1: 192.168.1.0/25 (hosts: .1-.126)
- Subnet 2: 192.168.1.128/25 (hosts: .129-.254)

---

### 10. TCP/IP Model Layers

#### Layer Structure (5-Layer Model)
1. **Application Layer** (5)
   - User applications (HTTP, FTP, SMTP, DNS, Telnet)
   - Protocols define how apps communicate
   - Adds header (encapsulation)

2. **Transport Layer** (4)
   - TCP (connection-oriented, reliable)
   - UDP (connectionless, fast)
   - Adds port numbers (TCP/UDP header)
   - Ports identify services (HTTP=80, HTTPS=443, DNS=53)

3. **Network Layer** (3)
   - IP (IPv4, IPv6)
   - Routing (finds path to destination)
   - Adds IP header (source & destination IP)
   - Routers operate here

4. **Data Link Layer** (2)
   - MAC addresses (physical addresses)
   - Frames, switches, hubs
   - Adds MAC header + frame check
   - Ensures delivery on local segment

5. **Physical Layer** (1)
   - Cables, signals, electrical
   - Bits on wire
   - Hubs, repeaters

#### Encapsulation at Each Layer
```
Application: [Data]
Transport:   [TCP/UDP Header][Data]
Network:     [IP Header][TCP/UDP Header][Data]
Data Link:   [MAC Header][IP Header][TCP/UDP Header][Data][FCS]
Physical:    [Electrical Signal]
```

#### Key Concepts
- **PDU Names** (Protocol Data Unit):
  - Application: Message
  - Transport: Segment (TCP) or Datagram (UDP)
  - Network: Packet
  - Data Link: Frame
  - Physical: Bit

- **Loose Coupling**: Each layer independent, only interfaces with adjacent layers
- **Only MAC used on local network** (Data Link)
- **Only IP used for routing** (Network Layer)

---

### 11. Purpose of Internet Protocol (IP)

#### Why IP Exists
- **Problem**: Need to send data across multiple networks
- **Solution**: IP provides end-to-end delivery across networks

#### IP Functions
1. **Logical Addressing**: IP addresses (32-bit for IPv4)
2. **Routing**: Determines path through networks
3. **Fragmentation**: Breaks large packets into smaller pieces if needed
4. **Reassembly**: Puts fragmented packets back together at destination
5. **TTL Management**: Prevents infinite loops (decrements each hop)

#### How IP Works with Masks
- IP address + mask = determines if destination is local or remote
- Local destination: Use ARP to find MAC, send direct
- Remote destination: Send to default gateway (router)
- Router looks at destination IP and forwards appropriately

---

### 12. Structured Cabling Best Practices

#### Layout Principles
- **Star Topology**: Central telecommunications room, all cables radiate out
- **Cable Length Limits**: Max 90 meters horizontal run
- **Solid Core**: Horizontal cables (stiff but good conductor)
- **Stranded Core**: Patch cables (flexible, won't break as easily)

#### Telecommunications Room Setup
- **Central Equipment Rack**: 19 inches wide, height in U (1U = 1.75 inches)
- **Patch Panel**: Female connectors on front, punchdown to horizontal cables in back
- **Labeling**: Critical for troubleshooting and maintenance
- **Power**: Dedicated circuit recommended, UPS for protection
- **Cooling**: Climate control to prevent overheating
- **Security**: Lockable room

#### Cable Installation Steps
1. **Planning**: Get floor plan, determine drops locations
2. **Design**: Determine telecom room location (<90m from drops), cable routes
3. **Pulling**: Run cables through ceiling/walls/raceways
4. **Termination**: Punch down to patch panel, test continuity
5. **Documentation**: Label everything, keep records

#### Why Structured Cabling Matters
- Simplifies troubleshooting
- Allows for network growth
- Reduces downtime when adding new devices
- Provides organized, professional appearance
- Supports compliance with standards (TIA/EIA)

---

## 🟡 MEDIUM PRIORITY - Connection Types & Wireless

### 13. Connection Types & Technologies

#### DSL (Digital Subscriber Line)
- **Speed**: 1.5-10 Mbps downstream, 128 Kbps-1 Mbps upstream (asymmetric)
- **Medium**: Existing telephone copper lines
- **Pros**: Available almost everywhere phone lines exist
- **Cons**: Speed depends on distance from central office, shared line with phone

#### T1 (Leased Line)
- **Speed**: 1.544 Mbps (24 channels of 64 Kbps)
- **Type**: Dedicated, digital
- **Pros**: Reliable, dedicated, symmetric
- **Cons**: Expensive ($300-1000/month), requires contract

#### SONET (Synchronous Optical Network)
- **Speed**: OC-1 (51.84 Mbps) to OC-192 (9.95 Gbps)
- **Medium**: Fiber-optic
- **Pros**: Very fast, long distance, reliable
- **Cons**: Very expensive, requires fiber infrastructure

#### 802.11 (WiFi)
- **Speed**: 54 Mbps (802.11g) to 11 Gbps (802.11ax)
- **Range**: 30-100 meters (indoors)
- **Pros**: Mobile, flexible, no cabling
- **Cons**: Interference, security risk, shared medium

#### Satellite
- **Speed**: 10-50 Mbps
- **Range**: Anywhere with satellite signal
- **Latency**: 500+ ms (geostationary orbit)
- **Pros**: Available in remote areas
- **Cons**: High latency, expensive, weather dependent

---

### 14. Wireless Networks - CSMA/CA Deep Dive

#### Why CSMA/CA (Not CSMA/CD)
- **Hidden Node Problem**: Device A and C can't hear each other (B in middle)
- **Can't detect collisions**: Wireless devices can't listen while transmitting
- **Solution**: Avoid collisions before they happen

#### 802.11 Access Method
1. **Listen** to medium (carrier sense)
2. If clear, wait random backoff period (collision avoidance)
3. Transmit frame
4. Recipient sends ACK (acknowledgment)
5. If no ACK, assume collision and retry with longer backoff

#### RTS/CTS (Request to Send / Clear to Send)
- **Optional handshake** to prevent hidden node collisions
- **Sender**: Sends RTS with duration of data transmission
- **Receiver**: Sends CTS with same duration
- **Other devices**: See CTS, stay silent for that duration
- **Result**: Eliminates hidden node collisions

#### 802.11 Standards
- **802.11a**: 54 Mbps, 5 GHz, less interference
- **802.11b**: 11 Mbps, 2.4 GHz, longer range
- **802.11g**: 54 Mbps, 2.4 GHz (backward compatible with 11b)
- **802.11n**: 300 Mbps, dual band (2.4 & 5 GHz)
- **802.11ac**: 1.3 Gbps, 5 GHz only
- **802.11ax (WiFi 6)**: 11 Gbps, 2.4 & 5 GHz, better multi-device performance

---

### 15. Wireless Security: Encryption, MAC Filtering, Authentication

#### Encryption Methods
- **WEP (Wired Equivalent Privacy)**: BROKEN, don't use
- **WPA (WiFi Protected Access)**: Better than WEP, uses TKIP
- **WPA2 (802.11i)**: Current standard, uses AES (strong encryption)
- **WPA3**: Latest, improved security, easier setup for guests

#### MAC Filtering
- **How it works**: Only specific MAC addresses allowed to connect
- **Pros**: Prevents unauthorized devices
- **Cons**: MAC addresses can be spoofed, maintenance nightmare
- **Recommendation**: Use with other methods, not alone

#### Authentication Methods
- **PSK (Pre-Shared Key)**: Password-based, simplest
- **Enterprise**: RADIUS server, certificate-based (802.1X)
- **WPA3 Personal**: Easier setup than WPA2
- **WPA3 Enterprise**: Strongest security, uses 192-bit encryption

#### Best Practice
- **Use WPA2 minimum** (WPA3 if available)
- **Strong password**: At least 12 characters, mixed case/numbers/symbols
- **MAC filtering**: Supplementary, not primary defense
- **Change default credentials**: On access point
- **Disable WPS**: WiFi Protected Setup can be hacked

---

### 16. Ad Hoc vs Infrastructure Mode

#### Infrastructure Mode
- **Access Point**: Central device all clients connect through
- **Topology**: Star topology with AP at center
- **Coverage**: Limited by AP range (30-100m)
- **Scaling**: Can add multiple APs to extend coverage
- **Security**: Easier to centralize and manage
- **Use Case**: Most common, homes, offices, businesses
- **Connection**: Must connect to AP first, then to network

#### Ad Hoc Mode
- **No Access Point**: Devices connect directly to each other
- **Topology**: Mesh topology, peer-to-peer
- **Coverage**: Extends through multi-hop (device A → B → C)
- **Scaling**: Can add many devices, range extends
- **Security**: More difficult to manage
- **Use Case**: Temporary networks, disaster recovery, gaming
- **Connection**: Devices form network without central authority

#### Key Difference
- **Infrastructure**: Managed, centralized control
- **Ad Hoc**: Decentralized, peer-to-peer (like a mesh)

---

## 🟢 MEDIUM-LOW PRIORITY - Additional Topics

### 17. NICs (Network Interface Cards)

#### Purpose
- **Interface** between device and network
- **Converts** data from device to network signals
- **MAC Address**: Unique hardware address on NIC

#### Characteristics
- **Multispeed NICs**: Support multiple speeds (1 Mbps, 10 Mbps, 100 Mbps, 1 Gbps)
- **Auto-Sensing**: Automatically detects network speed and adjusts
- **Full-Duplex**: Can send and receive simultaneously
- **Half-Duplex**: Only send or receive at a time (old hubs)

#### Modern NICs
- Standard: 1 Gbps
- High-end: 10 Gbps or faster
- Wireless: Built into laptops
- Multiple NICs: Server might have 2+ for redundancy or bonding

#### LED Indicators
- **Link Light (steady)**: Connected to network
- **Activity Light (flashing)**: Data being transmitted/received
- Diagnostics: Use these to quickly verify connection

---

### 18. Packet vs Circuit Switching

#### Circuit Switching
- **Connection**: Dedicated path established before data transfer
- **How**: Like phone call, connection maintained for duration of communication
- **Reservation**: Bandwidth reserved for entire connection
- **Examples**: Traditional phone system, ISDN
- **Pros**: Guaranteed bandwidth, low latency, order preserved
- **Cons**: Inefficient if not constantly transmitting, slower to establish, no resource sharing

#### Packet Switching
- **Connection**: No path established, packets sent individually
- **Routing**: Each packet can take different route
- **Sharing**: Bandwidth shared dynamically, used only when sending
- **Examples**: Internet, email, web browsing
- **Pros**: Efficient bandwidth use, fast data transfer, robust (reroutes around problems)
- **Cons**: Variable latency, packets can arrive out of order, congestion possible

#### Comparison
| Aspect | Circuit | Packet |
|--------|---------|--------|
| Connection | Established before | None needed |
| Bandwidth | Reserved | Shared |
| Routing | Fixed path | Dynamic |
| Efficiency | Low for bursty data | High for bursty data |
| Latency | Consistent | Variable |
| Example | Phone | Internet |

---

### 19. Calculations You May Need to Perform

#### Transmission Time
```
Time = (File Size in Bytes × 8) / Link Speed in bps
```
Always multiply bytes by 8 to convert to bits!

#### Overhead Percentage
```
% Overhead = (Total Header + Trailer Bytes) / Total Frame Size × 100
% Data = (Data Bytes) / Total Frame Size × 100
```

#### Base Conversions
- **Binary to Decimal**: Sum powers of 2 where bit is 1
- **Decimal to Binary**: Repeatedly divide by 2, collect remainders
- **Hex to Binary**: Each hex digit = 4 bits
- **Binary to Hex**: Group 4 bits, convert each group

#### Boolean Logic
- **AND**: 1 AND 1 = 1, all others = 0
- **OR**: 0 OR 0 = 0, all others = 1
- **NOT**: Flip all bits
- **XOR**: 1 XOR 1 = 0, others = 1

#### Effective Average Data Rate
```
Effective Rate = (Useful Data / Total Transmitted) × Link Speed
Consider: headers, trailers, overhead, retransmissions
```

#### Mesh Connections
```
Full Mesh: n(n-1)/2
where n = number of devices
```

#### Bandwidth Calculation
```
BW = High Frequency - Low Frequency
```

#### Subnet Calculations
```
Number of Subnets = 2^(bits borrowed)
Hosts per Subnet = 2^(host bits) - 2
```

---

## 🔵 LOWER PRIORITY - Background Knowledge

### 20. Additional Topics for Context

#### Broadband vs Baseband (More Detail)
- Baseband: Single digital signal, entire bandwidth used
- Broadband: Multiple analog signals, frequency division

#### Collision vs Broadcast Domains (Quick Review)
- **Collision Domain**: Where devices compete for medium (1 domain per hub)
- **Broadcast Domain**: Where broadcasts received (1 per switch/network, separated by router)

#### Frame Movement (Quick Reference)
- **Hub**: Floods to all ports (broadcasts)
- **Switch**: Learns MAC table, forwards to specific port (intelligent)
- **Router**: Routes based on IP, separates networks

---

## ✅ STUDY CHECKLIST FOR MIDTERM

- [ ] CSMA/CD vs CSMA/CA: Can you explain the difference and when each is used?
- [ ] ARP: Can you walk through the 4-step process?
- [ ] Broadband vs Baseband: Can you describe and compare?
- [ ] Topologies: Can you describe pros/cons of star, bus, ring, mesh?
- [ ] Media: Can you compare fiber, TP, coaxial, wireless?
- [ ] Hub vs Switch vs Router: Can you explain the differences?
- [ ] Broadcast/Collision Domains: Can you identify them in a network?
- [ ] Ethernet Frames: Can you describe the structure and how it moves through devices?
- [ ] IP/Mask: Can you identify NetID and HostID?
- [ ] TCP/IP Layers: Can you describe each layer?
- [ ] Structured Cabling: Can you explain best practices?
- [ ] Wireless Security: Can you describe encryption, MAC filtering, authentication?
- [ ] Ad Hoc vs Infrastructure: Can you explain the difference?
- [ ] Calculations: Can you do transmission time, overhead %, base conversion, Boolean logic?

---

**Material Coverage**: This guide covers ~95% of material from lectures, powerpoints, and homework. Remaining 5% may come from textbook test bank.

**Last Updated**: March 11, 2026
**Focus on Physical & Data Link Layers for the Midterm**
