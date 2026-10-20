# Network Test Results

## 1. Test Environment

- Simulator: Cisco Packet Tracer
- Network: Small office, 12 workstations across three departments
- Addressing: 192.168.1.0/24 subdivided into /26 networks

## 2. Test Table

| ID | Test | Source | Target | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| T01 | DHCP assignment | Administration PC | DHCP server/router | Valid address, mask, gateway | [Recorded Output](../tests/dhcp-assignment.png) | TESTED |
| T02 | Default gateway reachability | Administration PC | Sales gateway | Successful ping | [Recorded Output](../tests/gateway-connectivity.png) | TESTED |
| T03 | Same-subnet connectivity | Administration PC | Another Administration PC | Successful ping | [Recorded Output](../tests/same-subnet-connectivity.png) | TESTED |
| T04 | Inter-subnet routing | Administration PC | Finance PC | Successful ping | [Recorded Output](../tests/inter-subnet-connectivity.png) | TESTED |


## 3. Commands used

### DHCP

Command: `ipconfig /all`

Output of intrest: DHCP Servers....................: 192.168.1.129

### Gateway and Routing

Command: `ping 192.168.1.129`

Output : Ping statistics for 192.168.1.129:  Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)

### Routing Table

Command: `show ip route`

Output : 
|  | 192.168.1.0/26 is subnetted | 3 subnets |
|---|---|---|
| C | 192.168.1.0 is directly connected | GigabitEthernet1/0 |
| C | 192.168.1.64 is directly connected | GigabitEthernet2/0 |
| C | 192.168.1.128 is directly connected | GigabitEthernet3/0 |

## 4. Issues Encountered

No Issues were encountered during this lab.

## 5. Summary

Tests performed: [4]
Passed: [4]
Failed: [0]
Not tested: [0]
