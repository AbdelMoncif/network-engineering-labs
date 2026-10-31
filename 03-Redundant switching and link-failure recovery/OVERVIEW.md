## Overview

Designed and simulated a redundant enterprise-style Layer 2 switching infrastructure in Cisco Packet Tracer using four interconnected switches.

The network follows a distribution/access architecture with two distribution switches and two access switches. It implements departmental VLAN segmentation, IEEE 802.1Q trunking, Spanning Tree Protocol (STP), and LACP-based EtherChannel aggregation.

Per-VLAN STP root bridge priorities are configured to distribute traffic across both distribution switches, while redundant physical connections provide alternative paths in the event of link failures.

## Objectives

- Design a redundant four-switch network using a distribution/access architecture.
- Implement departmental VLAN segmentation.
- Configure 802.1Q trunk links to transport multiple VLANs.
- Configure STP root bridge priorities independently for each VLAN.
- Distribute root bridge responsibilities between two distribution switches.
- Implement LACP EtherChannel bundles between distribution and access switches.
- Investigate native VLAN mismatches and STP-related configuration issues.
- Verify VLAN membership, trunk operation, STP port roles, and EtherChannel status.
- Explore network resilience through link and switch failure testing.

## Technologies

- Cisco Packet Tracer
- Cisco IOS CLI
- Layer 2 switching
- VLANs
- IEEE 802.1Q trunking
- Spanning Tree Protocol (STP)
- Per-VLAN STP root bridge configuration
- LACP (IEEE 802.1AX)
- EtherChannel
- Network redundancy and high availability

## Network Architecture

The topology consists of four switches:

- **Switch A:** Distribution switch; primary STP root for VLAN 10 and secondary root for VLAN 20.
- **Switch B:** Distribution switch; primary STP root for VLAN 20 and secondary root for VLAN 10.
- **Switch C:** Access switch serving the left-side endpoints.
- **Switch D:** Access switch serving the right-side endpoints.

The distribution switches connect to both access switches through redundant paths. Two-link LACP EtherChannels connect Switch A to Switch C and Switch A to Switch D, while individual inter-switch links connect Switch C to Switch B and Switch B to Switch D.

## Network Topology

![Enterprise Layer 2 topology](evidence/topology.png)

## VLAN and IP Addressing

The network uses two departmental VLANs:

| VLAN | Department | Network |
|---|---|---|
| 10 | Sales | 192.168.10.0/24 |
| 20 | Finance | 192.168.20.0/24 |

Endpoint distribution and addressing details are documented in [VLAN and IP Addressing Plan](docs/vlan-and-ip-addressing-plan.md).

## Spanning Tree Protocol

STP is configured to distribute root bridge responsibilities between the two distribution switches.

- Switch A is the primary root for VLAN 10.
- Switch B is the primary root for VLAN 20.

This per-VLAN configuration provides different preferred Layer 2 paths for departmental traffic.

## EtherChannel and Link Aggregation

LACP is used to aggregate two physical FastEthernet links into logical EtherChannel interfaces.

The bundles connect:
- Switch A to Switch C.
- Switch A to Switch D.

This provides additional aggregate link capacity and resilience against individual member-link failures.

## Configuration and Implementation

Detailed configuration and design decisions are documented in [STP and EtherChannel Configuration](docs/stp-and-etherchannel.md).

The Packet Tracer simulation is provided in `enterprise-layer2-redundancy.pkt`.

## Validation and Testing

See [Test Results](docs/test-results.md) for verification of VLANs, trunk links, STP root bridge selection, EtherChannel operation, and network failure recovery.

Tests are distinguished between completed, failed, and not yet performed.

## Current Limitations and Future Improvements

The current implementation focuses on Layer 2 switching and redundancy. Inter-VLAN routing and redundant default gateway services have not yet been implemented.

Potential improvements include:

- Layer 3 switching and inter-VLAN routing.
- HSRP gateway redundancy.
- EtherChannel member failure testing.
- Distribution switch failure and recovery testing.
- STP convergence and traffic-path analysis.

## Lessons Learned

- Per-VLAN STP root bridge placement can influence traffic paths and distribute forwarding responsibilities between distribution switches.
- EtherChannel combines multiple physical links into one logical connection, changing how STP evaluates redundant paths.
- Native VLAN mismatches can cause inconsistent trunk behavior and should be investigated at both ends of a trunk.
- STP requires the relevant VLANs to exist and be active across participating switches.
- Redundant physical links do not automatically guarantee end-to-end availability; STP states and failure recovery must be verified.
