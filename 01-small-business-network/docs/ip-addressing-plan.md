## IP Addressing Plan

## 1. Address Allocation

The allocated address block is 192.168.1.0/24. It is divided into three /26 subnets, one for each department.

| Department     |    Network       |   Subnet Mask   | Usable Host Range           | Broadcast     | Default Gateway |
|---------------------------------------------------------------------------------------------------------------------|
| Sales          | 192.168.1.0/26   | 255.255.255.192 | 192.168.1.1–192.168.1.62    | 192.168.1.63  | 192.168.1.1     |
| Finance        | 192.168.1.64/26  | 255.255.255.192 | 192.168.1.65–192.168.1.126  | 192.168.1.127 | 192.168.1.65    |
| Administration | 192.168.1.128/26 | 255.255.255.192 | 192.168.1.129–192.168.1.190 | 192.168.1.191 | 192.168.1.129   |

## 2. DHCP Allocation

DHCP dynamically assigns IPv4 addresses to departmental workstations. Reserve gateway addresses have been excluded from the pools

| Department     | DHCP Pool                     |
|------------------------------------------------|
| Sales          | 192.168.1.2 – 192.168.1.62    |
| Finance        | 192.168.1.66 – 192.168.1.126  |
| Administration | 192.168.1.130 – 192.168.1.190 |


## 3. Notes

- Each department has a separate /26 subnet with 62 usable IPv4 addresses.
- The three allocated subnets do not overlap with each other.
- The 192.168.1.192/26 subnet remains available for a future expansion.
- Separate subnets provide logical segmentation but do not enforce access restrictions by themselves.
