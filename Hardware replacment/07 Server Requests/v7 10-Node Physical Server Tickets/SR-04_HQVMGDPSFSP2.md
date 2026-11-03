# SR-04 — HQVMGDPSFSP2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | PROD |
| Data Center | HQ |
| OS | Windows Server 2025 |
| Native / Local Storage Requirement | C:\\ = 200 GB. D:\\ = 300 GB. Total native/local storage = 500 GB, mirrored. Shared clustered business data remains on separately provisioned SAN storage. |
| Memory | 128 GB minimum |
| Server Network | Server Distribution |
| Purpose | GDPS PROD physical file/service cluster node 2 replacing N3B. Requested hostname: HQVMGDPSFSP2. |
| Existing Server Being Replaced | N3B - ALPHA3 Production Cluster node. |
| Existing Alpha DNS / IP Traceability | N3B: 172.16.35.19 (IE2, primary), 172.16.35.20 (IE3). Cluster alias: alpha3.gpo.gov. |
| RDP Access | Matthew Taylor; Muyiwa Aniyikaye |
| Patching Group | PROD node 2 must use an approved production patch group/window that does not overlap SR-03. Do not use a shared 4th-Friday 11 am–2 pm window for both PROD nodes. Select the exact production catalog label in ServiceNow before submission. |
| Affinity Rule | N/A / None — physical server |
| Description | HQVMGDPSFSP2 — GDPS PROD physical file/service cluster node 2 replacing N3B. |
| Watchlist | Muyiwa Aniyikaye |

## Special Requirements

Provision this request as a **physical server** with hostname **HQVMGDPSFSP2**. The `VM` characters are part of the established GPO hostname convention for this GDPS server and do not indicate that the platform is virtual. Do not rename without an approved architecture change.

This server is one member of the two-node GDPS PROD Windows Server Failover Cluster and replaces the existing N3B physical node. Provide minimum 128 GB RAM, native/local Windows storage with C:\\ = 200 GB and D:\\ = 300 GB, 500 GB total mirrored, redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent storage paths/fabrics, Windows MPIO support, and shared HPE enterprise storage.

PROD shared SAN storage baseline: **14.4 TB usable minimum**, with final LUN presentation per the controlled GDPS storage design/storage request.

Use an independent File Share Witness for WSFC quorum. The witness must reside on a third independent system, not on either PROD cluster node and not on the PROD cluster's own shared storage.

The PROD nodes must not share an overlapping reboot window. SR-03 and SR-04 must be assigned to separate approved production patch groups/windows. A daytime 4th-Friday 11 am–2 pm shared reboot window is not accepted for both nodes.

Final IP, DNS, VLAN, firewall, Fibre Channel zoning, LUN masking, WWPN, and other infrastructure values for GDPS are assigned by the appropriate GPO infrastructure teams.

## Existing Network Traceability

N3B has confirmed node interfaces:
- **172.16.35.19 — IE2, primary**
- **172.16.35.20 — IE3**
- **Cluster alias:** `alpha3.gpo.gov`

These Alpha addresses are retained for replacement and migration traceability; they are not automatically assigned to the new GDPS node.

## Native Storage Baseline

Provision the native/local Windows disk layout as:

- **C:\\ = 200 GB** — Windows Server system/OS volume; one-to-one capacity match to Alpha3 `ALPHA3SYS`.
- **D:\\ = 300 GB** — native/local GDPS application, paging, and server-local working volume; one-to-one capacity match to N3B `N3B_PAGE`.
- **Total native/local storage = 500 GB, mirrored.**

Shared clustered business data remains on separately provisioned SAN storage.
## Storage Disk Justification

The native Windows disk layout matches the current Alpha3 production node roles one-to-one:

| Windows drive | Replaces on Alpha3 | Alpha3 size | Basis |
|---|---|---:|---|
| **C:\\ = 200 GB** | System disk `ALPHA3SYS` (OS, system software) | 200 GB | One-to-one replacement of the current Alpha3 system-disk capacity. |
| **D:\\ = 300 GB** | Local disk `N3B_PAGE` (paging) + locally installed services | 300 GB | One-to-one replacement of the current Alpha3 local-disk capacity; locally installed GDPS services run here. |
| **Total 500 GB** | — | **500 GB** (200 + 300) | Matches the current Alpha3 production node total for these roles. |

**ServiceNow justification text:**

> Sizes match the current Alpha3 production node one-to-one. The Alpha uses a 200 GB system disk (ALPHA3SYS) and a 300 GB local disk (N3B_PAGE) per node. On Windows, C:\\ (200 GB) replaces the system disk and D:\\ (300 GB) replaces the local disk and hosts locally installed GDPS services. Total 500 GB, mirrored. Business data remains on SAN.
