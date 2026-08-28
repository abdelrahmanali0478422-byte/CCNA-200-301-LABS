# CCNA 200-301 | Day 04 Lab: Basic Device Configuration & Password Security

This repository contains my completed hands-on lab for **Day 04** of [Jeremy's IT Lab CCNA 200-301 Course](https://www.youtube.com/@JeremysITLab). 

In this lab, I practiced basic Cisco IOS device management, host naming conventions, privileged access passwords, password encryption, and saving running configurations into NVRAM.

---

## 📌 Lab Objectives
1. Configure hostnames for network devices (`R1` and `SW1`).
2. Secure **Privileged EXEC Mode** using both encrypted (`enable secret`) and plain-text (`enable password`) methods.
3. Enable global weak password encryption using `service password-encryption`.
4. Verify device running configurations (`show running-config`).
5. Save active configurations from RAM to NVRAM (`copy running-config startup-config`).

---

## 🛠️ Configurations & CLI Commands Executed

### 1. Router Configuration (`R1`)
* **Hostname Set:** `R1`
* **Privileged Password Setup:**
  ```ciscolike
