# SR-02 - HQVMGDPSFST2

## GPO IT Service Hub - New Server Request

| Field | Value |
|---|---|
| Requested physical server name | HQVMGDPSFST2 |
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| Environment | Test |
| Data center | HQ |
| OS | Windows Server 2025 |
| Memory | 128 GB minimum |
| Network | Server Distribution |
| Description | HQVMGDPSFST2 - GDPS TEST physical file/service cluster node 2. |
| Replacement | N/A - new GDPS TEST environment; production mirror. |
| RDP access | Matthew Taylor |
| Watchlist | Muyiwa Aniyikaye |
| Patching group | SCCM_Server_Patching_General_D - Server Reboots 4th Friday 11 am-2pm |

## Data drive requirements

No additional local authoritative data drive. Use standard Windows Server OS drive (100 GB minimum). GDPS business files reside on TEST >=14.4 TB usable HPE Enterprise Storage for Windows Server / WSFC. LUN00-LUN09 must be presented at or above their controlled minimum capacities.

## Purpose

GDPS TEST physical file/service cluster node. TEST mirrors PROD so production-equivalent clustering, storage, failover, and recovery can be validated before release.

## Special requirements

Provision as the peer of HQVMGDPSFST1 in the two-node HQ GDPS TEST WSFC cluster. Redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent fabrics, independent File Share Witness, and no authoritative GDPS business files on local disk.

Coordinate patching/reboots so both TEST nodes are never rebooted simultaneously. Final IP/DNS/VLAN/security-boundary values are assigned by GPO Network/Security.

## Controlled references

- GDPS Hardware Master v4.3
- GDPS Hardware Acquisition SOW - CDW-G v1.9
- GDPS Storage Architecture and LUN Design v1.1
- GDPS Windows File Cluster and SMB Namespace Standard v1.8
