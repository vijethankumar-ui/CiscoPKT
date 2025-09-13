# Enterprise Network Design & Implementation Report

## 1. Project Overview  
This project involves the **design and implementation of an Enterprise Network** for a trading floor support centre employing **600 staff**.  
The company is relocating to a new building with **three floors** and requires a scalable, secure, and redundant network.  

The design follows a **Hierarchical Network Model** with redundancy at each layer, ensuring **high availability, scalability, and security**.

---

## 2. Requirements  

1. Use Cisco Packet Tracer for network simulation.  
2. Implement a **Hierarchical model** with redundancy (2 routers, 2 multilayer switches).  
3. Provide **redundant ISP connections** (2 ISPs).  
4. Enable **wireless access** in each department.  
5. Assign each department a **unique VLAN and subnet**.  
6. Subnet the base network `172.16.1.0/24` to allocate IPs per department.  
7. Connect the company to ISPs using public IPs:  
   - `195.136.17.0/30`  
   - `195.136.17.4/30`  
   - `195.136.17.8/30`  
   - `195.136.17.12/30`  
8. Configure basic device settings: hostnames, passwords, banner, disable DNS lookup.  
9. Enable **Inter-VLAN routing** on multilayer switches.  
10. Configure multilayer switches for **both routing and switching**.  
11. Assign IPs dynamically using **DHCP servers** (server room).  
12. Assign **static IPs** to server devices.  

---

## 3. Organizational Structure & User Distribution  

- **First Floor**  
  - Sales & Marketing (VLAN 10) → 120 users  
  - HR & Logistics (VLAN 20) → 120 users  

- **Second Floor**  
  - Finance & Accounts (VLAN 30) → 120 users  
  - Admin & PR (VLAN 40) → 120 users  

- **Third Floor**  
  - ICT Department (VLAN 50) → 120 users  
  - Server Room (VLAN 60) → 12 devices  

**Total Staff: 600 + Servers**  

---

## 4. Network Topology  

![Enterprise Network Topology](network-diagram.png)  

- **Core Layer**: Two routers connected to two ISPs (redundancy).  
- **Distribution Layer**: Two multilayer switches providing inter-VLAN routing.  
- **Access Layer**: Switches, PCs, wireless APs, and printers.  
- **Server Room**: DHCP, DNS, Email servers with static addressing.  

---

## 5. IP Addressing & VLAN Plan  

| Department / VLAN | Subnet | Gateway (SVI) | Users |
|-------------------|---------|----------------|-------|
| VLAN 10 - Sales & Marketing | 172.16.1.0/25   | 172.16.1.1   | 120 |
| VLAN 20 - HR & Logistics   | 172.16.1.128/25 | 172.16.1.129 | 120 |
| VLAN 30 - Finance          | 172.16.2.0/25   | 172.16.2.1   | 120 |
| VLAN 40 - Admin & PR       | 172.16.2.128/25 | 172.16.2.129 | 120 |
| VLAN 50 - ICT              | 172.16.3.0/25   | 172.16.3.1   | 120 |
| VLAN 60 - Server Room      | 172.16.3.128/28 | 172.16.3.129 | 12 |

**Public IPs (ISP Links):**  
- Router to ISP1: `195.136.17.0/30` and `195.136.17.4/30`  
- Router to ISP2: `195.136.17.8/30` and `195.136.17.12/30`  

---

## 6. Key Configurations  

### 6.1 Basic Device Setup  
```bash
hostname CORE-R1
no ip domain-lookup
enable secret cisco123
banner motd ^Authorized Access Only!^
line console 0
 password class123
 login
```
### 6.2VLAN & Inter-VLAN Routing (SVI)
```bash
vlan 10
 name SALES
interface vlan 10
 ip address 172.16.1.1 255.255.255.128
 no shutdown
```
### 6.3 DHCP Server (Server Room)
```bash
ip dhcp pool SALES
 network 172.16.1.0 255.255.255.128
 default-router 172.16.1.1
 dns-server 172.16.3.130
```
### 6.4 NAT Overload (PAT)
```bash
access-list 1 permit 172.16.0.0 0.0.255.255
ip nat inside source list 1 interface g0/0 overload
```
### 6.5 Port Security Example
```bash
interface fa0/1
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
```
### 6.6 SSH Configuration
```bash
ip domain-name company.local
crypto key generate rsa
username admin secret cisco123
line vty 0 4
 login local
 transport input ssh
```
7. Testing & Verification

PC-to-PC Ping across VLANs
DHCP assigns correct IPs dynamically
Static IPs assigned to servers
DNS Resolution tested successfully
SSH login tested from remote PC
NAT providing internet access
Redundancy tested by disabling one ISP link

8. Conclusion

The enterprise network design successfully:
Supports 600+ users across 3 floors and 6 departments
Provides high availability using redundant ISPs and multilayer switches
Ensures security with port security, SSH, and ACLs
Provides flexibility & scalability for future growth
This project demonstrates a realistic enterprise network model in Cisco Packet Tracer with advanced technologies such as VLANs, Inter-VLAN routing, DHCP, SSH, NAT, ACLs, and WLAN.




