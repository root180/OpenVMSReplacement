# SR-10 — IMVMGDPSFSC4

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
| Purpose | GDPS COOP / DCIAC physical recovery cluster node replacing N13B. Requested hostname: IMVMGDPSFSC4. |
| Existing Server Being Replaced | N13B - ALPHA13 / DCIAC03 COOP Cluster node. |
| Existing Alpha DNS / IP Traceability | alpha13.gpo.gov - 172.23.6.43, 172.23.6.42, 172.23.6.45, 172.23.6.44 (source cluster/service DNS set; node-specific split not established by DNS sweep) |
| RDP Access | Matthew Taylor |
| Patching Group | SCCM_Server_Patching_General_D — Server Reboots 4th Friday 11 am–2 pm, subject to cluster-safe sequential reboot coordination |
| Affinity Rule | N/A / None — physical server |
| Description | IMVMGDPSFSC4 — GDPS COOP / DCIAC physical recovery cluster node replacing N13B. |
| Watchlist | Muyiwa Aniyikaye |

## Special Requirements

Provision this physical server with hostname **IMVMGDPSFSC4**. Do not rename without an approved architecture change.

This server is a member of a two-node Windows Server Failover Cluster and must preserve the existing Alpha deployment pattern for the environment. Provide minimum 128 GB RAM, redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent storage paths/fabrics, Windows MPIO support, and shared HPE enterprise storage appropriate to the environment.

COOP / DCIAC HPE enterprise recovery storage; final capacity and LUN presentation per controlled GDPS storage design.

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
