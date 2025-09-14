#  Small Enterprise Networking Project (Cisco Packet Tracer)

##  Overview
This project shows three interconnected LANs (Library, Admin, and Lab) using Cisco Packet Tracer.
Each LAN is connected via its own router, and the routers are linked together to form a WAN.

## Network Design
-LANs: Library, Admin, Lab
-Routers: Cisco 2911 (one per LAN)
-Switches: Cisco 2960-24TT (one per LAN)
-End Devices: 2 PCs per LAN
-WAN Links: Router-to-Router serial/DCE connections

## Technologies Implemented
-Basic LAN Switching
-Router-to-Router WAN links
-Static IPv4 Addressing for LANs & WAN links
-Routing (Static or Dynamic – RIP/OSPF can be used)
-Inter-LAN Communication

##  Requirements
-Cisco Packet Tracer (v8.x or later recommended)
-Knowledge of:
   -IP Addressing
   -Routing (Static / RIP / OSPF)
   -Switch and Router configuration basics

##  How to Run
1. Open the .pkt file in Cisco Packet Tracer.
2. Assign IP addresses to PCs and router interfaces.
3. Configure routing (static routes or RIP/OSPF) on all routers.
4. Test connectivity using ping between PCs across LANs.

##  Network diagram
![Network Topology](Screenshot%202025-09-14%20223307.png)

