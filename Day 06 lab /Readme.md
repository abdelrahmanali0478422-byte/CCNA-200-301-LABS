# CCNA Day 06 Lab: ARP & MAC Address Table Analysis (Jeremy's IT Lab)

Welcome to the documentation for **Day 06 Lab** of Jeremy's IT Lab CCNA course! 🚀  
In this lab, we dive deep into the fundamentals of Layer 2 and Layer 3 networking, focusing on how the **Address Resolution Protocol (ARP)** operates to resolve MAC addresses from known IP addresses, testing network connectivity using `ping`, and managing the **MAC Address Table** on Cisco switches using `show` and `clear` commands.

---

## 📌 Lab Objectives

1. **Address Resolution Protocol (ARP)**: Understand how a host dynamically discovers the MAC address of a destination IP address within the local network.
2. **ICMP Ping**: Verify Layer 3 end-to-end connectivity between local hosts.
3. **Switch MAC Address Table Management**:
   - Inspect dynamically learned MAC addresses on Cisco switches (`show mac address-table`).
   - Clear dynamic MAC address table entries (`clear mac address-table dynamic`).
   - Observe how switches re-learn MAC addresses as frame traffic flows through interfaces.

---

## 🛠️ Network Topology & Key Concepts

The topology consists of a local Ethernet LAN with multiple end-user PCs connected through a Cisco Catalyst Switch.

* **Layer 2 Data Link Header**: Requires Destination MAC Address & Source MAC Address.
* **Layer 3 Network Header**: Requires Destination IP Address & Source IP Address.

> **Key Rule**: Before a host can encapsulate an IP packet into an Ethernet frame, it **must** know the destination MAC address (or the gateway MAC address if reaching an outside network).

---

## 📝 Lab Walkthrough & Step-by-Step Analysis

### Step 1: Observing the ARP Process & Cache

When PC1 wants to send ICMP Echo Requests (`ping`) to PC2:
1. PC1 checks its local **ARP Cache/Table** (`arp -a` or `show arp`).
2. If no entry exists for PC2's IP address, PC1 holds the IP packet and generates an **ARP Request Broadcast**:
   - **Target IP**: `192.168.1.X` (PC2)
   - **Target MAC**: `FF:FF:FF:FF:FF:FF` (Layer 2 Broadcast)
3. The switch floods the ARP request out all ports except the receiving port.
4. PC2 responds with an **ARP Reply Unicast**:
   - Contains PC2's exact hardware MAC address.
5. PC1 stores PC2's MAC address in its ARP cache and proceeds to send the `ping`.

<!-- 📷 REPLACE THIS LINE BY DRAGGING SCREENSHOT 1 HERE -->

---

### Step 2: Verifying Connectivity with `ping`

After ARP resolution successfully populates the host's ARP table, ICMP echo requests can be transmitted end-to-end without dropped frames.

```bash
# Example Ping Command on Host
C:\> ping 192.168.1.20
