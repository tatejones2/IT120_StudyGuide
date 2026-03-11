# IT 120 Midterm Cheat Sheet

**Study the main concepts below and understand the key definitions. This cheat sheet is organized by frequency/importance.**

---

## 🎯 CRITICAL CONCEPTS TO MEMORIZE

### Network Topologies (Know ALL characteristics)
- **Point-to-Point**: Direct connection, simple, not expandable
- **Bus**: Single cable, all on line, needs termination at ends
- **Ring**: Circular, data flows around circle, no termination needed
- **Star (Hub-and-Spoke)**: Central connection point, most fault tolerant per device
- **Mesh**: Fully-meshed = n(n-1)/2 connections; partially-meshed = at least 2 redundant
- **Star-Bus**: Looks like star, acts like bus (MOST COMMON TODAY)
- **Star-Ring**: Looks like star, acts like ring (in hub box)

### Cable Types & Ratings
- **UTP**: Most common, unshielded, cheaper
- **STP**: Shielded, needed in high EMI areas
- **Fiber-Optic**: Immune to EMI, long distance, uses light not electricity
- **CAT Ratings** (memorize speed):
  - CAT 5e: 1 Gbps (recognized)
  - CAT 6: 10 Gbps (recognized)
  - CAT 6a: 10 Gbps (recognized)
  - CAT 3-4: Old, rare
  - CAT 7-8: Not officially recognized

### Connectors
- **RJ-45**: Networks (8P8C, 4 pairs)
- **RJ-11**: Phones (2 pairs)
- **BNC**: Coaxial, older networks
- **Fiber**: ST (bayonet), SC (push), LC (duplex), MT-RJ (multi)

### Cable Installation Standards (TIA/EIA)
- **Horizontal cabling**: ALWAYS solid core, under 90 meters
- **Patch cables**: Stranded core, max 5 meters
- **Total run**: 90m horizontal + 5m patch + 5m patch = 100m max
- **Equipment Rack**: 19 inches wide, height in U (1U = 1.75 inches)
- **Telecommunications Room**: Central hub, contains switch, router, server, patch panel

### Connecting Devices
- **Repeater**: Physical layer, extends cable length
- **Hub**: Physical layer, multiport repeater, broadcasts everything
- **Switch**: Data link layer, reads MAC addresses, forwards only to destination port
- **Bridge**: Same as switch (Layer 2 Switch)

### MAC & Ethernet Addressing
- **MAC Address Format**: xx:xx:xx:xx:xx:xx or xx-xx-xx-xx-xx-xx (48 bits = 6 bytes)
- Must have exactly 2 hex digits per octet (6 octets total)
- Each octet = 8 bits

### Structured Cabling Layout
- **Demarcation Point (Demarc)**: Where ISP/phone company responsibility ends
- **Network Interface Unit (NIU)**: Serves as demarc in SOHO (modem/gateway)
- **Patch Panel**: Female connectors on front, punchdown to horizontal cables in back
- **Work Area**: Wall outlet + NIC = connection point
- **Cable Management**: Critical for troubleshooting, keep organized and labeled

---

## ⚡ KEY FORMULAS (Definitely on test)

### Transmission Time
```
Time = (File Size in Bytes × 8 bits/byte) / Link Speed in bps
```
**Example**: 10 MB over 1 Gbps link
```
(10 MB × 8 bits/byte) / 1 Gbps = 0.08 seconds
(10 × 10^6 × 8) / (10^9) = 8 × 10^7 / 10^9 = 0.08 seconds
```

### Overhead Percentage
```
% Overhead = (Header + Trailer bytes) / Total bytes × 100
% Data = (Data bytes) / Total bytes × 100
```

### Mesh Topology Connections
```
Number of connections = n(n-1)/2
where n = number of devices
```
**Example**: 20 nodes = (20×19)/2 = 190 connections

### Bandwidth
```
Bandwidth = High Frequency - Low Frequency (in Hz)
```

### Internet Header Length (IHL) to Bytes
```
Header Size = IHL × 4 bytes
Example: IHL=5 → 5 × 4 = 20 bytes
```

---

## 📊 ENCAPSULATION & LAYERS (TCP/IP 5-Layer Model)

### Layer Order (Top to Bottom):
1. **Application Layer**: Browsers, email, etc.
2. **Transport Layer**: TCP/UDP (adds header)
3. **Network Layer**: IP, routing (adds header)
4. **Data Link Layer**: MAC, switching (adds header + trailer)
5. **Physical Layer**: Cables, electrical signals

### Key Concept:
- **Encapsulation**: Each layer wraps data with headers
- **Loose Coupling**: Layers work independently, can modify one layer without affecting others
- **Protocol Headers** added at each layer contribute to overhead

---

## 🔧 TROUBLESHOOTING PROCESS

### Step 1: Visual Check
- Is everything plugged in?
- Are cables properly connected?

### Step 2: Scope the Problem
- **All computers affected?** → Shared resource (switch, print server)
- **One computer?** → Host, NIC, or local cabling

### Step 3: Hardware vs Software
- **One application fails** → Software
- **Can browse but no email** → Software
- **Nothing works** → Hardware

### Step 4: LED Indicators
- **Link light (steady)**: NIC connected
- **Activity light (flashing)**: Network traffic

### Step 5: Isolation Process
1. Plug system into known good outlet
2. If works: Cabling problem
3. If doesn't work: NIC, connector, or driver issue

### Testing Tools
- **Cable Tester**: Verifies cable and terminated ends
- **Continuity Tester**: Wiremap test
- **Multimeter**: Electrical properties
- **TDR/OTDR**: Advanced distance/fault location

### Common Cable Issues
- **Crosstalk (NEXT/FEXT)**: Signal interference between pairs
- **Attenuation**: Signal weakens over distance
- **Broken/shorted wires**: No continuity
- **Incorrect termination**: Miswired or bad connections
- **EMI/RFI interference**: Electrical or radio interference

---

## 💡 COMMON HOMEWORK/TEST QUESTION TYPES

### Type 1: MAC Address Validation
- Must be: 6 octets of exactly 2 hex digits each
- Separators: : or - (not mixed)
- **Invalid examples**: `9a-1b-2c-71d-1e-f7` (71d has 3 chars), `1a-3-c6-08-90-10` (3 has 1 char)

### Type 2: Data Size Calculations
- Convert GB/MB to bytes: multiply by 10^9 or 10^6
- Convert to bits: multiply by 8
- Divide by speed in bps to get time in seconds

### Type 3: Overhead/Percentage Questions
- Identify: data bytes, header bytes, trailer bytes
- Total = data + headers + trailers
- Overhead % = (headers + trailers) / total × 100

### Type 4: Network Design Questions
- Always consider: cable length limits (90m), growth capacity, cost
- Telecom room placement: within 90m of all drops
- Horizontal cable: ALWAYS solid core
- Patch cables: ALWAYS stranded core

### Type 5: Binary/Hex Conversions
- Hex to Binary: Each hex digit = 4 bits
- Binary to Decimal: Sum powers of 2
- Show your work: Even partial credit requires showing steps

### Type 6: Logical Operations (AND/OR)
- **AND**: 1 AND 1 = 1, all others = 0
- **OR**: 0 OR 0 = 0, all others = 1
- Convert hex → binary → do operation → convert back

### Type 7: RFC/Protocol Header Questions
- **RFC 791**: IP protocol, network layer
- **IP Header Fields**: Version, IHL, ToS, Total Length, ID, Flags, Fragment Offset, TTL, Protocol, Checksum, Source, Destination, Options, Padding
- **Time to Live (TTL)**: Max time data allowed to exist on internet
- **Padding**: Ensures header ends on 32-bit boundary

### Type 8: Wireless Frame Addressing
- **ToDS=0, FromDS=1**: Receiving (destination sees AP address)
- **ToDS=1, FromDS=0**: Sending (original AP address)
- **ToDS=1, FromDS=1**: On distribution system (both AP addresses)

### Type 9: Network Upgrade Scenarios
- For cameras/high-speed: Need Gigabit (1000BaseT with Cat6/6a)
- UTP sufficient for up to 100m with proper category
- Fiber for very long distances or heavy EMI
- Upgrade: Switch, cabling, NICs, software

### Type 10: Wireless Standards
- **802.11ax (Wi-Fi 6)**: Best performance with many devices
- **Security**: WPA3 (most secure), WPA2 acceptable
- **Access**: Consider channel interference from competitors
- **Setup**: PoE switches, access points, encryption

---

## 🌳 NETWORK INSTALLATION CHECKLIST

### Planning Phase (Step 1-2)
- [ ] Get floor plan
- [ ] Identify telecom room location(s)
- [ ] Map cable runs (no more than 90m)
- [ ] Plan routes (ceiling, wall, raceway, floor)
- [ ] Plan extra drops for future growth

### Design Phase (Step 3)
- [ ] Telecom room: <90m from all drops, power, cooling, expandable, lockable
- [ ] Cable type: CAT5e minimum (CAT6 for futureproofing)
- [ ] Equipment: Switch, patch panel, router, server, UPS, rack

### Installation Phase (Step 4)
- [ ] Pull cable from telecom room to drops
- [ ] Neat cable management (critical!)
- [ ] Proper termination and testing
- [ ] Label everything
- [ ] Document everything

### Testing & Troubleshooting
- [ ] Continuity test each run
- [ ] Verify speed capability
- [ ] LED light checks
- [ ] Functional network test

---

## 🔑 QUICK REFERENCE: WHEN TO USE WHAT

### Cable Type Decision
- **UTP**: Default choice, cost-effective, most locations
- **STP**: Only if high EMI environment
- **Fiber**: Long distances (>100m), highest speeds, EMI immune

### When to Upgrade from Star-Bus
- Need Gigabit speeds → Upgrade switch to Gigabit switch
- Need Gigabit cabling → Upgrade to CAT6/6a
- Adding high-bandwidth devices → Plan for segmentation or dedicated lines
- Growth → Add drops during initial install, not after

### Troubleshooting Priority
1. Check physical connections first (plugged in, lights on)
2. Check if one or all computers affected
3. Determine if hardware or software problem
4. Use LED indicators before busting out tools
5. Test known-good connections for comparison

---

## 📝 IMPORTANT TERMS TO KNOW

- **Fault Tolerance**: System can keep working even when something fails
- **Bandwidth**: Range of frequencies (Hz) OR bits per second (bps) depending on context
- **EMI/RFI**: Electrical/Radio interference that corrupts signals
- **Crosstalk**: Signal from one wire affecting another wire
- **Attenuation**: Signal weakening over distance
- **Termination**: Resistor at end of cable to prevent reflections (bus/ring topologies)
- **Punchdown Block**: Where patch panel cables connect to horizontal runs
- **PoE**: Power over Ethernet (delivers power + data on same cable)
- **Plenum**: Higher fire rating, less smoke/fumes (3-5x cost of PVC)
- **Multimode Fiber**: Uses LEDs, good for shorter distances
- **Single-mode Fiber**: Uses lasers, better for long distances

---

## ⚠️ COMMON MISTAKES TO AVOID

1. ❌ Using stranded core for horizontal runs (must be solid)
2. ❌ Mixing MAC address separators (: and -)
3. ❌ Forgetting to multiply by 8 when converting bytes to bits
4. ❌ Running cables longer than 90 meters horizontally
5. ❌ Placing telecom room away from devices
6. ❌ Not showing work on calculations
7. ❌ Forgetting overhead bytes in encapsulation problems
8. ❌ Using wrong CAT rating (Cat5 won't support 1 Gbps)
9. ❌ Not accounting for growth in network design
10. ❌ Confusing logical vs physical topology

---

## 🎓 STUDY TIPS

1. **Draw topology diagrams**: Understand pros/cons of each
2. **Memorize the formulas**: Especially transmission time and overhead %
3. **Practice calculations**: Binary/hex conversion, bandwidth, overhead
4. **Understand the reasoning**: Why CAT5e for 1Gbps? Why solid core horizontally?
5. **Review RFC 791**: Know IP header fields and what they mean
6. **Walk through troubleshooting**: Process matters, not just the answer
7. **Learn the standards**: TIA/EIA, 802.11, IEEE standards
8. **Cable management**: This comes up in network design questions
9. **Growth planning**: Companies always plan for expansion
10. **Test tools**: Know what each tool does and when to use it

---

**Last Updated**: March 11, 2026
**Good luck on your midterm!**
