# 🗺️ Network Operating System & Cisco Packet Tracer — Learning Roadmap

> Aligned with your **Jaringan Komputer (Computer Networks)** syllabus — Semester 4, Informatika UNS.

---

## How to Use This Roadmap

Each phase maps to your [[RPS-CN|RPS weekly schedule]]. Phases contain **Theory** (concepts to master) and **🖥️ Packet Tracer Labs** (hands-on exercises). Check off items as you complete them.

---

## Phase 1 — Foundations (Week 1–2)

> **Goal:** Understand *why* networks exist, what the building blocks are, and get comfortable with the Cisco IOS CLI.

### Theory

- [x] Network components: hosts, end devices, intermediary devices
  - your existing note → [[Pengenalan Jaringan Komputer — CN — 1]]
- [ ] Roles of [[Switch]] vs [[Router]]
- [ ] LAN vs WAN vs Internet / Intranet / Extranet
- [ ] What a Network OS is (Cisco IOS, MikroTik RouterOS)
- [x] IOS CLI modes: User EXEC → Privileged EXEC → Global Config → Interface Config
  - your existing note → [[Network Operating System — CN — 2]]

### 🖥️ Packet Tracer Labs

| # | Lab | Key Skills |
|---|-----|-----------|
| 1 | **Hello Packet Tracer** — Place 2 PCs + 1 Switch, connect with straight-through cables, assign IPs via GUI, ping between PCs | Device placement, cable types, IP config on end devices |
| 2 | **CLI First Steps** — Open a Router CLI, practice `enable`, `configure terminal`, `show ip interface brief`, `exit` | Navigating IOS modes |
| 3 | **Basic Router Setup** — Recreate the 3-router + 4-subnet topology from your lecture, configure IPs on all interfaces | `interface gig0/0`, `ip address`, `no shutdown` |

---

## Phase 2 — IP Addressing & Static Routing (Week 2–4)

> **Goal:** Master IPv4 addressing, subnetting basics, and configure routers so packets can travel across multiple networks.

### Theory

- [x] IPv4 address structure, dotted-decimal ↔ binary conversion
- [x] CIDR notation & subnet masks (`/24` = `255.255.255.0`)
- [x] Network address, broadcast address, usable host range
- [x] What routing is — routing table, directly connected vs static routes
- [x] Next-hop concept
- [ ] Reference models overview: [[OSI Model]] & [[TCP-IP Model]]
- [ ] Data encapsulation & de-encapsulation across layers

### 🖥️ Packet Tracer Labs

| # | Lab | Key Skills |
|---|-----|-----------|
| 4 | **Static Routing End-to-End** — Using the 3-router topology, add static routes so PC0 can ping PC2 across all networks | `ip route`, `show ip route`, `show ip route static` |
| 5 | **Troubleshooting Challenge** — Intentionally mis-configure one route or IP, then diagnose with `ping`, `show ip interface brief`, and `show ip route` | Systematic debugging |
| 6 | **Subnet Calculator** — Given `172.16.0.0/16`, calculate and configure 4 subnets, assign IPs, verify with ping | Subnetting math, address planning |

---

## Phase 3 — Network Access & Ethernet (Week 5–7)

> **Goal:** Understand how data actually travels on the wire (Physical & Data Link layers) and how switches forward frames.

### Theory

- [ ] Physical layer: copper (UTP), fiber optic, wireless media
- [ ] Ethernet frame structure & MAC addresses
- [ ] How a Switch builds and uses its MAC address table
- [ ] ARP (Address Resolution Protocol) — mapping IP → MAC
- [ ] Difference between straight-through, crossover, and Auto-MDIX
- [ ] Network Layer deep-dive: IPv4 header, IPv6 introduction
- [ ] Router packet-forwarding process

### 🖥️ Packet Tracer Labs

| # | Lab | Key Skills |
|---|-----|-----------|
| 7 | **ARP in Action** — Build a LAN, use Simulation Mode to watch ARP Request/Reply and observe MAC address table on the Switch | Simulation mode, `show mac address-table` |
| 8 | **Cable Type Challenge** — Build a topology requiring both straight-through & crossover cables; verify with link lights | Cable selection |
| 9 | **Multi-Router Packet Walk** — Use Simulation Mode to trace a ping packet hop-by-hop across 3 routers; note encapsulation changes at each layer | Encapsulation, PDU inspection |

---

## Phase 4 — Intermediate Topics (Week 9–13)

> **Goal:** Deepen IP addressing skills (subnetting, VLSM), understand Transport & Application layers, and build more complex topologies.

### Theory

- [ ] Binary/decimal/hex conversions for IP addresses
- [ ] Subnetting: fixed-length & VLSM (Variable Length Subnet Masking)
- [ ] IPv6 addressing fundamentals
- [ ] ICMP & `ping` / `traceroute` internals
- [ ] Transport Layer: TCP vs UDP, connection-oriented vs connectionless
- [ ] TCP 3-way handshake, flow control, windowing
- [ ] Application Layer protocols: HTTP, DNS, DHCP, FTP, SMTP/POP3
- [ ] Client-server interactions at the application level

### 🖥️ Packet Tracer Labs

| # | Lab | Key Skills |
|---|-----|-----------|
| 10 | **VLSM Network Design** — Given a company with 4 departments of different sizes, subnet `192.168.1.0/24` efficiently using VLSM | Address planning, waste minimization |
| 11 | **DNS & HTTP Server** — Add a server to your topology, configure DNS + HTTP services, browse from a PC | Server configuration in PT, DNS resolution |
| 12 | **DHCP Server** — Configure a router or server as DHCP server so PCs get IPs automatically | `ip dhcp pool`, `network`, `default-router` |
| 13 | **TCP vs UDP Simulation** — Use Simulation Mode to compare a TCP connection (HTTP) vs a UDP connection (DNS), observe the 3-way handshake | Protocol analysis |
| 14 | **Traceroute** — Use `tracert` / `traceroute` to map the path between distant PCs | Hop-by-hop analysis |

---

## Phase 5 — Capstone: Building a Small Network (Week 14–15)

> **Goal:** Integrate everything into a realistic small-network project — design, implement, secure, test, and document.

### Theory

- [ ] Network design principles (hierarchy, redundancy, documentation)
- [ ] Basic security: Access Control Lists (ACL), password on console/VTY lines
- [ ] [[Firewall]] concepts & simple packet filtering
- [ ] Performance testing & troubleshooting methodology

### 🖥️ Packet Tracer Labs

| # | Lab | Key Skills |
|---|-----|-----------|
| 15 | **Small Office Network** — Design and build a network for a 3-department office: separate subnets, a router with static routes, a DHCP & DNS server, and end devices in each department | Full lifecycle: plan → build → configure → test |
| 16 | **Security Hardening** — Add console & VTY passwords, enable SSH, create a basic ACL to block specific traffic | `line console 0`, `password`, `access-list` |
| 17 | **Break-Fix Final** — Receive a pre-built topology with 5+ intentional errors; find and fix them all | Troubleshooting mastery |

---

## 📚 Key Resources

| Resource | Location |
|----------|----------|
| Course Syllabus (RPS) | [[RPS-CN]] |
| Lecture Slides — NOS | [[Network_Operating_System__CN-2_.pdf]] |
| Lecture Slides — Packet Tracer | [[Cisco Packet Tracer (CN-P-2).pdf]] |
| Cisco Ref Book | Iwan Sofana, *Cisco CCNA & Jaringan Komputer* (2014) |
| Cisco ITN v7 | *CCNA Introduction To Networks v7* (2016) |

## 🔑 IOS Command Cheat Sheet

| Command | Purpose |
|---------|---------|
| `enable` | Enter Privileged EXEC mode |
| `configure terminal` | Enter Global Config mode |
| `interface gig0/0` | Enter interface config |
| `ip address <IP> <MASK>` | Set IPv4 address |
| `no shutdown` | Activate interface |
| `ip route <NET> <MASK> <NEXT-HOP>` | Add static route |
| `show ip interface brief` | Quick interface summary |
| `show ip route` | View routing table |
| `show running-config` | View current config |
| `ping <IP>` | Test connectivity |
| `traceroute <IP>` | Trace packet path |
| `copy running-config startup-config` | Save config to NVRAM |

---

> [!TIP]
> After each lab, write a short reflection in your Obsidian vault — what went wrong, what you learned, and any IOS commands you want to memorize. This builds your Zettelkasten over time.
