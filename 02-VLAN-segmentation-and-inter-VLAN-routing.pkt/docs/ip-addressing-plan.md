# VLAN and IP Addressing Plan

## 1. VLAN Allocation

| VLAN ID | Name | Purpose |
|---|---|---|
| 10 | ADMINISTRATION | Administration workstations |
| 20 | FINANCE | Finance workstations |
| 30 | SALES | Sales workstations |
| 99 | NATIVE | Native VLAN and static-IP trunking tests |

VLANs 10, 20, and 30 are assigned separate IPv4 networks. VLAN 99 is used to test native VLAN forwarding between switches.

## 2. IPv4 Address Allocation

The following table illustrates the addressing scheme.

| VLAN | Network | Subnet Mask | Default Gateway | Address Assignment |
|---|---|---|---|---|
| 10 | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1 | DHCP |
| 20 | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1 | DHCP |
| 30 | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1 | DHCP |
| 99 | 192.168.99.0/24 | 255.255.255.0 | Not required for Layer 2 testing | Static IP |

## 3. Router Subinterfaces

The router uses its physical GigabitEthernet0/0 interface to carry traffic for the departmental VLANs.

| Router Subinterface | VLAN ID | IPv4 Address |
|---|---|---|
| G0/0.10 | 10 | 192.168.10.1/24 |
| G0/0.20 | 20 | 192.168.20.1/24 |
| G0/0.30 | 30 | 192.168.30.1/24 |

Each departmental subinterface uses 802.1Q encapsulation with the corresponding VLAN ID. The router acts as the default gateway for each departmental network and provides DHCP service as configured.

## 4. VLAN 99 Static Addressing

VLAN 99 is used for native VLAN forwarding tests between the two switches.

Example static configuration:

| Device | IPv4 Address | Subnet Mask |
|---|---|---|
| Native VLAN test PC on SW1 | 192.168.99.1 | 255.255.255.0 |
| Native VLAN test PC on SW2 | 192.168.99.2 | 255.255.255.0 |

Both test PCs belong to the same IP network. A default gateway is unnecessary for testing communication between these PCs on the same subnet.


## 5. Trunk Configuration Notes

- Configure the inter-switch link as an 802.1Q trunk.
- Ensure VLANs 10, 30, and 99 are allowed on the inter-switch trunk.
- Configure VLAN 99 as the native VLAN on that trunk.
- Configure the switch-to-router link to carry VLANs 10, 20, and 30.
- If VLAN 99 is also configured as the native VLAN on the router-facing trunk, configure the router side consistently with `encapsulation dot1Q 99 native`.

VLAN 99 does not need an IP gateway or DHCP pool for the Layer 2 connectivity test. If the router-facing trunk uses VLAN 99 as its native VLAN, a matching router subinterface can be configured without an IP address when no Layer 3 service is required for that VLAN.
