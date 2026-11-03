# SR-06 — IMVMGDPSFSD2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | DR |
| Data Center | IM |
| OS | Windows Server 2025 |
| Native / Local Storage Requirement | C:\\ = 200 GB. D:\\ = 300 GB. Total native/local storage = 500 GB, mirrored. Shared clustered business data remains on separately provisioned SAN storage. |
| Memory | 128 GB minimum |
| Server Network | Server Distribution |
| Purpose | GDPS DR physical file/service cluster node 2 replacing N6B. Requested hostname: IMVMGDPSFSD2. |
| Existing Server Being Replaced | N6B - ALPHA6 Production Backup / DR Cluster node. |
| Existing Alpha DNS / IP Traceability | alpha6.gpo.gov - 172.19.128.44, 172.19.128.43, 172.19.128.42, 172.19.128.41 (source cluster/service DNS set; node-specific split not established by DNS sweep) |
| RDP Access | Matthew Taylor |
| Patching Group | SCCM_Server_Patching_General_D — Server Reboots 4th Friday 11 am–2 pm, subject to cluster-safe sequential reboot coordination |
| Affinity Rule | N/A / None — physical server |
| Description | IMVMGDPSFSD2 — GDPS DR physical file/service cluster node 2 replacing N6B. |
| Watchlist | Muyiwa Aniyikaye |

## Special Requirements

Provision this physical server with hostname **IMVMGDPSFSD2**. Do not rename without an approved architecture change.

This server is a member of a two-node Windows Server Failover Cluster and must preserve the existing Alpha deployment pattern for the environment. Provide minimum 128 GB RAM, redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent storage paths/fabrics, Windows MPIO support, and shared HPE enterprise storage appropriate to the environment.

DR HPE enterprise storage for Windows Server / WSFC; final capacity and LUN presentation per controlled GDPS storage design.

Use an independent File Share Witness for WSFC quorum. The witness contains quorum metadata only and must not reside on clustered GDPS business-data storage.

Peer nodes in the same cluster must not be rebooted simultaneously. Patching and maintenance must preserve cluster availability.

Final IP, DNS, VLAN, firewall, Fibre Channel zoning, LUN masking, WWPN, and other infrastructure values are assigned by the appropriate GPO infrastructure teams.

## Replacement Control

This request follows the existing Alpha physical placement and recovery model. **TEST is the only new physical cluster.** All PROD, DR, and COOP requests identify the exact Alpha node being replaced.

For COOP requests, the deployment location is **DCIAC — Data Center in a Crate (CRATE)**, matching the existing COOP setup.

## Existing Network Traceability

The Alpha DNS/IP information above is retained for source-system traceability and migration validation only. It does not assign or reserve an IP address for the new GDPS server. New GDPS IP/DNS/VLAN values remain subject to GPO Network/Security assignment.

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
