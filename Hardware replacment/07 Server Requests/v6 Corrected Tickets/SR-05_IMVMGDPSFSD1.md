# SR-05 - IMVMGDPSFSD1

## GPO IT Service Hub - New Server Request

| Field | Value |
|---|---|
| Requested physical server name | IMVMGDPSFSD1 |
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| Environment | Disaster Recovery |
| Data center | IM (Iron Mountain) |
| OS | Windows Server 2025 |
| Memory | 128 GB minimum |
| Network | Server Distribution |
| Description | IMVMGDPSFSD1 - GDPS DR physical file/service cluster node 1. |
| Replacement | Part of replacement of ALPHA6 Production Backup / DR Cluster (N6A + N6B). |
| RDP access | Matthew Taylor |
| Watchlist | Muyiwa Aniyikaye |
| Patching group | SCCM_Server_Patching_General_D - Server Reboots 4th Friday 11 am-2pm |

## Data drive requirements

No additional local authoritative data drive. DR business files reside on >=14.4 TB usable HPE Enterprise Storage for Windows Server / WSFC. LUN00-LUN09 must be at or above their controlled minimum capacities.

## Purpose

GDPS DR physical file/service cluster node replacing the ALPHA6 Production Backup / DR capability.

## Special requirements

Provision in the two-node IM GDPS DR WSFC cluster. DR receives PROD replication. Redundant power/network/FC, MPIO, independent File Share Witness, and no authoritative GDPS business files on local disk.

Coordinate patching/reboots with IMVMGDPSFSD2 so both DR nodes are never rebooted simultaneously.

## Controlled references

- GDPS Hardware Master v4.3
- GDPS Hardware Acquisition SOW - CDW-G v1.9
- GDPS Storage Architecture and LUN Design v1.1
- GDPS Windows File Cluster and SMB Namespace Standard v1.8
