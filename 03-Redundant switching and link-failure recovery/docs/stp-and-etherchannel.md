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
switchport trunk allowed vlan 10,20
```

Where required, trunk configuration is applied to the logical Port-Channel interface rather than independently configuring incompatible settings on its member interfaces.

## 4. Native VLAN Troubleshooting

During configuration, a native VLAN mismatch warning was observed:

```text
%CDP-4-NATIVE_VLAN_MISMATCH
```

The warning indicated that the two ends of a trunk were configured with different native VLANs: VLAN 99 on one side and VLAN 1 on the other.

### Diagnosis

The trunk configuration was inspected using:

```cisco
show interfaces trunk
```

### Resolution

The native VLAN must be configured consistently on both ends of each relevant trunk.

Example:

```cisco
switchport trunk native vlan 99
```

For EtherChannel links, the trunk configuration should be consistent across the logical channel and both endpoints.

## 5. STP VLAN Availability Troubleshooting

The following message was encountered:

```text
No spanning tree instance exists.
```

This prompted an investigation of VLAN availability and STP operation.

Relevant checks include:

```cisco
show vlan brief
show interfaces trunk
show spanning-tree vlan 10
show spanning-tree vlan 20
```

VLANs must be created and active on the relevant switches, and the trunk links must allow the VLANs to traverse the network.

## 6. Failure Recovery and Future Testing

Planned failure tests include:

- Disconnecting one physical EtherChannel member to verify that the logical channel remains operational.
- Disconnecting a complete EtherChannel to observe the alternative STP forwarding path.
- Shutting down a distribution switch to observe STP reconvergence and connectivity recovery.

Actual recovery behavior and convergence observations will be documented in the test results.
