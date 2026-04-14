---
title:
  - Pengenalan Jaringan Komputer
type: Lecture
course:
  - Computer Networks
topic:
  - Network Fundamentals
semester: 4
tags:
  - computer-networks
  - networking
  - college
  - lecture-note
status: 🌿 incubating
created: 2026-03-04
---

# Pengenalan Jaringan Komputer

 **Reference:** Cisco CCNAv7 – Introduction to Networks (ITN) Companion Guide
 **Source:** [[Pengenalan Jaringan Komputer (CN-1).pdf]]

---

## Daftar Isi

1. [[#1. Networking Today — Why Networks Matter]]
2. [[#2. Komponen Jaringan Komputer (Network Components)]]
    - [[#2.1 Peran Host (The Role of Hosts)]]
    - [[#2.2 Peer-to-Peer (P2P)]]
    - [[#2.3 End Device]]
    - [[#2.4 Intermediary Device]]
    - [[#2.5 Switch & Router — The Two Most Important Devices]]
    - [[#2.6 Media Jaringan Komputer (Network Media)]]
3. [[#3. Jenis-jenis Jaringan Komputer (Types of Computer Networks)]]
    - [[#3.1 LAN (Local Area Network)]]
    - [[#3.2 WAN (Wide Area Network)]]
    - [[#3.3 Comparison LAN vs. WAN]]
    - [[#3.4 Internet]]
    - [[#3.5 Intranet]]
    - [[#3.6 Extranet]]
4. [[#4. Internet Connection — Converged Network]]
    - [[#4.1 What Was the Problem Before Convergence?]]
    - [[#4.2 What Is a Converged Network?]]
5. [[#5. Reliable Network — Network Architecture]]
    - [[#5.1 What Is Network Architecture?]]
    - [[#5.2 Fault Tolerance]]
    - [[#5.3 Scalability]]
    - [[#5.4 Quality of Service (QoS)]]
    - [[#5.5 Security]]
6. [[#6. Network Trends]]
    - [[#6.1 Bring Your Own Device (BYOD)]]
    - [[#6.2 Online Collaboration]]
    - [[#6.3 Cloud Computing (Komputasi Awan)]]
7. [[#Summary — Key Concepts at a Glance]]

---

## 1. Networking Today — Why Networks Matter

At the most fundamental level, computer networks exist because humans need to communicate — and communication, in the modern world, is nearly as essential as food, water, and shelter. Networks allow us to send messages, share files, access information, and collaborate with people who are physically far away, in ways that were impossible just a few decades ago.

The key insight here is that a **network** is not just cables and routers — it is the infrastructure that enables human connection at a global scale. The moment you send a message on WhatsApp, stream a video, or open a webpage, you are depending on a chain of networked devices working in coordination.

---

## 2. Komponen Jaringan Komputer (Network Components)

Every network, no matter how large or small, is built from the same basic building blocks. Understanding these components is essential before you can understand how networks behave.

### 2.1 Peran Host (The Role of Hosts)

Every computer connected to a network is called a **host** or an **end device**. The word "host" captures the idea that the device either _hosts_ (provides) a service, or it is the _recipient_ of one.

Hosts can play two roles:

**Server:** A server is a computer whose primary job is to provide information or services to other devices on the network. It sits and _waits_ for requests, then fulfills them. Examples include:

- **Email server** — stores and forwards email messages
- **Web server** — delivers web pages when a browser requests them
- **File server** — stores files that can be accessed by other devices on the network

The server does not initiate communication; it responds to it.

**Client:** A client is a computer that _initiates_ requests to a server in order to retrieve information or use a service. When you open a browser and type a URL, your computer is acting as a client — it sends a request to a web server and waits for the page to come back. When you open your email app, your device is a client querying an email server.

This **client-server model** underpins most of the internet as we know it.

### 2.2 Peer-to-Peer (P2P)

The client-server model assumes a clear division of roles. But there is an alternative: the **Peer-to-Peer (P2P)** model, where a single device can function as _both_ a client and a server at the same time.

Imagine two computers in a small home network. Computer A shares its printer, making it a "server" of printer resources. Computer B shares its music folder, making it a "server" of files. But both can also _request_ from each other, making each a client too.

P2P is recommended only for **very small networks** because it doesn't scale well. As the number of devices grows, the absence of a dedicated server creates confusion and performance problems — every device must manage its own resources while also serving others. ^42d1a3

### 2.3 End Device

An **end device** (also called an end node) is the source or destination of all data in a network. It is where communication begins and where it ends. Data originates at an end device, travels through the network infrastructure, and arrives at another end device.

Think of end devices as the "edges" of the network — computers, phones, printers, IP cameras, smart TVs. They don't _route_ or _relay_ traffic for others (that's the job of intermediary devices); they generate or consume it.

### 2.4 Intermediary Device

**Intermediary devices** sit _between_ end devices and are responsible for moving data through the network. They don't originate or consume data — they relay it. Examples include:

- **[[Switch]]** — connects devices within the same local network
- **Wireless Access Point (WAP)** — allows wireless devices to connect to the network
- **Router** — connects different networks together
- **[[Firewall]]** — monitors and controls traffic for security purposes

What do intermediary devices actually do? Their responsibilities include:

1. **Regenerating and retransmitting data signals** — signals weaken over distance; intermediary devices boost and forward them.
2. **Maintaining information about available network paths** — they "know" the map of the network.
3. **Notifying other devices of errors and communication failures** — if a link goes down, they alert the rest of the network.
4. **Redirecting data through alternate paths when a failure occurs** — like a GPS rerouting around a traffic jam.
5. **Classifying and directing messages according to priority** — some data (like voice calls) needs to arrive faster than others (like email).
6. **Permitting or denying data flow based on security settings** — enforcing who is allowed to talk to whom.

### 2.5 [[Switch]] & Router — The Two Most Important Devices

When building a small office network, the two most critical pieces of hardware are the **[[Switch|switch]]** and the **router**. They serve complementary but distinct purposes.

**[[Switch]]:** A [[Switch|switch]] connects all the devices _within_ a single network (like all the computers and printers in one office). It creates a shared space where those devices can communicate with each other. When a packet arrives at a [[Switch|switch]], the [[Switch|switch]] reads the destination address and forwards it only to the correct device — unlike older technology (hubs) that would broadcast to everyone. This makes [[Switch|switches]] efficient.

**[[Router]]:** A router connects _multiple networks_ (or multiple [[Switch|switches]]) together. Think of a [[Switch|switch]] as connecting rooms within a building, and a router as connecting different buildings. A router also provides the gateway to the **internet**. Without a router, your office network would be an island — isolated from everything else.

Additional roles of a router:

- Acts as a **dispatcher**, choosing the most efficient route for packets to travel across the network.
- Can assign **priority** to different devices or types of traffic — for example, giving video conferencing traffic priority over file downloads.

### 2.6 Media Jaringan Komputer (Network Media)

Data traveling through a network must physically move from one place to another. That movement happens through **network media** — the physical channels that carry the signals. There are three types:

**1. Kabel Logam / Metal Cable (e.g., Copper):** Copper wires are the most traditional form of network media. Data is encoded as **electrical impulses** — variations in voltage that represent binary 0s and 1s. Ethernet cables (like the Cat5e or Cat6 cables you might plug into a laptop) are copper-based. Copper is cheap and easy to work with, but is susceptible to electromagnetic interference and has distance limitations.

**2. Kabel Serat Kaca / Fiber Optic:** Instead of electricity, fiber optic cables carry data as **pulses of light**. The cable itself is made of extremely thin strands of glass or plastic. Because light travels faster and experiences less signal loss than electrical signals, fiber optic cables can carry data over much longer distances at much higher speeds. They are used in backbone infrastructure — the "highways" of the internet.

**3. Transmisi Nirkabel / Wireless Transmission:** Wireless networks encode data as **electromagnetic waves**, using modulation of specific radio frequencies (like 2.4 GHz or 5 GHz in Wi-Fi). There are no physical cables; the signal travels through the air. This offers flexibility (devices can move around), but is more susceptible to interference and security risks compared to wired connections.

---

## 3. Jenis-jenis Jaringan Komputer (Types of Computer Networks)

Not all networks are the same size. Networks are classified by geographic scope, ownership, and the kind of connections they use.

### 3.1 LAN (Local Area Network)

A **Local Area Network (LAN)** is a network that spans a small geographic area — typically a single building, floor, or campus. A home network, a school computer lab, or an office floor are all examples of LANs.

Key characteristics:

- Connects end devices in a **limited area**
- Managed by a **single organization or individual** (you own and control it)
- Provides **high-speed bandwidth** to internal devices — speeds of 1 Gbps or more are common

LANs are relatively inexpensive to set up and offer high performance because the distances involved are short.

### 3.2 WAN (Wide Area Network)

A **Wide Area Network (WAN)** spans a large geographic area — cities, countries, or even continents. The internet itself is the largest WAN in existence. When your office in Surakarta needs to communicate with a branch in Jakarta, the traffic travels over a WAN.

Key characteristics:

- Connects **multiple LANs** across large distances
- Typically managed by **one or more service providers** (ISPs, telcos) — you don't own the infrastructure, you rent access to it
- Generally provides **lower bandwidth** than LANs, because the links are longer and more expensive to provision

### 3.3 Comparison: LAN vs. WAN

|Aspect|LAN|WAN|
|---|---|---|
|Geographic scope|Small (building, campus)|Large (city, country, global)|
|Management|Single org / individual|Service providers|
|Bandwidth|High|Relatively lower|
|Ownership|You own the infrastructure|You lease from providers|

### 3.4 Internet

The **internet** is not a single network — it is a massive, interconnected collection of LANs and WANs spanning the entire globe. Every home network, every corporate network, every university network is a LAN. Those LANs connect to WANs (via routers and ISPs), and those WANs connect to each other, forming the internet.

The physical media used to carry data across these WANs includes copper cables, fiber optic cables, and wireless (including satellite) transmission.

### 3.5 Intranet

An **intranet** is a private network that looks and behaves like the internet, but is restricted to members of a specific organization. Only employees (or other authorized users) can access it. Companies use intranets for internal communication, document sharing, HR portals, and other internal tools that should not be publicly accessible.

The critical distinction: an intranet is _private_ — it uses the same web-based technologies as the internet but is [[Firewall|firewalled]] off from public access.

### 3.6 Extranet

An **extranet** extends a company's intranet to _carefully selected outsiders_ — suppliers, contractors, customers, or partner organizations who need secure access to specific parts of the company's network.

The key difference from an intranet is that the extranet is accessible to _trusted external parties_, not just internal employees. It's more open than an intranet, but more restricted than the public internet.

Practical examples of extranets:

- A manufacturing company giving suppliers access to inventory and ordering systems
- A hospital providing an online booking system that doctors at external clinics can use to schedule patient appointments
- A regional education office granting individual schools access to specific budget reports and administrative data

The diagram from the lecture illustrates this as three concentric circles: the innermost is the **Intranet** (company only), the middle ring is the **Extranet** (suppliers, customers, collaborators), and the outermost is the **Internet** (the whole world).

---

## 4. Internet Connection — Converged Network

### 4.1 What Was the Problem Before Convergence?

Historically, organizations ran _separate networks_ for different types of communication. Telephone calls traveled over telephone networks. Video traveled over broadcast networks. Computer data traveled over computer networks. Each of these networks:

- Had its own dedicated **physical cabling**
- Used its own **technology** for transmitting signals
- Operated according to its own **rules and standards**

This was expensive, complicated to maintain, and inefficient. Every service required its own infrastructure.

### 4.2 What Is a Converged Network?

A **converged network** solves this problem by carrying _all_ types of communication — data, voice, and video — over a _single, unified_ network infrastructure using a _single set of rules and standards_.

This is why modern internet connections can carry your phone call (VoIP), your Netflix stream, your file downloads, and your video conference simultaneously, all over the same cable or wireless connection.

The benefits are significant: organizations no longer need to maintain separate cable plants, separate expertise teams, or separate hardware for each communication type. Everything runs over one unified platform.

---

## 5. Reliable Network — Network Architecture

### 5.1 What Is Network Architecture?

**Network architecture** refers to the technologies, standards, and design decisions that support the infrastructure carrying data through a network. It is not just about the physical hardware — it encompasses the principles that determine how the network behaves.

To meet the expectations of users (who expect networks to be fast, always available, and secure), network architects must design for four fundamental characteristics:

### 5.2 Fault Tolerance

**Fault tolerance** is the ability of a network to continue operating — with minimal disruption — even when one or more of its components fail. A fault-tolerant network is designed for resilience.

How is this achieved? By building in **redundancy** — multiple paths between a source and a destination. If one path fails (because a router crashes or a cable is cut), traffic is automatically rerouted through an alternative path. From the user's perspective, nothing breaks — the experience is unaffected.

This is why critical internet infrastructure has so many interconnected routers and cables. The internet was originally designed by ARPA (the U.S. military research agency) with fault tolerance in mind — it needed to keep working even if parts of it were destroyed. The same principle applies at every level of modern network design.

### 5.3 Scalability

**Scalability** means that a network can grow — adding new users, devices, and applications — without degrading the performance experienced by existing users.

This is possible because network designers follow established **standards and protocols** (agreed-upon rules for how data is formatted, transmitted, and interpreted). Because everyone follows the same standards, new devices from any vendor can be added to the network without needing to redesign everything from scratch.

Think of it like electrical sockets: because sockets are standardized, you can plug in any new appliance without rewiring your house. Similarly, because networking protocols are standardized, a new device can join a network seamlessly.

### 5.4 Quality of Service (QoS)

**Quality of Service (QoS)** is a set of mechanisms that ensure the network delivers an acceptable experience for all users and all types of traffic, even under load.

Not all network traffic is equal. Downloading a file can tolerate delays — if it takes an extra second, you probably won't notice. But a live phone call or video conference cannot tolerate delays — even a fraction of a second of lag is perceptible and disruptive.

When a network is **congested** (demand for bandwidth exceeds available bandwidth), QoS allows routers to _prioritize_ certain types of traffic. Voice and video packets jump the queue; file download packets wait. This ensures that critical, time-sensitive communication remains smooth even when the network is under stress.

Without QoS, congestion would affect everyone equally — your phone call would break up just as much as your file download would slow down.

### 5.5 Security

Network security is a broad topic, but the lecture distinguishes two primary dimensions:

**Keamanan Infrastruktur Jaringan (Network Infrastructure Security):**

- Physical security of network devices — ensuring that routers, [[Switch|switches]], and servers are in locked, access-controlled locations
- Preventing unauthorized access to the devices themselves (e.g., requiring authentication to log into a router)

**Keamanan Informasi (Information Security):**

- Protecting the _data_ that flows through the network from being intercepted, modified, or destroyed

The three goals of information security form the **CIA Triad**:

1. **Confidentiality (Kerahasiaan):** Only the intended recipient can read the data. Achieved through encryption.
2. **Integrity (Integritas):** The data is not altered during transmission. Achieved through hashing and digital signatures.
3. **Availability (Ketersediaan):** Authorized users can access the data when they need it. Achieved through redundancy, backups, and protection against denial-of-service attacks.

**Internal Threats** (threats from within the organization):

- Lost or stolen devices (laptops, phones) containing sensitive data
- Accidental misuse by employees (e.g., clicking a phishing link)
- Malicious insiders (employees intentionally leaking or sabotaging data)

**External Threats** (threats from outside):

- Viruses, worms, and Trojan horses — malicious software that spreads through networks
- Spyware and adware — software that covertly collects information or displays unwanted content
- Zero-day attacks — exploiting vulnerabilities that are not yet publicly known or patched
- Threat actor attacks — deliberate attacks by hackers or criminal organizations
- Denial of Service (DoS) attacks — flooding a server with requests to make it unavailable to legitimate users
- Data interception — eavesdropping on network traffic
- Identity theft — stealing credentials or personal information

**Security Tools:** For home and small office networks:

- **Antivirus and antispyware software** on end devices
- **[[Firewall]]** to block unauthorized access

For larger networks, additional tools include:

- **Dedicated [[Firewall]] systems**
- **Access Control Lists (ACL)** — rules that specify which traffic is allowed or denied
- **Intrusion Prevention Systems (IPS)** — active systems that detect and block attacks in real time
- **Virtual Private Networks (VPN)** — encrypted tunnels that allow secure remote access

---

## 6. Network Trends

### 6.1 Bring Your Own Device (BYOD)

**BYOD** is a policy (and a trend) where employees or students are allowed — or even encouraged — to use their own personal devices (laptops, tablets, smartphones, e-readers) to access organizational resources.

The advantage is flexibility: people work on devices they are already familiar and comfortable with. The challenge is security: personal devices are outside the organization's direct control, potentially creating vulnerabilities.

### 6.2 Online Collaboration

Modern networks enable **online collaboration** — the ability for multiple people in different physical locations to work together on shared projects in real time. Tools like **Cisco Webex**, **Zoom**, and **Google Meet** exemplify this trend. This was made possible by converged networks that can carry high-quality video and audio alongside data.

### 6.3 Cloud Computing (Komputasi Awan)

**Cloud computing** refers to storing data, running applications, and accessing computing resources over the internet — specifically, on servers located in **data centers** — rather than on a local hard drive or local server.

Key capabilities of cloud computing:

- Store personal files or back up data remotely (e.g., Google Drive, iCloud)
- Access applications through a browser without installing them locally (e.g., Google Docs)
- Enable businesses to deliver data to any device, anywhere in the world

Cloud computing is made possible by massive **data centers** — large facilities housing thousands of servers. Small businesses that cannot afford to build their own data center can simply rent server space and storage from major cloud providers (AWS, Google Cloud, Azure), paying only for what they use. This drastically lowers the barrier to entry for deploying internet services.

---

## Summary — Key Concepts at a Glance

| Concept             | Definition                                                             |
| ------------------- | ---------------------------------------------------------------------- |
| Host / End Device   | Any device that is a source or destination of network data             |
| Server              | Device that provides services/data to clients                          |
| Client              | Device that requests services/data from a server                       |
| P2P                 | Network model where devices act as both client and server              |
| Intermediary Device | Device that relays data between end devices ([[Switch]], router, [[Firewall]] ) |
| [[Switch]]              | Connects devices within the same local network                         |
| Router              | Connects different networks; provides internet access                  |
| LAN                 | Network covering a small geographic area                               |
| WAN                 | Network covering a large geographic area                               |
| Internet            | Global collection of interconnected LANs and WANs                      |
| Intranet            | Private network accessible only to org members                         |
| Extranet            | Private network with controlled access for trusted external parties    |
| Converged Network   | Single network infrastructure carrying data, voice, and video          |
| Fault Tolerance     | Network's ability to survive and recover from failures                 |
| Scalability         | Network's ability to grow without degrading performance                |
| QoS                 | Mechanism for prioritizing traffic to ensure reliable delivery         |
| Security (CIA)      | Confidentiality, Integrity, Availability of data                       |
| BYOD                | Policy allowing personal devices for work/study                        |
| Cloud Computing     | Using remote servers via the internet for storage and applications     |

## Questions
1. In [[#2.2 Peer-to-Peer (P2P) |P2P]] section, it is said that "[[#^42d1a3 |the absence of a dedicated server creates confusion and performance problems]]". What does it mean by **confusion and performance problems** ?