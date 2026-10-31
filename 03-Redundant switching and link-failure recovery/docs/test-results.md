# Network Test Results

## 1. Test Environment

- Simulator: Cisco Packet Tracer
- Architecture: Two distribution switches and two access switches
- VLANs: 10 (Sales), 20 (Finance)
- Spanning Tree: Per-VLAN root bridge configuration
- Link Aggregation: LACP EtherChannel

## 2. Configuration Verification

| ID | Test | Verification Command | Result | Status |
|---|---|---|---|---|
| T01 | VLAN creation | show vlan brief | [See result](../tests/show-vlan-brief.png) | TESTED |
| T02 | Access-port assignment | show vlan brief | [See result](../tests/show-vlan-brief.png) | TESTED |
| T03 | Trunk configuration | show interfaces trunk | [See result](../tests/show-interfaces-trunk.png) | TESTED |
| T04 | STP root VLAN 10 | show spanning-tree vlan 10 | [See result](../tests/show-spanning-tree-vlan-10.png) | TESTED |
| T05 | STP root VLAN 20 | show spanning-tree vlan 20 | [See result](../tests/show-spanning-tree-vlan-20.png) | TESTED |
| T06 | EtherChannel A-C | show etherchannel summary | [See result A](../tests/show-etherchannel-summary-A.png) , [See result C](../tests/show-etherchannel-summary-C.png) | TESTED |
| T07 | EtherChannel A-D | show etherchannel summary | [See result A](../tests/show-etherchannel-summary-A.png) , [See result D](../tests/show-etherchannel-summary-D.png) | NOT TESTED |


## 3. Connectivity Testing

| ID | Test | Expected Result | Result | Status |
|---|---|---|---|---|
| T09 | Same-VLAN connectivity across access switches | Successful communication | [See result A](../tests/same-vlan-ping.png) | TESTED |
| T10 | VLAN 10 endpoint connectivity | Successful communication between Sales PCs | [See result A](../tests/vlan-10-endpoint-connectivity.png) | TESTED |
| T11 | VLAN 20 endpoint connectivity | Successful communication between Finance PCs | [See result A](../tests/vlan-20-endpoint-connectivity.png) | TESTED |
| T12 | Cross-VLAN connectivity | No communication without Layer 3 routing | [See result A](../tests/inter-vlan-connectivity.png) | TESTED |

## 4. Failure and Recovery Testing

| ID | Failure Scenario | Expected Behavior | Result | Status |
|---|---|---|---|---|
| T13 | Disconnect one EtherChannel member | Remaining member maintains the logical link | [See result A](../tests/single-etherchannel-ping.png) | TESTED |
| T14 | Disconnect an entire EtherChannel | STP may transition an alternative path to forwarding | [See result A](../tests/double-etherchannel-ping.png) | TESTED |

## 5. Troubleshooting Records

### Native VLAN Mismatch

**Observed message:**

```text
%CDP-4-NATIVE_VLAN_MISMATCH
```

**Cause:** Different native VLAN IDs were configured at opposite ends of a trunk.

**Resolution:** Aligning the native VLAN configuration on both endpoints.



## 6. Summary

- Tests performed: [13]
- Tests passed: [13]
- Tests failed: [0]



