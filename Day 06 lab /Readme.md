readme_content = """# CCNA 200-301 Lab Day 06: ARP & Switch MAC Address Table Operations

Welcome to the **CCNA Day 06 Lab** guide! This repository contains a detailed walkthrough, verification steps, and command reference based on **Jeremy's IT Lab** series for the Cisco Certified Network Associate (CCNA 200-301) exam.

---

## 📑 Table of Contents
- [Lab Overview & Objectives](#-lab-overview--objectives)
- [Topology Overview](#-topology-overview)
- [Step-by-Step Lab Walkthrough](#-step-by-step-lab-walkthrough)
  - [Step 1: ARP Resolution & Broadcast/Unicast Frame Flow](#step-1-arp-resolution--broadcastunicast-frame-flow)
  - [Step 2: ICMP Ping Verification](#step-2-icmp-ping-verification)
  - [Step 3: Inspecting the Switch MAC Address Table](#step-3-inspecting-the-switch-mac-address-table)
  - [Step 4: Filtering MAC Address Table Entries](#step-4-filtering-mac-address-table-entries)
  - [Step 5: Clearing Dynamic MAC Address Table Entries](#step-5-clearing-dynamic-mac-address-table-entries)
 
---

## 🎯 Lab Overview & Objectives

In local area networks (LANs), Layer 2 Ethernet communication relies on knowing the destination MAC address of the target device. When a host knows a destination IPv4 address but lacks the corresponding MAC address, it uses the **Address Resolution Protocol (ARP)**. Simultaneously, Layer 2 switches dynamically populate and manage their **MAC Address Table** (CAM Table) to optimize frame forwarding.

### Core Objectives:
1. **Analyze ARP Operations**: Observe ARP Request broadcasts (`FF:FF:FF:FF:FF:FF`) and ARP Reply unicast responses.
2. **Verify Connectivity**: Use ICMP Echo Requests/Replies (`ping`) to generate traffic and update neighbor tables.
3. **Manage Switch MAC Address Tables**: Inspect Layer 2 mappings using `show mac address-table`.
4. **Filter Table Output**: Constrain command outputs by interface and dynamic learning state.
5. **Clear Dynamic Entries**: Reset learned MAC mappings using `clear mac address-table dynamic`.
6. **Understand Re-Learning Mechanics**: Observe how switches update their tables based on frame source MAC headers.

---

## 🌐 Topology Overview

```text
       +-------------------------------------------------------+
       |                     Switch SW1                        |
       |                   (Cisco Catalyst)                    |
       +-------+-------------------+-------------------+-------+
               | G0/1              | G0/2              | G0/3
               |                   |                   |
               |                   |                   |
        +------+------+     +------+------+     +------+------+
        |     PC1     |     |     PC2     |     |     PC3     |
        | 192.168.1.1 |     | 192.168.1.2 |     | 192.168.1.3 |
        +-------------+     +-------------+     +-------------+

🛠️ Step-by-Step Lab Walkthrough
Step 1: ARP Resolution & Broadcast/Unicast Frame Flow
When PC1 (192.168.1.1) attempts to communicate with PC2 (192.168.1.2) for the first time:

ARP Cache Check: PC1 checks its local ARP cache (arp -a). If no mapping for 192.168.1.2 exists, encapsulation pauses.

ARP Request (Broadcast): PC1 sends an ARP Request asking "Who has 192.168.1.2? Tell 192.168.1.1".

Source MAC: PC1_MAC

Destination MAC: FFFF.FFFF.FFFF (Layer 2 Broadcast)

Switch Flooding: SW1 receives the frame on interface GigabitEthernet0/1.

Learning: SW1 records PC1_MAC -> GigabitEthernet0/1 in its MAC Address Table.

Flooding: Since the destination is broadcast, SW1 floods the frame out all ports except G0/1 (reaching PC2 and PC3).

ARP Reply (Unicast): PC3 drops the packet. PC2 processes it and sends an ARP Reply containing its MAC address (PC2_MAC).

Source MAC: PC2_MAC

Destination MAC: PC1_MAC (Unicast)

Switch Forwarding: SW1 learns PC2_MAC on GigabitEthernet0/2 and forwards the reply directly out G0/1.

Step 2: ICMP Ping Verification
Once the ARP entry is resolved, PC1 can successfully encapsulate and send ICMP Echo Request packets to PC2.

On PC1, execute a ping command to PC2:
C:\> ping 192.168.1.2
Verify that the first ICMP packet is not dropped (or only the initial packet drops if ARP resolution timed out during simulation mode).

Display the updated local ARP table on PC1:
C:\> arp -a
Internet Address      Physical Address      Type
192.168.1.2           5060.0a11.2233        dynamic
Step 3: Inspecting the Switch MAC Address Table
To see how SW1 maps connected device MAC addresses to physical switch interfaces, access the switch CLI in Privileged EXEC mode (#).
SW1# show mac address-table
Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    5060.0a11.1111    DYNAMIC     Gi0/1
   1    5060.0a11.2233    DYNAMIC     Gi0/2
   1    5060.0a11.3344    DYNAMIC     Gi0/3
Total Mac Addresses for this criterion: 3
Step 4: Filtering MAC Address Table Entries
In larger production environments, show mac address-table can output thousands of entries. Filtering by specific interfaces or learning types is essential for troubleshooting.

Filter by Specific Interface:
To view only the MAC address learned on port GigabitEthernet0/1:
SW1# show mac address-table interface gigabitethernet 0/1
Step 5: Clearing Dynamic MAC Address Table Entries
Cisco switches automatically age out dynamic MAC address entries after 300 seconds (5 minutes) of inactivity. However, network engineers can manually clear entries to test dynamic learning or flush stale mappings.

Clear all dynamically learned MAC addresses from SW1:
SW1# clear mac address-table dynamic
