# Day 03 Lab: TCP/IP Model & Data Encapsulation

## 📌 Lab Overview
This lab focuses on the fundamental concepts of data transmission across networks. It includes a hands-on Packet Tracer simulation to trace packet movement, observe network interfaces, and understand the core mechanisms of the **TCP/IP model** and **Data Encapsulation**.

---

## 🧠 Theoretical Concepts

### 1. Protocols & Standards
* **Protocol:** A set of rules that govern how data is transmitted and understood between devices on a network.
* **Standard:** Established guidelines that ensure interoperability, allowing devices from different vendors (e.g., Cisco, Huawei, HP) to communicate seamlessly.

### 2. Network Governing Organizations
* **IEEE (Institute of Electrical and Electronics Engineers):** Responsible for developing and standardizing protocols such as **Ethernet (IEEE 802.3)** and **Wi-Fi (IEEE 802.11)**.
* **IETF (Internet Engineering Task Force):** Responsible for developing and documenting core internet protocols (e.g., `TCP`, `UDP`, `IP`, `HTTPS`, `DNS`). These standards are published as **RFCs (Request for Comments)**.

### 3. TCP/IP Model Layers & Payload Concept
* **The Hop:** A hop represents one segment of a data packet's journey between routers or network devices from its source to its destination.
* **Payload:** The actual data or content carried by a protocol from the layer immediately above it.
  * *Example:* The payload of a Transport Layer **Segment** is the actual **Data** originating from the Application Layer.

### 4. Encapsulation & Decapsulation
* **Encapsulation:** The process of adding specific headers (and sometimes trailers) to data as it moves down the TCP/IP layers from the source application to the physical network.
* **Decapsulation:** The reverse process of stripping away these headers as the data moves up the layers at the destination device.

---

