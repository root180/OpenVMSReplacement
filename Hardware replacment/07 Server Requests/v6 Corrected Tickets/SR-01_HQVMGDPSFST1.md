# SR-01 - HQVMGDPSFST1

## GPO IT Service Hub - New Server Request

| Field | Value |
|---|---|
| Requested physical server name | HQVMGDPSFST1 |
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| Environment | Test |
| Data center | HQ |
| OS | Windows Server 2025 |
| Memory | 128 GB minimum |
| Network | Server Distribution |
| Description | HQVMGDPSFST1 - GDPS TEST physical file/service cluster node 1. |
| Replacement | N/A - new GDPS TEST environment; production mirror. |
| RDP access | Matthew Taylor |
| Watchlist | Muyiwa Aniyikaye |
| Patching group | SCCM_Server_Patching_General_D - Server Reboots 4th Friday 11 am-2pm |

## Data drive requirements

No additional local authoritative data drive. Use standard Windows Server OS drive (100 GB minimum). GDPS business files reside on TEST >=14.4 TB usable HPE Enterprise Storage for Windows Server / WSFC. LUN00-LUN09 must be presented at or above their controlled minimum capacities.

## Purpose

GDPS TEST physical file/service cluster node. TEST mirrors PROD so production-equivalent clustering, storage, failover, and recovery can be validated before release.

## Special requirements

Provision as one member of the matched two-node GDPS TEST WSFC cluster. Redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent fabrics, independent File Share Witness, and no authoritative GDPS business files on local disk. Capacity may be larger but must not be smaller than the controlled minimum.

Coordinate patching/reboots with HQVMGDPSFST2 so both TEST nodes are never rebooted simultaneously. If the selected SCCM group cannot guarantee sequential/cluster-aware patching, assign an approved complementary schedule before implementation.

Final IP/DNS/VLAN/security-boundary values are assigned by GPO Network/Security.

## Controlled references

- GDPS Hardware Master v4.3
- GDPS Hardware Acquisition SOW - CDW-G v1.9
- GDPS Storage Architecture and LUN Design v1.1
- GDPS Windows File Cluster and SMB Namespace Standard v1.8
