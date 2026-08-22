# Enterprise Campus Network Simulation

## 📌 Project Overview
This project simulates a scalable, multi-tier campus network architecture using Cisco Packet Tracer. The objective was to design a network with strict logical segmentation, centralized routing, and integrated network services (DHCP, DNS, HTTP) across both wired and wireless infrastructure.

## 🏗️ Topology & Architecture
![Network Topology](docs/campus_network2.png) 


The network is built around a central routing hub (R1) connecting three primary zones:
1.  **Staff Operations:** (`192.168.0.0/24`)
2.  **Data Center / Server Farm:** (`203.172.16.0/24`) Hosting internal academic and sports web portals.
3.  **Student Campus / Classrooms:** Segmented into multiple VLANs using an 802.1Q trunk.

## ⚙️ Technologies & Protocols Implemented
* **VLAN Configuration & 802.1Q Trunking:** Isolated broadcast domains for Classrooms 1, 2, and 3 to improve security and network performance.
* **Router-on-a-Stick (Inter-VLAN Routing):** Configured sub-interfaces on the central Cisco router to route traffic between the disparate campus VLANs.
* **DHCP with IP Helper:** Centralized DHCP server in a management VLAN, utilizing `ip helper-address` on the router to forward broadcast requests across subnet boundaries.
* **DNS & HTTP Services:** Integrated internal domain resolution for user-friendly access to the server farm (`fcicollege.edu`).
* **Wireless Edge:** Deployed Access Points to support mobile devices and laptops within the classroom VLANs.

## 📊 IP Addressing Scheme
| Network / VLAN | VLAN ID | Subnet | Default Gateway | Purpose |
| :--- | :---: | :--- | :--- | :--- |
| Staff | - | `192.168.0.0/24` | `192.168.0.1` | Administration |
| Data Center | - | `203.172.16.0/24` | `203.172.16.1` | Web Hosting |
| Classroom 1 | 10 | `172.16.10.0/24` | `172.16.10.1` | Student Access |
| Classroom 2 | 20 | `172.16.20.0/24` | `172.16.20.1` | Student Access |
| Classroom 3 | 30 | `172.16.30.0/24` | `172.16.30.1` | Student Access |
| Management/DHCP| 99 | `172.16.99.0/24` | `172.16.99.1` | Infrastructure |

## 🚀 How to Run the Simulation
1. Clone this repository to your local machine.
2. Open `SimpleCollegeNetwork.pkt` using Cisco Packet Tracer (Version 9.0.0 or higher).
3. **Test DHCP:** Open any laptop in Classroom 1, toggle the IP configuration to Static, then back to DHCP. It will pull a `172.16.10.x` address.
4. **Test Routing & DNS:** Open the web browser on the Staff PC (`192.168.0.10`) and navigate to `academics.fcicollege.edu`.

## 🔮 Future Improvements
* Implement **HSRP** for default gateway redundancy.
* Introduce **Access Control Lists (ACLs)** to restrict student VLANs from accessing the Staff management network.
* Add redundant distribution switches and configure **Spanning Tree Protocol (STP)** to eliminate single points of failure.
