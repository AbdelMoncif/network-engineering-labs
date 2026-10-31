
# VLAN and IP Addressing Plan

## 1. VLAN Allocation

| VLAN ID | Department | Network | Subnet Mask |
|---|---|---|---|
| 10 | Sales | 192.168.10.0/24 | 255.255.255.0 |
| 20 | Finance | 192.168.20.0/24 | 255.255.255.0 |

Both VLANs are extended across the access switching infrastructure through trunk links.

## 2. Endpoint Distribution

| Switch | VLAN 10 (Sales) | VLAN 20 (Finance) |
|---|---:|---:|
| Switch C | 6 PCs | 2 PCs |
| Switch D | 2 PCs | 3 PCs |
| **Total** | **8 PCs** | **5 PCs** |

## 3. Network Segmentation

Each department operates in a separate Layer 2 broadcast domain and uses its own IPv4 subnet.

VLAN 10 and VLAN 20 traffic can traverse the interconnected switches through appropriately configured trunk links.

Communication between the two IP networks requires Layer 3 routing, which is outside the scope of the current Layer 2 implementation.

## 4. Address Assignment

The addressing was done statically as the DHCP implementation that is failure proof  would require HSRP configutation which is outside the scope of this lab.

## 5. Trunk VLAN Requirements

The inter-switch connections must transport VLANs 10 and 20.

The allowed VLAN configuration should be consistent across the relevant trunk and EtherChannel links.

A native VLAN of 99 was introduced during configuration and is documented separately in the STP and EtherChannel troubleshooting section.
