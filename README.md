# 🚀 ARES-1 Mars Colony Cyber Defense Network

**Cisco Packet Tracer Cybersecurity Project**

ARES-1 is a simulated Mars colony network designed to demonstrate how network segmentation and layered security controls can protect critical infrastructure from both internal and physical-access attacks.

The environment separates Earth Mission Control, Mars operational networks, autonomous rover systems, research systems, security systems, telemetry services, and critical life-support infrastructure.

The project demonstrates both **authorized and unauthorized traffic scenarios**, including a compromised Mars rover attempting to reach an oxygen-control system and a rogue device attempting to gain access through a secured switch port.


## 🛰️ Network Architecture

The ARES-1 environment is divided into multiple security zones using VLANs and separate IP subnets.

| VLAN    | Network         | Purpose                    |
| ------- | --------------- | -------------------------- |
| VLAN 10 | `10.10.10.0/24` | Control Room               |
| VLAN 20 | `10.10.20.0/24` | Research Lab               |
| VLAN 30 | `10.10.30.0/24` | Autonomous Rovers          |
| VLAN 40 | `10.10.40.0/24` | Security Systems           |
| VLAN 50 | `10.10.50.0/24` | Critical OT / Life Support |
| VLAN 60 | `10.10.60.0/24` | Telemetry Servers          |

Earth Mission Control uses:

`192.168.100.0/24`

The Earth-to-Mars communication link uses:

`172.16.0.0/30`

Inter-VLAN routing is implemented using **Router-on-a-Stick with IEEE 802.1Q trunking**.


## 🔐 Security Controls

The network uses multiple defensive layers rather than relying on a single security mechanism.

* **VLAN Segmentation** — Separates control, research, rover, security, server, and critical OT systems.
* **IT/OT Separation** — Life-support systems are isolated in the dedicated Critical OT network.
* **Extended ACLs** — Restrict unauthorized traffic between network zones.
* **Least-Privilege Access** — Only approved systems can communicate with critical infrastructure.
* **Port Security** — Prevents unauthorized devices from replacing legitimate endpoints.
* **Sticky MAC Learning** — Learns and secures authorized device MAC addresses.
* **Unused Port Shutdown** — Unused switch ports are administratively disabled.
* **Black-Hole VLAN 999** — Unused ports are assigned to an isolated VLAN.
* **Static Routing** — Provides controlled connectivity between Earth Mission Control and the Mars network.


## ☠️ Simulated Attack Scenarios

### Attack 1 — Compromised Rover

A simulated compromised rover in **VLAN 30** attempted to communicate with the critical oxygen-control system in **VLAN 50**.

**Source:** `ROVER-01` — `10.10.30.10`
**Target:** `O2-CTRL01` — `10.10.50.10`

**Result:** 🚫 Blocked

The `PROTECT-CRITICAL-OT` extended ACL prevented unauthorized Rover traffic from reaching the Critical OT network.

---

### Attack 2 — Rogue Device

A rogue device was connected to the switch port normally used by the legitimate Research Lab computer.

**Target Port:** `ARES-CORE-SW1 Fa0/2`

The switch detected a different MAC address through **Sticky MAC Port Security** and placed the port into:

`Secure-shutdown`

**Result:** 🚫 Unauthorized device blocked



## ✅ Verification Results

The final network configuration was tested to confirm that legitimate communication remains available while unauthorized access is blocked.

| Test                                     | Expected Result | Final Result       |
| ---------------------------------------- | --------------- | ------------------ |
| Control Room → Oxygen Controller         | Allow           | ✅ Success          |
| Compromised Rover → Oxygen Controller    | Block           | 🚫 Blocked         |
| Earth Mission Control → Telemetry Server | Allow           | ✅ Success          |
| Earth Mission Control → Control Room     | Block           | 🚫 Blocked         |
| Legitimate Lab PC → Research Gateway     | Allow           | ✅ Success          |
| Rogue Device → Secured Lab Port          | Block           | 🚫 Secure-shutdown |

These tests confirm that the network security controls enforce the intended least-privilege access policies without disrupting authorized communication.


## 🧠 Skills Demonstrated

This project demonstrates practical experience with:

* Cisco Packet Tracer
* IPv4 Addressing and Subnetting
* VLAN Configuration
* Access and Trunk Ports
* IEEE 802.1Q
* Router-on-a-Stick
* Inter-VLAN Routing
* Static Routing
* Route Summarization
* Extended Access Control Lists
* Wildcard Masks
* ACL Direction and Rule Ordering
* Network Segmentation
* IT/OT Security
* Least-Privilege Network Design
* Switch Port Security
* Sticky MAC Learning
* Rogue Device Detection
* Unused Port Hardening
* Packet Tracer Simulation Mode
* ICMP and ARP Troubleshooting


## 📁 Project Files

* `ARES-1_Mars_Colony_Cyber_Defense_FINAL.pkt` — Final Cisco Packet Tracer project file
* `README.md` — Project documentation, architecture, security controls, attack scenarios, and verification results

To explore the network, download the `.pkt` file and open it using **Cisco Packet Tracer**.
