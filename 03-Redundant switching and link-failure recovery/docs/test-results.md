# Network Test Results

## 1. Test Environment

- Simulator: Cisco Packet Tracer
- Architecture: Two distribution switches and two access switches
- VLANs: 10 (Sales), 20 (Finance)
- Spanning Tree: Per-VLAN root bridge configuration
- Link Aggregation: LACP EtherChannel

## 2. Configuration Verification

| ID | Test | Verification Command | Expected Result | Status |
|---|---|---|---|---|
| T01 | VLAN creation | show vlan brief | VLANs 10 and 20 exist | NOT TESTED |
| T02 | Access-port assignment | show vlan brief | Correct departmental VLAN membership | NOT TESTED |
| T03 | Trunk configuration | show interfaces trunk | Required VLANs allowed on trunks | NOT TESTED |
| T04 | STP root VLAN 10 | show spanning-tree vlan 10 | Switch A is root | NOT TESTED |
| T05 | STP root VLAN 20 | show spanning-tree vlan 20 | Switch B is root | NOT TESTED |
| T06 | EtherChannel A-C | show etherchannel summary | Both links bundled | NOT TESTED |
| T07 | EtherChannel A-D | show etherchannel summary | Both links bundled | NOT TESTED |
| T08 | LACP neighbors | show lacp neighbor | Expected LACP neighbors detected | NOT TESTED |

## 3. Connectivity Testing

| ID | Test | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| T09 | Same-VLAN connectivity across access switches | Successful communication | Pending | NOT TESTED |
| T10 | VLAN 10 endpoint connectivity | Successful communication between Sales PCs | Pending | NOT TESTED |
| T11 | VLAN 20 endpoint connectivity | Successful communication between Finance PCs | Pending | NOT TESTED |
| T12 | Cross-VLAN connectivity | No communication without Layer 3 routing | Pending | NOT TESTED |

## 4. Failure and Recovery Testing

| ID | Failure Scenario | Expected Behavior | Actual Result | Status |
|---|---|---|---|---|
| T13 | Disconnect one EtherChannel member | Remaining member maintains the logical link | Pending | NOT TESTED |
| T14 | Disconnect an entire EtherChannel | STP may transition an alternative path to forwarding | Pending | NOT TESTED |
| T15 | Shut down Switch A | Remaining topology may provide alternative connectivity after reconvergence | Pending | NOT TESTED |
| T16 | Shut down Switch B | Remaining topology may provide alternative connectivity after reconvergence | Pending | NOT TESTED |

## 5. Troubleshooting Records

### Native VLAN Mismatch

**Observed message:**

```text
%CDP-4-NATIVE_VLAN_MISMATCH
```

**Cause:** Different native VLAN IDs were configured at opposite ends of a trunk.

**Resolution:** Align the native VLAN configuration on both endpoints.

**Retest:** Record the resulting trunk configuration and whether the mismatch warning disappears.

### STP VLAN Availability

**Observed message:**

```text
No spanning tree instance exists.
```

**Investigation:** Inspect VLAN existence, active status, and trunk allowed VLAN configuration.

**Resolution:** Record the actual corrective configuration.

**Retest:** Verify the relevant STP instance with `show spanning-tree vlan 10` or `show spanning-tree vlan 20`.

## 6. Evidence

Screenshots documenting the tests are stored in the evidence directory.

- VLAN membership: evidence/vlan-brief.png
- Trunk operation: evidence/trunk-status.png
- STP VLAN 10: evidence/spanning-tree-vlan10.png
- STP VLAN 20: evidence/spanning-tree-vlan20.png
- EtherChannel: evidence/etherchannel-summary.png
- LACP neighbors: evidence/lacp-neighbors.png

## 7. Summary

- Configuration tests performed: [Fill in]
- Connectivity tests performed: [Fill in]
- Failure tests performed: [Fill in]
- Tests passed: [Fill in]
- Tests failed: [Fill in]
- Tests not performed: [Fill in]

Only verified results are marked as PASS.
