Overview : 
Designed and simulated a small office network in Cisco Packet Tracer for a company of 12 employees split across 3 departements which are : Sales, Finance and Administration.
This project focuses on IP addressing, Subnetting, DHCP, DNS, routing, and verification of end-to-end connectivity.

Objectives :
- Design a network topology for the 3 deparments
- Find a solution to the restriction of having only one allocated address block (192.168.1.0 /24)
- Configure the IP addresses and default gateways
- Configure DHCP for automatic workstation addressing
- Establish routing between subnets
- Verify network connectivity
- Document test results

Network Design
The network is divided into separate IP subnets for Sales, Finance and Administration using /26 subnetting.
Using seperate subnets provides distinct Layer 3 networks for each departement and room for growth (extra hosts, and one extra department) within the address block requirement.
For the sake of this lab I did not prevent departments from communicating with each other, as that would require additional security configurations which I will display in other labs.

Addressing Plan : 
see docs/ip-addressing-plan.md
