---
title:
  - Network Operating System
type: Lecture
course:
  - Computer Networks
topic:
  - Network Infrastructure
semester: 4
tags:
  - network-os
  - cisco-ios
  - routing
  - ipv4
  - static-routing
  - packet-tracer
  - computer-networks
created: 2026-03-05
---

# Network Operating System

 **Reference:** Lecture Slides — Network Operating System (CN-2)
 **Source:** [[Network_Operating_System__CN-2_.pdf]]

---

## Table of Contents

1. [[#1. What is a Network Operating System?]]
    - [[#1.1 Operating Systems on Network Devices]]
    - [[#1.2 CLI — Command Line Interface]]
2. [[#2. Simulating IOS with Cisco Packet Tracer]]
    - [[#2.1 A Brief Overview of IPv4 Addressing]]
    - [[#2.2 Designing a Network in Packet Tracer]]
    - [[#2.3 Configuring IPv4 on End Devices]]
    - [[#2.4 Configuring IPv4 on a Router with IOS]]
    - [[#2.5 Configuring Static Routing on a Router]]
    - [[#2.6 Verifying Connectivity]]
    - [[#2.7 Troubleshooting]]
3. [[#Summary — Key Concepts at a Glance]]

---

## 1. What is a Network Operating System?

### 1.1 Operating Systems on Network Devices

Every electronic device — whether it's a PC, a smartphone, or a network device — requires an **operating system (OS)** to function. The operating system is the core software that manages the hardware and provides an interface for users and other programs to interact with the device.

For everyday computers and laptops, the most common operating systems are **Windows**, **macOS**, and **Linux**. For smartphones and tablets, we have **Apple iOS** and **Android**. However, network devices such as [[Router|routers]], [[Switch|switches]], wireless access points, and [[Firewall|firewalls]] also have their own operating systems — only the form and usage differ from what we typically encounter on a PC.

Two of the most widely used network operating systems in industry and education are:

**Cisco IOS (Internetworking Operating System)** is the OS that runs on nearly all network devices manufactured by Cisco, one of the largest networking equipment companies in the world. Cisco IOS is the primary focus of this course, as it is an industry standard and is widely studied for networking certifications such as CCNA.

**MikroTik RouterOS** is a network operating system developed by MikroTik, a Latvia-based company. RouterOS is widely used in Indonesia because of its more affordable pricing compared to Cisco products. RouterOS is also CLI-based but its interface looks slightly different — as shown in the lecture slides, its interface uses a terminal like PuTTY and displays structured text output when you enter commands such as `ipv6 address print` or `ipv6 route print`.

### 1.2 CLI — Command Line Interface

Unlike PC operating systems that use a **GUI (Graphical User Interface)** — a graphics-based interface where you can click icons, open windows, and use a mouse — network operating systems like Cisco IOS generally operate using a **CLI (Command Line Interface)**, a text-based interface where all interaction is done through typed commands.

Why CLI instead of GUI? There are several fundamental reasons. First, CLI is far more efficient in terms of resource consumption — network devices don't need to waste memory and processing power just to render graphics. Second, CLI enables very precise control; every command has a clear function and its result is predictable. Third, CLI can be easily automated through scripts, which is extremely useful when you need to configure hundreds of devices at once.

With CLI on a network operating system, a network technician can:
- Run network programs and features by typing text commands.
- Enter configurations such as IP addresses, routing tables, and security settings.
- View output and device status directly on a monitor or terminal screen.

---

## 2. Simulating IOS with Cisco Packet Tracer

Cisco Packet Tracer (the version used in this course is 9.0.0.0810) is a network simulation software developed by Cisco Systems. It allows us to build, configure, and test computer networks virtually — without needing expensive physical hardware. This is an incredibly valuable learning tool because we can experiment, make mistakes, and learn from them without the risk of damaging real equipment.

### 2.1 A Brief Overview of IPv4 Addressing

Before diving into the simulation, we need to understand the basics of IPv4 addressing, as this is the foundation of all network configurations we will perform.

**What does CIDR notation like `192.168.10.0/24` mean?**

Every device on a network needs a unique **IP (Internet Protocol) address** to be identified and to communicate. An IPv4 address consists of 32 bits, typically written in dotted-decimal format — four decimal numbers separated by dots, e.g., `192.168.10.1`. The number after the slash (`/24`) is called the **prefix length** or **subnet mask in CIDR (Classless Inter-Domain Routing) notation**, and it indicates how many of the 32 total bits are used to identify the **network**, while the remainder are used to identify individual **hosts** (devices) within that network.

For the notation `192.168.10.0/24`, the number 24 means the first 24 bits are the network portion, and the remaining 8 bits (32 - 24 = 8 bits) are the host portion. From this we can calculate:

- **Number of usable hosts** = 2^(32-24) - 2 = 2^8 - 2 = 256 - 2 = **254 hosts**. We subtract 2 because one address is used as the **network address** (the address representing the network itself, which cannot be assigned to a device) and one is used as the **broadcast address** (used to send a message to all devices in the network simultaneously).
- **Network address**: `192.168.10.0/24` — all host bits are set to 0.
- **First host address** (the first IP address usable by a device): `192.168.10.1/24`.
- **Last host address** (the last IP address usable by a device): `192.168.10.254/24`.
- **Broadcast address**: `192.168.10.255/24` — all host bits are set to 1.

**Subnet mask** is another way to express the same thing. For `/24`, the subnet mask is `255.255.255.0`. The value 255 in binary is `11111111`, meaning those 8 bits are entirely part of the network portion. The value 0 means the final 8 bits are the host portion.

This is crucial to understand because every time we configure a network device, we must always enter the IP address along with its subnet mask.

**Topology used in the simulation:**

In this simulation, we work with a network topology consisting of 3 [[Router|routers]] and 4 different subnets (networks):
- **Network 1**: `192.168.1.0/24` — a local network on the Router0 side, connected to PC0 and PC1 through a [[Switch|switch]].
- **Network 2**: `10.0.0.0/8` — a link network between Router0 and Router1. The `/8` prefix means only the first 8 bits are the network portion, so the number of usable hosts is much larger.
- **Network 3**: `11.0.0.0/8` — a link network between Router1 and Router2.
- **Network 4**: `192.168.2.0/24` — a local network on the Router2 side, connected to PC2.

### 2.2 Designing a Network in Packet Tracer

To build the network topology in Cisco Packet Tracer, there are several basic steps to follow:

**Choosing devices:** From the device panel at the bottom of the Packet Tracer interface, select [[Router|router]] model **2911** (this is a Cisco 2900-series router commonly used in simulations) and [[Switch|switch]] model **Switch-PT**. These models are chosen because they support the features we will be learning, including multiple Gigabit Ethernet ports.

**Choosing cable types:** In both real and simulated networks, choosing the correct cable type is important:
- **Straight-through cable** is used to connect devices of different types — for example, a computer to a [[Switch|switch]], or a [[Router|router]] to a [[Switch|switch]]. This is the most commonly used cable.
- **Crossover cable** is used to connect two devices of the same type directly — for example, computer to computer, or [[Router|router]] to [[Router|router]]. Internally, a crossover cable reverses the transmit and receive paths so that both devices can communicate without an intermediary.

**Displaying port (interface) labels:** To make it easier to identify which port is connected to which, you can enable permanent port label display through **Options → Preferences → Interface → Always Show Port Labels in Logical Workspace**. Without this setting, port labels only appear when the cursor hovers over a cable, which can be inconvenient when you need to see the entire topology.

### 2.3 Configuring IPv4 on End Devices

An **end device** is a device that serves as the ultimate source or destination of communication in a network — in this simulation, our end devices are PCs (personal computers). Each end device must be configured with three essential pieces of information:

1. **IP Address** — the unique address that identifies this device within its network.
2. **Subnet Mask** — determines which part of the IP address is the network portion and which is the host portion. For a `/24` network, the subnet mask is `255.255.255.0`.
3. **Default Gateway** — the IP address of the [[Router|router]] that will serve as the "exit door" when this device needs to communicate with another network. Without a default gateway, an end device can only communicate with other devices on the same network.

There are two ways to configure IP settings on an end device in Packet Tracer:

**Method 1 — Through the GUI (IP Configuration):** Click on the PC, open the **Desktop** tab, then click **IP Configuration**. Here you can manually fill in the IP Address, Subnet Mask, Default Gateway, and DNS Server in the provided fields. This method is intuitive and suitable for beginners.

**Method 2 — Through the Command Prompt:** Click on the PC, open the **Desktop** tab, then open **Terminal/Command Prompt**. Type the command:
```
ipconfig <<IPv4 Address>> <<Subnet Mask>> <<Default Gateway>>
```
A concrete example: to configure PC0 with IP `192.168.1.2`, subnet mask `255.255.255.0`, and default gateway `192.168.1.1`, the command is:
```
ipconfig 192.168.1.2 255.255.255.0 192.168.1.1
```

Note that the default gateway must be set to the IP address of the [[Router|router]] interface that is connected to the same network as the PC. PC0 is on Network 1 (`192.168.1.0/24`), and Router0 has an interface on the same network with IP `192.168.1.1`, so PC0's default gateway is `192.168.1.1`. Likewise, PC2, which is on Network 4 (`192.168.2.0/24`), uses the default gateway `192.168.2.1` (the Router2 interface connected to that network).

### 2.4 Configuring IPv4 on a Router with IOS

A [[Router|router]] needs to be configured with an IP address on every **interface** (physical port) that connects to a network. Interfaces on a Cisco 2911 [[Router|router]] are typically named **GigabitEthernet0/0** (abbreviated `Gig0/0`), **GigabitEthernet0/1** (`Gig0/1`), and so on — these are ports with transfer speeds of up to 1 Gigabit per second.

To configure a [[Router|router]], we use the **Cisco IOS CLI** with a hierarchical sequence of commands. Cisco IOS has several different **modes**, and we must be in the correct mode to execute a given command:

**Steps to configure an IP address on a router interface:**

**User EXEC Mode** (`Router>`) is the basic mode when you first log in to the [[Router|router]]. In this mode you can only view limited information; you cannot change the configuration.

**Enter Privileged EXEC mode** with the command:
```
Router>enable
```
The prompt changes to `Router#`. In this mode (indicated by the `#` sign), you have full access to view all information and run diagnostic commands.

**Enter Global Configuration mode** with the command:
```
Router#configure terminal
```
The prompt changes to `Router(config)#`. This is the mode where you can begin modifying the [[Router|router]]'s configuration globally.

**Enter Interface Configuration mode** — for example, for interface Gig0/0:
```
Router(config)#interface gig0/0
```
The prompt changes to `Router(config-if)#`. You are now inside the configuration of that specific interface.

**Assign an IP address to the interface:**
```
Router(config-if)#ip address 192.168.1.1 255.255.255.0
```
This command assigns the IP address `192.168.1.1` with subnet mask `255.255.255.0` to interface Gig0/0.

**Activate the interface:**
```
Router(config-if)#no shutdown
```
By default, interfaces on a Cisco [[Router|router]] are in an **administratively down** state (disabled by default). You must explicitly activate them using the `no shutdown` command (the `no` prefix always means "negate" or "disable" a configuration — in this case, we are "negating the shutdown," which means activating the interface).

**Exit interface configuration mode:**
```
Router(config-if)#exit
```
Repeat the same process for interface Gig0/1 with a different IP according to the connected network. For example, for the interface connected to Network 2:
```
Router(config)#interface gig0/1
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#exit
```

**Commands to verify IP configuration on the router:**

After configuring, we need to ensure the configuration is correct. Two useful commands:

`Router#show interfaces` — displays comprehensive information about all interfaces, including IP address, subnet mask, status (up/down), traffic statistics, and more. The output is very long and detailed.

`Router#show ip interface brief` — displays a brief summary of all interfaces in a table format with columns for Interface, IP-Address, OK?, Method, Status, and Protocol. This is much easier to read when you just want to quickly check IP addresses and interface statuses. From this output you can see whether an interface is `up/up` (active) or still `administratively down/down` (not yet activated).

**Removing an IP configuration:**

If you want to remove an IP address that has already been configured, use the `no` prefix on the same command. For example, to remove IP `192.168.1.1/24` from interface Gig0/0:
```
Router#configure terminal
Router(config)#interface gig0/0
Router(config-if)#no ip address 192.168.1.1 255.255.255.0
```

### 2.5 Configuring Static Routing on a Router

> [!NOTE]
> Routing concepts will be explored in greater depth in Week 7 (Network Layer). This section covers the basic static routing configuration needed for the Packet Tracer simulation.

After every [[Router|router]] interface has been configured with the correct IP address, the [[Router|router]] can already communicate with networks that are directly attached to it (**directly connected networks**). However, the [[Router|router]] does not yet know how to reach networks that are _not_ directly connected. This is where **routing** comes in.

**What is routing?** Routing is the process by which a [[Router|router]] determines the best path to forward data packets from one network to another. The [[Router|router]] stores this information in a table called the **routing table**.

**Static routing** is an approach where we manually tell the [[Router|router]] the path to every network that is not directly connected. The opposite is **dynamic routing** (such as RIP, OSPF, EIGRP) where [[Router|routers]] automatically exchange routing information with each other. Static routing is suitable for small networks whose topology rarely changes, such as the simulation we are working with here.

**Command to add a static route:**
```
Router(config)#ip route <<Network Address>> <<Mask>> <<Next Hop>>
```
- **Network Address** — the address of the destination network you want to reach.
- **Mask** — the subnet mask of the destination network.
- **Next Hop** — the IP address of the next [[Router|router]] (neighbor) that must be traversed to reach the destination network. This is the IP address of the neighboring [[Router|router]]'s interface that is directly connected to ours.

**Complete configuration example for all three routers:**

**Router0** (has direct access to Network 1 and Network 2; needs routes to Network 3 and Network 4):
```
Router>enable
Router#configure terminal
Router(config)#ip route 11.0.0.0 255.0.0.0 10.0.0.2
Router(config)#ip route 192.168.2.0 255.255.255.0 10.0.0.2
```
Explanation: Router0 is connected to Router1 through Network 2. The IP of Router1's interface facing Router0 is `10.0.0.2`. Therefore, to reach Network 3 (`11.0.0.0/8`) or Network 4 (`192.168.2.0/24`), Router0 must forward packets to `10.0.0.2` (Router1), because Router1 knows how to forward them further.

**Router1** (connected to Network 2 and Network 3; needs routes to Network 1 and Network 4):
```
Router>enable
Router#configure terminal
Router(config)#ip route 192.168.1.0 255.255.255.0 10.0.0.1
Router(config)#ip route 192.168.2.0 255.255.255.0 11.0.0.2
```
Explanation: To reach Network 1 (`192.168.1.0/24`), Router1 must forward to `10.0.0.1` (Router0's interface on Network 2). To reach Network 4 (`192.168.2.0/24`), Router1 forwards to `11.0.0.2` (Router2's interface on Network 3).

**Router2** (connected to Network 3 and Network 4; needs routes to Network 2 and Network 1):
```
Router>enable
Router#configure terminal
Router(config)#ip route 10.0.0.0 255.0.0.0 11.0.0.1
Router(config)#ip route 192.168.1.0 255.255.255.0 11.0.0.1
```
Explanation: To reach Network 2 (`10.0.0.0/8`) and Network 1 (`192.168.1.0/24`), Router2 must forward packets to `11.0.0.1` (Router1's interface on Network 3).

**Checking the routing table:**

To view all routes known to the [[Router|router]] (both directly connected and static):
```
Router>show ip route
```
The output of this command includes a legend at the top explaining the meaning of each letter code: `C` = connected (directly connected), `L` = local, `S` = static, `R` = RIP, `O` = OSPF, `D` = EIGRP, and so on. This information is important for understanding the origin of each route.

To view only the static routes that we have configured:
```
Router>show ip route static
```

### 2.6 Verifying Connectivity

After all IP and routing configurations are complete, the next step is to verify that the network is actually working — that devices on different networks can communicate with each other. There are three ways to do this:

**Method 1 — Ping from an End Device:**

**Ping** is one of the most fundamental network diagnostic tools. How it works: the sending device transmits a small packet called an **ICMP Echo Request** to the destination IP address, and if the network is functioning properly, the destination device replies with an **ICMP Echo Reply**. If the reply is received, the connection between the two devices is confirmed to be working.

From the Command Prompt on a PC in Packet Tracer, type:
```
ping <<Destination IP>>
```
Example: to ping from PC0 (IP `192.168.1.2`) to PC2 (IP `192.168.2.2`), open the Command Prompt on PC0 and type:
```
ping 192.168.2.2
```
If successful, the output will display four lines of "Reply from 192.168.2.2: bytes=32 time<1ms TTL=125," meaning the packet successfully made the round trip. At the bottom there will be a statistics summary: Sent = 4, Received = 4, Lost = 0 (0% loss) — an ideal result since no packets were lost.

**Method 2 — Ping from a Router:**

A [[Router|router]] can also perform a ping directly from its CLI. From User EXEC or Privileged EXEC mode, type:
```
ping <<Destination IP>>
```
Example from Router0 pinging PC2:
```
Router>ping 192.168.2.2
```
The ping output from a [[Router|router]] looks slightly different. A Cisco [[Router|router]] sends 5 ICMP packets, and each packet that receives a reply is displayed as an exclamation mark (`!`). If the connection is fully successful, the output will look like `!!!!!` (five exclamation marks) followed by "Success rate is 100 percent (5/5), round-trip min/avg/max = 1/5/16 ms."

**Method 3 — Using Add Simple PDU:**

Packet Tracer also provides a visual feature for testing connections using a **Simple PDU** (Protocol Data Unit). Click the envelope icon with a lightning bolt in the toolbar, then click the source device followed by the destination device. Packet Tracer will display a table with columns including Fire, Last Status, Source, Destination, Type, and others. If the connection is successful, the Last Status column will show **Successful**.

### 2.7 Troubleshooting

During the process of configuring and testing a network, you will often need to cancel a running command — for example, a ping sent to an address that hasn't been configured, which never receives a reply, causing the ping program to wait indefinitely.

To cancel a running command in Cisco IOS, use:
- **CTRL+C** — the first method to try. This is the standard interrupt signal that stops the running process.
- **CTRL+SHIFT+6** — if CTRL+C doesn't work, this key combination is a special Cisco IOS escape sequence that forces cancellation of a process, including a ping that is waiting for a reply.

As an example: if you accidentally type `ping 192.168.4.2` from Router0 when that address hasn't been configured on any network, the [[Router|router]] will attempt to send the ping and wait for a reply that will never come. The output will display "Success rate is 0 percent (0/1)" after a timeout. To stop this process before the timeout, press CTRL+SHIFT+6.

---

## Summary — Key Concepts at a Glance

| Concept | Definition |
| --- | --- |
| Network Operating System | A specialized OS for network devices ([[Router|routers]], [[Switch|switches]], etc.), e.g., Cisco IOS and MikroTik RouterOS |
| Cisco IOS | Cisco's operating system that runs on Cisco [[Router|routers]] and [[Switch|switches]]; operated via CLI |
| MikroTik RouterOS | An alternative network OS by MikroTik; its CLI interface can be accessed via PuTTY |
| CLI (Command Line Interface) | A text-based interface; all interaction is done by typing commands, not clicking with a mouse |
| GUI (Graphical User Interface) | A graphics-based interface like Windows/macOS; not commonly used on network devices |
| IPv4 Address | A 32-bit address that identifies a device on a network, written in dotted-decimal format (e.g., 192.168.1.1) |
| Subnet Mask | A value that determines the network and host portions of an IP address (e.g., 255.255.255.0 for /24) |
| CIDR Notation | A shorthand for writing subnet masks with a prefix length (e.g., /24 = 255.255.255.0) |
| Network Address | The first address in a subnet (all host bits = 0); cannot be assigned to a device |
| Broadcast Address | The last address in a subnet (all host bits = 1); used to send to all devices in the network |
| Default Gateway | The IP address of the [[Router|router]] that serves as the "exit door" for an end device to communicate outside its network |
| Interface | A physical port on a [[Router|router]] (e.g., GigabitEthernet0/0); each active interface must be configured with an IP |
| `no shutdown` | A Cisco IOS command to activate an interface that is in a default disabled state |
| Static Routing | Manually configured routing; the admin specifies the path to each destination network |
| Next Hop | The IP address of the neighboring [[Router|router]] to which packets are forwarded in a static route configuration |
| Routing Table | A table stored inside a [[Router|router]] that holds all information about known networks and how to reach them |
| Ping | An ICMP-based diagnostic tool for testing whether two devices can communicate |
| ICMP | Internet Control Message Protocol; the protocol used by the ping command |
| Cisco Packet Tracer | Cisco's network simulation software for learning and practicing IOS configuration without physical hardware |
| `show ip interface brief` | An IOS command to view a summary of IP addresses and statuses for all [[Router|router]] interfaces |
| `show ip route` | An IOS command to view the entire routing table of a [[Router|router]] |
| `show ip route static` | An IOS command to view only the static routes that have been configured |

---

## Questions
1. What is the fundamental difference between static routing and dynamic routing, and when should each be used?
2. Why are interfaces on a Cisco [[Router|router]] in an `administratively down` state by default? What is the design rationale behind this?
3. In the 3-router topology, why doesn't Router0 need to know the specific location of Network 3 — and only needs to know that the next hop is Router1?
4. What happens if static route configuration is asymmetric — for example, Router0 knows how to reach Network 4 but Router2 doesn't know how to reach Network 1?
5. What is the difference between a straight-through cable and a crossover cable, and how do modern devices handle this difference automatically (Auto-MDIX)?
