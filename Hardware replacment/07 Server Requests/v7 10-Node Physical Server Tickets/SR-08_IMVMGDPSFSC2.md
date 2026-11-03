# SR-08 — IMVMGDPSFSC2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | COOP |
| Data Center | DCIAC (Data Center in a Crate) |
| OS | Windows Server 2025 |
| Native / Local Storage Requirement | C:\\ = 150 GB. D:\\ = 330 GB. Both are native/local server storage. Shared clustered data remains on separately provisioned SAN storage. |
| Memory | 128 GB minimum |
| Server Network | Server Distribution |
| Purpose | GDPS COOP / DCIAC02 physical recovery cluster node replacing ALPHA12 in the existing ALPHA10 COOP environment. Requested hostname: IMVMGDPSFSC2. |
| Existing Server Being Replaced | ALPHA12 - ALPHA10 COOP / DCIAC02 cluster node. |
| Existing Alpha DNS / IP Traceability | alpha12.gpo.gov - 172.23.5.45, 172.23.5.44. |
| RDP Access | Matthew Taylor; Muyiwa Aniyikaye |
| Patching Group | COOP node 2 must use an approved COOP patch group/window that does not overlap its COOP peer or either PROD node. Select the exact non-overlapping COOP catalog label in ServiceNow before submission. |
| Affinity Rule | N/A / None — physical server |
| Description | IMVMGDPSFSC2 — GDPS COOP / DCIAC02 physical recovery cluster node replacing ALPHA12. |
| Watchlist | Muyiwa Aniyikaye |

## Special Requirements

Provision this request as a **physical server** with hostname **IMVMGDPSFSC2**. The `VM` characters are part of the established GPO hostname convention for this GDPS server and do not indicate that the platform is virtual. The `IM` hostname prefix is the controlled GDPS naming prefix for this COOP node; actual deployment location remains **DCIAC / Data Center in a Crate, DCIAC02**, as stated in this request. Do not rename without an approved architecture change.

This server is one member of the two-node GDPS COOP Windows Server Failover Cluster replacing the ALPHA10 / DCIAC02 COOP capability. Provide minimum 128 GB RAM, native/local Windows storage with C:\\ = 150 GB and D:\\ = 330 GB, redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent storage paths/fabrics, Windows MPIO support, and shared HPE enterprise recovery storage.

COOP / DCIAC recovery SAN baseline: **21.4 TB usable minimum**, with final LUN presentation per the controlled GDPS storage design/storage request.

COOP recovery depends on production data replication into DCIAC. Storage replication from PROD to COOP is provisioned under the separate controlled GDPS storage/replication request and must be cross-referenced to this server request when its ServiceNow request number is available.

Use an independent File Share Witness for WSFC quorum. The witness must reside on a third independent system, not on either COOP cluster node and not on the COOP cluster's own shared recovery storage.

COOP patching must be independent from PROD patching. SR-08 must use a window that does not overlap either its COOP peer or the PROD cluster maintenance windows so production and COOP recovery capacity are not taken down together.

Final IP, DNS, VLAN, firewall, Fibre Channel zoning, LUN masking, WWPN, and other infrastructure values for GDPS are assigned by the appropriate GPO infrastructure teams.

## Existing Network Traceability

ALPHA12 is a node of **ALPHA10 COOP / DCIAC02** and resolves as:
- **172.23.5.45**
- **172.23.5.44**
- DNS: `alpha12.gpo.gov`

These Alpha addresses are retained for replacement and migration traceability; they are not automatically assigned to the new GDPS node.

## Native Storage Baseline

Provision the native/local Windows disk layout as:

- **C:\\ = 150 GB** — Windows Server system/OS volume.
- **D:\\ = 330 GB** — native/local GDPS application and server-local working volume.

Shared clustered data remains on separately provisioned SAN storage.

## Storage Disk Justification

The native Windows disk layout is based on the current Alpha3 production node roles:

| Windows drive | Replaces on Alpha3 | Alpha3 size | Basis |
|---|---|---:|---|
| **C:\\ = 150 GB** | System disk `ALPHA3SYS` (OS, system software) | 200 GB, 118 GB used | The OS role moves from SAN to local disk. 150 GB covers today's usage plus Windows update growth. |
| **D:\\ = 330 GB** | Local disk `N3B_PAGE` (paging) + locally installed services | 300 GB | Matches the Alpha dedicated 300 GB local disk, plus room for the GDPS services that will run locally. |
| **Total 480 GB** | — | **500 GB** (200 + 300) | Slightly less than the Alpha uses today for the same roles. |

**ServiceNow justification text:**

> Sizes are based on the current Alpha3 production node. The Alpha uses a 200 GB system disk (ALPHA3SYS, 118 GB used) and a 300 GB local disk (N3B_PAGE) per node, 500 GB total for system and paging. On Windows, both roles move to local storage: C:\\ (150 GB) replaces the system disk, and D:\\ (330 GB) replaces the local paging disk and hosts locally installed GDPS services. Total 480 GB, mirrored. Business data remains on SAN.
