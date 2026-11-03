# SR-02 — HQVMGDPSFST2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | TEST |
| Data Center | HQ |
| OS | Windows Server 2025 |
| Native / Local Storage Requirement | C:\\ = 150 GB. D:\\ = 330 GB. Both are native/local server storage. Shared clustered data remains on separately provisioned SAN storage. |
| Memory | 128 GB minimum |
| Server Network | Server Distribution |
| Purpose | GDPS TEST physical file/service cluster node 2. TEST follows the Alpha two-node cluster pattern used in production so production-equivalent clustering, storage, failover, and recovery can be validated before release. Requested hostname: HQVMGDPSFST2. |
| Existing Server Being Replaced | N/A - new GDPS TEST environment; no existing Alpha node is being replaced. |
| Existing Alpha DNS / IP Traceability | N/A - TEST is new and has no existing Alpha node/IP replacement. |
| RDP Access | Matthew Taylor |
| Patching Group | Node 2 must be assigned to a different approved SCCM patch group/window from SR-01. SR-01 is SCCM_Server_Patching_General_D — Server Reboots 4th Friday 11 am–2 pm. Select the exact non-overlapping peer group label from the live ServiceNow catalog before submission; SR-02 must not use General_D if that would overlap SR-01. |
| Affinity Rule | N/A / None — physical server |
| Description | HQVMGDPSFST2 — GDPS TEST physical file/service cluster node 2. |
| Watchlist | Muyiwa Aniyikaye |

## Special Requirements

Provision this request as a **physical server** with hostname **HQVMGDPSFST2**. The `VM` characters are part of the established GPO hostname convention for this GDPS server and do not indicate that the platform is virtual. Do not rename without an approved architecture change.

This server is one member of a two-node Windows Server Failover Cluster and follows the Alpha two-node cluster pattern used in production. Provide minimum 128 GB RAM, native/local Windows storage with C:\\ = 150 GB and D:\\ = 330 GB, redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent storage paths/fabrics, Windows MPIO support, and shared HPE enterprise storage.

TEST shared SAN storage baseline: **14.4 TB usable minimum**, with final LUN presentation per the controlled GDPS storage design/storage request.

Use an independent File Share Witness for WSFC quorum. The witness must reside on a third independent system, not on either TEST cluster node and not on the TEST cluster's own shared storage.

The two TEST nodes must not share an overlapping reboot window. SR-01 and SR-02 must be placed in different approved SCCM patch groups/windows so peer nodes are never rebooted simultaneously.

Final IP, DNS, VLAN, firewall, Fibre Channel zoning, LUN masking, WWPN, and other infrastructure values are assigned by the appropriate GPO infrastructure teams.

## Replacement Control

TEST is the only new physical cluster and does not replace an existing Alpha TEST environment. Its design follows the Alpha two-node production cluster pattern for production-equivalent validation.

## Native Storage Baseline

Provision the native/local Windows disk layout as:

- **C:\\ = 150 GB** — Windows Server system/OS volume.
- **D:\\ = 330 GB** — native/local GDPS application and server-local working volume.

Shared clustered data remains on separately provisioned SAN storage.
