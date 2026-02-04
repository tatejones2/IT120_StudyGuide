# IT 120 Study Guide

## Table of Contents
1. [Network Topology](#network-topology)
2. [Cabling](#cabling)
3. [Connecting Devices](#connecting-devices)
4. [Structured Cabling Installation](#structured-cabling-installation)
5. [Testing & Troubleshooting](#testing--troubleshooting)

---

## Network Topology

### Definition
**Network Topology**: Methods cables and other pieces of hardware connect to one another.

- **Logical Topology**: How devices connect to each other with regards to data flow (also called signaling topology)
- **Physical Topology**: How a network is laid out in the messy real world (also called schematic)

### Point-to-Point Topology
- Two computers connect directly
- No need for a central hub
- Wired or wireless
- **Pros**: Very simple, no extra hardware required, private and secure link
- **Cons**: Cannot expand the network

### Bus Topology
- Single bus cable
- Connects all computers in a line
- Data flows from each computer onto the bus
- Terminating resistor required at ends to prevent data reflection
- **Pros**: Easy to install, uses less cabling
- **Cons**: Not fault tolerant, electrical limits on length, everyone can see all traffic

### Ring Topology
- Central ring of cable
- Connects computers in a ring
- Data flows from one computer to next one in circle
- No end of cable and no need for termination
- **Pros**: Easy to install and reconfigure
- **Cons**: Not fault tolerant, everyone can see all traffic

### Star Topology (Hub-and-Spoke)
- A central connection for all computers
- Better fault tolerance
- **Pros**: Easy to install and reconfigure, robust (link failure affects only one computer)
- **Cons**: More expensive, difficult to redesign, connection point is single point of failure

### Hybrid: Star-Ring
- Looks like a star, acts like a ring
- Ring shrunk down into a hub-like box
- Cables connect to the hub

### Hybrid: Star-Bus
- Looks like a star, acts like a bus
- Bus segment shrunk down into a hub-like box
- Cables connect to the hub
- **Most common today**

### Mesh Topology
**Fully-meshed**: Every computer connects directly to every other computer
- Most fault tolerant
- Often used in wireless networks
- Formula for connections: n(n-1)/2 where n = number of devices
- Example: 20 nodes = (20×19)/2 = 190 connections

**Partially-meshed**: At least two machines have redundant connections

**Pros**: Most robust, dedicated links, private and secure
**Cons**: Expensive due to number of ports and links

### Point-to-Multipoint
- A single system acts as common source through which all members of network converse
- Requires an intelligent device in the center
- **Pros**: Need a host to act as hub, private and secure links
- **Cons**: Hub host's capacity limits network size

### Fault Tolerance
**Fault Tolerance**: A system's capacity to keep functioning even when some part has failed.

---

## Cabling

### Bandwidth
In signal processing:
- Range of frequencies a medium can pass without losing half the power
- Example: A cable can pass frequencies between 10 KHz and 50 KHz
  - BW = high freq - low freq = 50 - 10 = 40 KHz

In computing:
- Number of bits per second (bps) that can be transmitted
- Bits/second is proportional to bandwidth in hertz
- Networks use bandwidth-efficient encoding schemes

### Coaxial Cable
- Central conductor wire surrounded by insulating material
- Braided metal shield layer shields transmissions from electromagnetic interference (EMI)
- Used primarily for cable modems, TV cable boxes, and video connections
- **Connectors**: 
  - BNC (bayonet connector) - used in older computer networks
  - F-type connector - used for cable/satellite
- **RG Rating**:
  - RG-6 is dominant cable today
  - RG-58 and RG-59 rarely used
- **Ohm Rating**: Measure of impedance (RG-6 and RG-59 rated at 75 Ohms)

### Twisted Pair
- Most common network cabling
- Twisted pairs of cables bundled together
- Twists reduce crosstalk interference
- **Two Types**:
  - **Shielded Twisted Pair (STP)**: Shielding protects from EMI, needed in locations with excessive EMI
  - **Unshielded Twisted Pair (UTP)**: Most common, cheaper than STP, used in Ethernet and telephone systems

### CAT Ratings for Twisted Pair

| CAT | Frequency | Max Speed | Status |
|-----|-----------|-----------|--------|
| CAT 3 | 16 MHz | 16 Mbps | Recognized |
| CAT 4 | 20 MHz | 20 Mbps | No longer recognized |
| CAT 5 | 100 MHz | 100 Mbps | No longer recognized |
| CAT 5e | 100 MHz | 1 Gbps | Recognized |
| CAT 6 | 250 MHz | 10 Gbps | Recognized |
| CAT 6a | 500 MHz | 10 Gbps | Recognized |
| CAT 7 | 600 MHz | 10+ Gbps | Not recognized |
| CAT 7a | 1000 MHz | 40-100 Gbps | Not recognized |
| CAT 8 | 2000 MHz | 25-40 Gbps | Not recognized |

### Connectors
- **RJ-11**: Two pairs of wires for telephones
- **RJ-45** (8P8C): Four pairs of wires for networks

### Solid vs Stranded Core
- **Solid Core**: Better conductor, but stiff (used for horizontal cabling per TIA/EIA)
- **Stranded Core**: Not as good a conductor, but does not break as easily

### Fiber-Optic Cable
- Transmits light instead of electrical signals
- Not affected by EMI
- Excellent for long-distance transmissions
  - Single copper cable: up to a few hundred meters
  - Fiber-optic cable: up to tens of kilometers

**Composition**:
- **Core**: The glass fiber
- **Cladding**: Reflects signal down the fiber
- **Buffer**: Gives strength
- **Insulating Jacket**: Protects inner components

**Designator**: Two-number format (Core/Cladding measurements)
- 62.5/125 μm - most common cable size

### Fiber-Optic Types
- **Multimode Fiber (MMF)**: Uses LEDs
- **Single-mode Fiber (SMF)**: Uses Lasers

### Light Sources
- **LEDs** (Light Emitting Diodes):
  - Low cost
  - Slower
  - Usually 850 nm wavelength
  
- **Lasers**:
  - Higher cost
  - Faster
  - Prevents modal distortion
  - High transfer rates over long distances
  - 1310 or 1550 nm wavelength

### Fiber-Optic Connectors
- **ST**: Bayonet-style
- **SC**: Push-in
- **LC**: Duplex
- **MT-RJ**: Multi-fiber connector

### Cable Fire Ratings
- **Polyvinyl Chloride (PVC)-rated**: No significant fire protection, lots of smoke
- **Plenum-rated**: Costs 3-5x more than PVC, burns with less smoke and fumes, often required
- **Riser-rated**: Used for cables in walls (vertical runs), less protection than plenum

---

## Connecting Devices

### Repeater
- Operates at the physical layer
- Connects two segments of the same LAN
- Regenerates signals to extend maximum length
- Forwards everything

### Hub
- Physical layer device
- Multiport repeater
- Sends frames received on one port out to all other ports
- Multiple hubs can be connected together
- More hubs can reduce network performance

### Switch (Bridge / Layer 2 Switch)
- Operates at physical layer and data link layers
- **Physical layer**: Acts as a hub
- **Data link layer**: Examines MAC addresses to send frames only to destination port
- Used to connect LANs in the same organization and location
- Originally expensive, now comparable in price to hubs
- Has become the standard network appliance, replacing hubs

### Bonding/Link Aggregation
- Multiple NICs to effectively double speed between device and switch

---

## Structured Cabling Installation

### Tree Topology
- Most commonly deployed topology
- **Pros**: More fault tolerant, used in broadband, expandable, manageable, error detection, point-to-point wiring
- **Cons**: Troubleshooting complex, costly, backbone can be single point of failure, reconfiguring challenging

### Cisco 3-Layer Model
- **Core Layer**: Manages large amounts of high-speed traffic (backbone)
- **Distribution Layer**: Security/firewalls, performs WAN filtering
- **Access Layer**: User interact with devices on the network

### Structured Cabling Standards
- Governed by **TIA/EIA standards** (Telecommunications Industry Association/Electronic Industry Alliance)
- Details on every aspect of cabled network:
  - Assessment of connections leading outside network
  - Type of cabling
  - Position of wall outlets
  - Network components

**Goals**:
- Create safe, reliable cabling infrastructure
- Communicate knowledgeably with cable installers
- Perform basic troubleshooting

### Basic Network Components
Most common network uses:
- Star-bus topology
- A switch (Layer 2 switch/bridge or hub)
- UTP cable
- 2 or more PCs

### Switch Location Considerations
- People tripping over cables
- EMI
- Exposed cables vulnerable to physical damage
- Challenges to network modifications

**Better Approach**: Keep switches in a **telecommunications room** (server room) with organized cabling hardware.

### Horizontal Cabling
- Runs from work area to telecommunications room
- Use CAT5e or better UTP cable (CAT6a for 10GBaseT)
- **Types**:
  - Solid core: Better conductor, stiff
  - Stranded core: Not as good conductor, less brittle
- **TIA/EIA Specification**: Horizontal cabling should always be solid core
- Typically four-pair UTP (high-end telephone setups use 25- or 100-pair)

### Telecommunications Room
- Heart of basic star topology
- One endpoint of horizontal runs
- Central component is **equipment rack**:
  - Safe, stable platform for hardware
  - Almost all network equipment can be rack-mounted

### Equipment Racks
- **Width**: 19 inches
- **Height Measurement**: U (equivalent to 1.75 inches)
  - Example: 60U rack is 105 inches high
- **Types**: Two post, four post, server rail rack
- **Houses**: Servers, UPS, PDU (power distribution unit), routers, switches

### Patch Panels and Cables
- Don't connect horizontal cabling directly to switch
- Instead use a **patch panel**:
  - Row of female connectors (ports) in front
  - Permanent connections to horizontal cables in back (punchdown block)
  - Connect with punchdown tool (110 block)
  - **Critical**: Proper labeling

**Patch Cable**:
- Stranded cable (not solid)
- Typical length: 2-5 feet (5 meters recommended maximum)
- **Cable Management**: Color-coded, documented clearly

**Alternative Connection Points**:
- **BIX block** (Nortel Networks): Installed on wall rather than in rack
- **Krone block** (Krone Group): Enables networking and audio interconnections

### Work Area
- Wall outlet: Female jack with CAT rating
- Mounting plate and faceplate
- Connect NIC (Network Interface Card) to wall outlet with patch cable
- **Source of most network failures**

### Cable Length Specifications
- Most Ethernets specify maximum 100 meters between switch and each computer
- In practice: Keep runs < 90 meters
  - Allows up to 5m patch cable in telecommunications room
  - Allows up to 5m patch cable in work area

### Building-Wide Networks
- Cabling on one floor: Star topology
- **High-speed backbone**: Runs vertically
  - Connects to multiswitch on each floor
  - Dedicated telephone cabling backbone runs alongside

### Demarc and NIU
- **Demarcation Point (Demarc)**: 
  - Dividing line of responsibility
  - Physical location of connection with outside world
  - Marks who is responsible for network function
  
- **Network Interface Unit (NIU)**:
  - Serves as demarc between SOHO (Small Office Home Office) and ISP
  - DSL or cable modem usually serves as demarc in home network

### Smart Jacks
- NIUs with remote loopback capability
- Challenge to ISP/telephone provider to diagnose system faults

### Connections Inside Demarc
- Network and telephone cables connect to **Customer-Premises Equipment (CPE)**
- Cabling runs from NIU to CPE (multiplexer or LAN switch connected to patch panel)
- **Main patch panel**: Called vertical cross-connect

### Installing Structured Cabling

**Step 1: Getting Floor Plan**
- Determine potential locations for telecommunications rooms
- Locate physical firewalls
- Give overall feel for scope of job
- Create one if none exists

**Step 2: Mapping the Runs**
- Determine length of cable runs (none longer than 90 meters)
- Determine route of cable runs (keep together in hooks, cable trays, or raceway)
- Determine location of each cable drop (where cable comes out of wall)
- Include extra drops
- Determine customer's plans and budget
- Decide if runs will be inside or outside walls

**Step 3: Telecom Room Location Criteria**
- Distance no more than 90 meters from drops
- Adequate power (dedicated circuit recommended)
- Low humidity
- Provide cooling
- Room for expansion
- Door should be lockable

**Step 4: Pulling Cable**
- Start in telecommunications room and pull to drops
- Open drop ceiling and string via hooks or cable trays
- Requires 2-3 people
- Hardest part: Working around old cable installations
- **Neatness counts!**

**Important**: Cable management is crucial for troubleshooting and maintenance

---

## Testing & Troubleshooting

### Verifying Cable Runs
- Verify each jack is properly connected
- Verify cable run can handle network speed
- Different challenges for copper and fiber:
  - Signal degradation
  - Lack of connection
  - Interference

### Copper Cable Challenges
- Potentially bad copper cable:
  - Incorrect length or speed
  - Broken or shorted wires
  - Incorrectly terminated when connected
  - Electrical or radio interference
  - Crosstalk and attenuation

**Testing Tools for Copper**:
- **Cable Tester**: Verifies cable and terminated ends are correct
- **Continuity Tester**: Runs wiremap test
- **Multimeter**: Measures electrical properties
- **Time Domain Reflectometer (TDR)**: Advanced testing

### Crosstalk and Attenuation
- **Crosstalk**:
  - Near-End Crosstalk (NEXT): Depends where listening and actual crosstalk exist
  - Far-End Crosstalk (FEXT)
  
- **Attenuation/Dispersion**:
  - Signal becomes steadily weaker as it progresses down wire
  - More susceptible to crosstalk
  - In fiber: Light propagating down fiber diffuses over distance

### Fiber Cable Challenges
- Signal loss:
  - Damaged cables or open connections
  - Dirty or mismatched connector
  - Fiber length (attenuation/dispersion)
  - Bend radius: Light leakage with too much bend
  
- Physical or Signal Mismatch:
  - Transceiver, fiber, or wavelength mismatch

**Testing Tools for Fiber**:
- **Optical Time Domain Reflectometer (OTDR)**: Determines continuity

### Diagnostics and Repair

**Start Here**:
1. Visually check that everything is plugged in
2. Does problem affect all computers or just one?
   - All: Problem with shared resource (switch, print server)
   - One: Problem in host or cabling between host and switch
3. Is the problem hardware or software?
   - One application fails: Try another application
   - User can browse internet but no email: Software problem
   - Nothing works (no internet, no print, no network): Hardware problem

### Using LED Indicators
- **UTP NICs have LEDs**:
  - Link light: Steady when NIC is connected
  - Activity light: Flashes when network traffic detected
- Many fiber-optic NICs don't have lights
- Switches also have link lights

### Isolating the Problem
1. Is problem in host or cabling?
   - Plug system into known good outlet
   - System works: Cabling problem likely (confirm with continuity test)
   - System doesn't work: NIC issue, bad connector, or incorrect driver

### Cable Testing Process
- Most problems occur at the work area
- Use tools to check continuity (ensure no breaks or disconnections)
- If no continuity: Isolate problem to patch cable or horizontal run

### NIC Diagnostics
- Use operating system or NIC diagnostic software
- Run Loopback test on NIC:
  - **Internal**: Checks circuitry only
  - **External** (with loopback plug): Also tests connector

### Telecommunications Room Troubleshooting
- Keep diagnostic process organized and documented
- Start at one end, don't skip connections
- Place sticker as you work to track progress

**Biggest Concerns**:
- **Uninterrupted Power Supply (UPS)**:
  - Monitoring tool
  - Provides security from power spikes and sags
  - Enables shutdown
  
- **Monitoring Tools**:
  - Voltage event recorder
  - Temperature monitoring
  - Environmental monitoring

---

## Key Formulas

**Transmission Time Calculation**:
```
Time = (File Size in Bytes × 8 bits/byte) / Link Speed in bps
```

**Example**: 10 MB over 1 Gbps link
```
(10 MB × 8 bits/byte) / 1 Gbps = 0.08 seconds
```

**Fully-Meshed Topology Connections**:
```
Number of connections = n(n-1)/2
where n = number of devices
```

---

**Last Updated:** February 4, 2026
**Source:** Mike Meyers' Guide to Managing and Troubleshooting Networks
