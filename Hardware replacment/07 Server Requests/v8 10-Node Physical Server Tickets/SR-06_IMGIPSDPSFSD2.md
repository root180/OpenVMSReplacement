# SR-06 — IMGIPSDPSFSD2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | DR |
| Data Center | IM |
| OS | Windows Server 2025 |
| Data Drive Requirements | C:\ = 200 GB. D:\ = 300 GB. |
| Native / Local Storage Requirement | C:\ = 200 GB. D:\ = 300 GB. Total native/local storage = 500 GB usable, hardware RAID 1 (mirrored). Shared clustered business data remains on separately provisioned SAN storage. |
| Memory | 128 GB minimum. See `GDPS_Memory_RAM_Requirement_Justification_v1.0.md` for the GPO system-owner engineering justification covering SR-01 through SR-10. |
| Server Network | Server Distribution |
| Purpose | GDPS DR physical file/service cluster node 2 replacing N6B. Requested hostname: IMGIPSDPSFSD2. |
| Existing Server Being Replaced | N6B - ALPHA6 DR / Production Backup Cluster node (HPE Integrity i6; HPE 3PAR storage). |
| Existing Alpha DNS / IP Traceability | alpha6.gpo.gov - 172.19.128.41, .42, .43, .44 (cluster set). N6B holds the addresses not used by N6A; node split to be confirmed with TCPIP SHOW INTERFACE. |
| RDP Access | Matthew Taylor |
| Patching Group | DR node 2: approved patch group/window that does not overlap SR-05 or the PROD window. Select the exact catalog label in ServiceNow before submission. |
| Affinity Rule | N/A / None — physical server |
| Description | IMGIPSDPSFSD2 — GDPS DR physical file/service cluster node 2 replacing N6B. |
| Watchlist | Muyiwa Aniyikaye |

## Special Requirements

Provision this request as a **physical server** with hostname **IMGIPSDPSFSD2**. The `VM` characters are part of the established GPO hostname convention for this GDPS server and do not indicate that the platform is virtual. Do not rename without an approved architecture change.

This server is one member of the two-node GDPS DR Windows Server Failover Cluster with peer node **IMGIPSDPSFSD1** (SR-05). Both nodes are active (active/active), matching the existing Alpha clusters. Provide minimum 128 GB RAM, native/local Windows storage with C:\ = 200 GB and D:\ = 300 GB (500 GB total, hardware RAID 1), redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to two independent fabrics (as the dual Brocade fabrics on the Alpha clusters), Windows MPIO support, and shared HPE enterprise storage.

DR shared SAN storage baseline: **14.4 TB usable minimum** (parity with the ALPHA6 HPE 3PAR array), with final LUN presentation per the controlled GDPS storage design and storage request ST-03. Production data is replicated from PROD (HQ) to DR, as ALPHA3 replicates to ALPHA6 today.

Use an independent File Share Witness for WSFC quorum. The witness must reside on a third independent system: not on either DR cluster node and not on the DR cluster's own shared storage. It holds quorum metadata only.

Peer nodes must never be rebooted together. SR-06 and SR-05 must be in different, non-overlapping approved patch groups/windows, and this node must not share the PROD patching window.

Final IP, DNS, VLAN, firewall, Fibre Channel zoning, LUN masking, WWPN, and other infrastructure values are assigned by the appropriate GPO infrastructure teams.

## Replacement Control

This request is a one-for-one physical replacement of the Alpha node identified above, following the existing Alpha physical placement and recovery model. One physical Alpha node replaced by one physical GDPS node does not imply one-IP-for-one-IP; the GDPS node receives the interfaces and addresses needed to reproduce the existing node role.

## Existing Network Traceability

The Alpha DNS/IP information above is retained for source-system traceability and migration validation only. It does not assign or reserve an IP address for the new GDPS server. New GDPS IP/DNS/VLAN values remain subject to GPO Network/Security assignment.

## Native Storage Baseline

Provision the native/local Windows disk layout as:

- **C:\ = 200 GB** — Windows Server system/OS volume; one-to-one capacity match to ALPHA3 `ALPHA3SYS`.
- **D:\ = 300 GB** — native/local GDPS application, paging, and server-local working volume; one-to-one capacity match to N3B `N3B_PAGE`.
- **Total native/local storage = 500 GB usable, hardware RAID 1 (mirrored).**

Shared clustered business data remains on separately provisioned SAN storage.

## Storage Disk Justification

The native Windows disk layout matches the current ALPHA3 production node roles one-to-one (ALPHA3 is the GDPS sizing standard):

| Windows drive | Replaces on ALPHA3 | ALPHA3 size | Basis |
|---|---|---:|---|
| **C:\ = 200 GB** | System disk `ALPHA3SYS` (OS, system software) | 200 GB | One-to-one replacement of the current ALPHA3 system-disk capacity. |
| **D:\ = 300 GB** | Local disk `N3B_PAGE` (paging) + locally installed services | 300 GB | One-to-one replacement of the current ALPHA3 local-disk capacity; locally installed GDPS services run here. |
| **Total 500 GB** | — | **500 GB** (200 + 300) | Matches the current ALPHA3 production node total for these roles. |

**ServiceNow justification text:**

> Sizes match the current Alpha3 production node one-to-one. The Alpha uses a 200 GB system disk (ALPHA3SYS) and a 300 GB local disk (N3B_PAGE) per node. On Windows, C:\ (200 GB) replaces the system disk and D:\ (300 GB) replaces the local disk and hosts locally installed GDPS services. Total 500 GB, mirrored. Business data remains on SAN.
