# SR-03 - HQVMGDPSFSP1

## GPO IT Service Hub - New Server Request

| Field | Value |
|---|---|
| Requested physical server name | HQVMGDPSFSP1 |
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| Environment | Production |
| Data center | HQ |
| OS | Windows Server 2025 |
| Memory | 128 GB minimum |
| Network | Server Distribution |
| Description | HQVMGDPSFSP1 - GDPS PROD physical file/service cluster node 1. |
| Replacement | Part of replacement of ALPHA3 Production Cluster (N3A + N3B). |
| RDP access | Matthew Taylor |
| Watchlist | Muyiwa Aniyikaye |
| Patching group | SCCM_Server_Patching_General_D - Server Reboots 4th Friday 11 am-2pm |

## Data drive requirements

No additional local authoritative data drive. PROD business files reside on >=14.4 TB usable HPE Enterprise Storage for Windows Server / WSFC. LUN00-LUN09 must be at or above their controlled minimum capacities.

## Purpose

GDPS PROD physical file/service cluster node replacing the ALPHA3 production clustered file-service capability.

## Special requirements

Provision as one member of the two-node HQ GDPS PROD WSFC cluster. Redundant power/network/FC, MPIO, independent File Share Witness, and no authoritative GDPS business files on local disk. PROD is the authoritative environment and replication source to DR and COOP.

Coordinate patching/reboots with HQVMGDPSFSP2 so both PROD nodes are never rebooted simultaneously.

## Controlled references

- GDPS Hardware Master v4.3
- GDPS Hardware Acquisition SOW - CDW-G v1.9
- GDPS Storage Architecture and LUN Design v1.1
- GDPS Windows File Cluster and SMB Namespace Standard v1.8
