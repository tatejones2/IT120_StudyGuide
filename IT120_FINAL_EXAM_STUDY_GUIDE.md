# IT 120 Final Exam Study Guide

**Coverage**: Lectures + PowerPoints + homework ≈ 95% of exam. Remaining ≈ 5% may come from textbook test bank.

---

## 1) CIDR (Classless Inter-Domain Routing)
**What it is**: A way to write IP networks using a slash prefix, like `192.168.10.0/24`. The `/24` means the first 24 bits are the network part.

**Why it’s useful**:
- Replaces old “Class A/B/C” rules.
- Allows networks of any size (more efficient, less waste).
- Enables **route aggregation** (combining many routes into one).

### Three ways to calculate subnet info
You can find network details using **one of three methods**:

**A) With a subnet mask**
- Example: `10.5.8.0/21` → mask = `255.255.248.0`
- **Network address**: IP AND mask
- **Broadcast**: last address in range
- **Hosts**: all addresses between network and broadcast

**B) With block size**
- Find the **block size** = 256 - mask value in the **first “non-255” octet**.
- Example: `/21` → mask = `255.255.248.0` → block size = 256 - 248 = 8
- Subnets increase by 8 in that octet.

**C) With min/max addresses**
- If you know the range, min = network, max = broadcast
- Hosts are between min+1 and max-1

### Number of valid hosts
- Formula: $2^{host\ bits} - 2$
- Host bits = 32 - prefix length
- Example: /27 → host bits = 5 → $2^5 - 2 = 30$ hosts

### Subblock addresses and masks
- “Subblock” = each subnet’s network address (start of each block)
- Example: /27 block size = 32 → subblocks at .0, .32, .64, .96, .128, .160, .192, .224

---

## 2) DHCP (Dynamic Host Configuration Protocol)
**What it is**: Automatically gives devices IP addresses and network settings.

**Purpose**:
- Prevents manual IP setup
- Avoids duplicate IPs
- Easier management at scale

**DHCP Process (DORA)**:
1. **Discover**: Client broadcasts: “Any DHCP server?”
2. **Offer**: Server replies with an IP offer
3. **Request**: Client asks to use that offer
4. **Acknowledge**: Server confirms lease

### Static vs Dynamic Addressing
**Static**:
- Manually assigned IP
- Good for servers, printers, routers
- Never changes

**Dynamic**:
- Assigned by DHCP
- Good for laptops/phones
- Can change when lease expires

**Setup**:
- Static: configure IP, mask, gateway, DNS manually
- Dynamic: set device to “Obtain IP automatically”

---

## 3) Fragmentation
**What it is**: Breaking a large IP packet into smaller pieces to fit a network’s MTU.

**Purpose**:
- Different networks allow different max packet sizes (MTU)
- Routers split packets if too large

**Where it happens**:
- IPv4: routers can fragment
- IPv6: routers do NOT fragment, sender must do it

---

## 4) IPv4 vs IPv6 (Key Differences)
- **Address size**: IPv4 = 32-bit, IPv6 = 128-bit
- **Notation**: IPv4 dotted decimal, IPv6 hexadecimal with colons
- **Addresses**: IPv6 has vastly more addresses
- **Fragmentation**: IPv4 routers can fragment; IPv6 routers can’t
- **Header**: IPv6 header simpler, uses extensions
- **Security**: IPv6 designed with IPsec support

---

## 5) DNS (Domain Name System)
**What it is**: Converts names (google.com) into IP addresses.

**How it works**:
1. Client asks DNS server
2. If not cached, DNS server queries others (root → TLD → authoritative)
3. Returns IP to client

**Why it matters**: Humans use names; networks use IPs

---

## 6) Autonomous Systems (AS)
**What it is**: A large network or group of networks run by one organization with a common routing policy.

**Relation to gateway routers**:
- **Gateway routers** connect one AS to another
- They use **BGP** to exchange routes between ASes

---

## 7) NAT (Network Address Translation)
**What it is**: Converts private IPs to public IPs (and back).

**Purpose**:
- Allows many devices to share one public IP
- Conserves IPv4 addresses
- Adds a layer of security (hides internal network)

---

## 8) IPv6 Details
**Notation**:
- Eight groups of four hex digits
- Example: `2001:0db8:0000:0000:0000:ff00:0042:8329`
- Can shorten: remove leading zeros, replace consecutive zeros with `::`

**Scope**:
- **Global unicast**: routable on internet
- **Link-local**: only on local network (starts with `fe80::`)
- **Unique local**: private, not routable on internet

**Aggregation**:
- Hierarchical addressing allows route summarization

**Migration process**:
- **Dual stack**: devices run IPv4 and IPv6
- **Tunneling**: IPv6 inside IPv4
- **Translation**: NAT64 and similar

---

## 9) Network Layer (Layer 3)
**Purpose**: End-to-end delivery across multiple networks.

**Primary purposes**:
- Logical addressing (IP)
- Routing between networks
- Fragmentation and reassembly

### IP Header Structure (IPv4)
Key fields you should recognize:
- Version
- IHL (header length)
- Total Length
- Identification
- Flags/Fragment Offset
- TTL
- Protocol
- Header Checksum
- Source IP
- Destination IP

---

## 10) Routing & Routers

### Routing Tables
- Built from **static routes** or **dynamic routing protocols**
- Contain destination networks + next hop

### How routers decide where to forward
1. Look at destination IP
2. Match with routing table
3. Use **longest prefix match**
4. Forward to next hop

### Routing Algorithms / Protocols
- **RIP**: distance vector, hop count, slow, max 15 hops
- **OSPF**: link-state, fast, uses cost
- **EIGRP**: Cisco proprietary, hybrid
- **BGP**: external routing between ASes, path-vector

---

## 11) Sockets
**What it is**: An endpoint for communication between two devices.

**Purpose**:
- Allows apps to send/receive data using IP + port

**Process / States (conceptual)**:
- **Open**: socket created
- **Listening**: server waiting for connection
- **Blocked/Wait**: waiting for data or connection
- **Close**: connection ended

---

## 12) Transport Layer (Layer 4)
**Purpose**: End-to-end delivery between applications.

### TCP vs UDP
- **TCP**: connection-oriented, reliable, ordered, error-checked
- **UDP**: connectionless, fast, no reliability

### TCP Handshake (3-way)
1. SYN (client → server)
2. SYN-ACK (server → client)
3. ACK (client → server)

---

## 13) Security Concepts

### Authorization vs Authentication vs Encryption vs Nonrepudiation
- **Authentication**: Prove who you are
- **Authorization**: What you’re allowed to do
- **Encryption**: Scrambles data so others can’t read it
- **Nonrepudiation**: Proof that someone did something (can’t deny it)

### IPSec
- Secures IP packets at the network layer
- Can authenticate and encrypt
- Works with IPv4 and IPv6

### Symmetric vs Asymmetric Encryption
**Symmetric**:
- Same key to encrypt/decrypt
- Fast, but key sharing is hard

**Asymmetric**:
- Public key encrypts, private key decrypts
- Slower, but solves key exchange problem

### Authentication Extensions
- Many exist because different systems have different needs (speed, compatibility, security level)

### Goals of Security
- **Confidentiality** (privacy)
- **Integrity** (no tampering)
- **Availability** (systems stay up)
- **Authentication** (verify identity)
- **Nonrepudiation** (proof of action)

### Digital Certificates
- Digital ID that verifies a public key belongs to someone
- Issued by a **Certificate Authority (CA)**
- Used in HTTPS, VPNs, authentication

---

## 14) Security Hardware
- **Firewall**: Blocks/permits traffic based on rules
- **IDS (Intrusion Detection System)**: Detects suspicious activity (alerts)
- **IPS (Intrusion Prevention System)**: Detects + blocks threats

---

## 15) VLANs (Virtual LANs)
**What it is**: Logical separation of networks on the same switch.

**Pros**:
- Improves security (separate departments)
- Reduces broadcast traffic
- Easier network management

**Cons**:
- More complex setup
- Requires VLAN-aware switches and routing between VLANs

---

# FINAL EXAM CHEAT SHEET (ONE PAGE)

**Write these on your one-page handwritten sheet.**

### CIDR + Subnetting
- CIDR: /prefix = network bits
- Hosts: $2^{host\ bits} - 2$
- Block size: 256 - mask octet
- Subnets = $2^{borrowed\ bits}$
- Longest prefix match

### DHCP (DORA)
- Discover → Offer → Request → Acknowledge
- Static = manual, Dynamic = DHCP

### IPv4 vs IPv6
- IPv4 = 32-bit, IPv6 = 128-bit
- IPv6 uses hex + colons, supports `::`
- IPv4 routers fragment; IPv6 does not

### NAT
- Private → Public translation
- Saves IPv4 addresses
- Hides internal network

### DNS
- Names → IPs
- Uses caching + hierarchy (root → TLD → authoritative)

### Fragmentation
- Split packets to fit MTU
- IPv4 routers can fragment; IPv6 sender only

### Layer 3 (Network)
- IP addressing + routing
- Header fields: Version, IHL, TTL, Protocol, Src/Dst IP

### Routing Protocols
- RIP (distance vector, hop count)
- OSPF (link-state, cost)
- EIGRP (Cisco hybrid)
- BGP (inter-AS)

### Transport Layer
- TCP = reliable, ordered, handshake
- UDP = fast, no reliability
- TCP 3-way: SYN → SYN-ACK → ACK

### Sockets
- Endpoint = IP + Port
- Server = listening, client = connect

### Security
- Authn = who you are
- Authz = what you can do
- Encryption = confidentiality
- Nonrepudiation = proof
- Symmetric vs Asymmetric
- IPSec = encrypt/authenticate IP

### Hardware Security
- Firewall = filter
- IDS = detect
- IPS = detect + block

### VLANs
- Logical network separation
- Pros: security, less broadcast
- Cons: complexity

---

**Last Updated**: May 11, 2026
