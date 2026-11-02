# SR-07 - IMVMGDPSFSC1

## GPO IT Service Hub - New Server Request

| Field | Value |
|---|---|
| Requested physical server name | IMVMGDPSFSC1 |
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| Environment | Disaster Recovery |
| Data center | IM (Iron Mountain) |
| OS | Windows Server 2025 |
| Memory | 128 GB minimum |
| Network | Server Distribution |
| Description | IMVMGDPSFSC1 - GDPS COOP / DCIAC recovery physical cluster node 1. |
| Replacement | Part of replacement of ALPHA13 DCIAC03 / Data Center in a Crate Cluster (N13A + N13B). |
| RDP access | Matthew Taylor |
| Watchlist | Muyiwa Aniyikaye |
| Patching group | SCCM_Server_Patching_General_D - Server Reboots 4th Friday 11 am-2pm |

## Data drive requirements

No additional local authoritative data drive. COOP business files reside on >=21.4 TB usable HPE Enterprise Recovery Storage for Windows Server / WSFC. LUN00-LUN09 must be at or above their controlled minimum capacities.

## Purpose

GDPS COOP / DCIAC physical recovery cluster node replacing the ALPHA13 DCIAC03 / Data Center in a Crate recovery capability.

## Special requirements

Provision as one member of the separate two-node GDPS COOP / DCIAC / CRATE WSFC cluster. COOP receives approved PROD recovery replication. Redundant power/network/FC, MPIO, independent File Share Witness, and no authoritative GDPS business files on local disk.

Coordinate patching/reboots with IMVMGDPSFSC2 so both COOP nodes are never rebooted simultaneously.

## Controlled references

- GDPS Hardware Master v4.3
- GDPS Hardware Acquisition SOW - CDW-G v1.9
- GDPS Storage Architecture and LUN Design v1.1
- GDPS Windows File Cluster and SMB Namespace Standard v1.8
