# STP and EtherChannel Configuration

## 1. Spanning Tree Protocol

### Root Bridge Distribution

The network uses per-VLAN STP root bridge placement to distribute forwarding responsibilities between the two distribution switches.

| Switch | VLAN 10 | VLAN 20 |
|---|---|---|
| Switch A | Primary root | Secondary root |
| Switch B | Secondary root | Primary root |

### Switch A

```cisco
spanning-tree vlan 10 root primary
spanning-tree vlan 20 root secondary
```

### Switch B

```cisco
spanning-tree vlan 20 root primary
spanning-tree vlan 10 root secondary
```

This configuration allows each vlan's traffic to take a separate route to destination.

VLAN 10 uses Switch A as its preferred root, while VLAN 20 uses Switch B.

The actual forwarding paths depend on STP port roles, path costs, and the operational topology.

### Verification

```cisco
show spanning-tree summary
show spanning-tree vlan 10
show spanning-tree vlan 20
```

These commands are used to inspect root bridge selection, port roles, port states, and STP operation.

## 2. EtherChannel Configuration

### Design

LACP is used to aggregate two physical FastEthernet links into one logical EtherChannel interface.

| Connection | Physical Links | Protocol |
|---|---|---|
| Switch A – Switch C | Fa0/3–Fa0/4 | LACP |
| Switch A – Switch D | Two physical links | LACP |

### Example Configuration

```cisco
interface range fa0/3-4
 channel-group 2 mode active
```

The logical interface is configured using:

```cisco
interface port-channel 2
```

The corresponding configuration must be applied consistently on both ends, with compatible speed, duplex, trunk mode, allowed VLANs, and native VLAN settings.

### Verification

```cisco
show etherchannel summary
```

The EtherChannel summary is used to verify that the logical channel is operational and that the physical member ports are bundled successfully.

## 3. Trunking

Inter-switch connections use IEEE 802.1Q trunking to transport VLAN 10 and VLAN 20.

Example configuration:

```cisco
switchport mode trunk
switchport trunk allowed vlan 10,20, 99
```

Where required, trunk configuration is applied to the logical Port-Channel interface rather than separately configuring the physical ports.

## 4. STP VLAN Availability Troubleshooting

The following message was encountered:

```text
No spanning tree instance exists.
```

Relevant checks:

```cisco
show vlan brief
show interfaces trunk
show spanning-tree vlan 10
show spanning-tree vlan 20
```

VLANs must be created and active on all the relevant switches.


Actual behavior will be documented in the test results.
