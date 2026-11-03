# SR-04 — HQVMGDPSFSP2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | PROD |
| Data Center | HQ |
| OS | Windows Server 2025 |
| Native / Local Storage Requirement | Minimum 300 GB usable native/local server storage, implemented as hardware RAID 1 (mirrored). Windows Server and locally installed GDPS applications/services reside on native server storage. Shared clustered data remains on separately provisioned SAN storage. |
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

This server is one member of the two-node GDPS PROD Windows Server Failover Cluster and replaces the existing N3B physical node. Provide minimum 128 GB RAM, minimum 300 GB usable native/local storage using hardware RAID 1 (mirrored), redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent storage paths/fabrics, Windows MPIO support, and shared HPE enterprise storage.

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

The source N3B local device **`$59$DKA0:`** is an HP logical volume on the server's hardware RAID controller with approximately **300 GB** total capacity. The GDPS replacement therefore requires minimum **300 GB usable native/local storage using hardware RAID 1 (mirrored)**. Windows Server and locally installed GDPS applications/services use native server storage; shared clustered data remains on separately provisioned SAN storage.
