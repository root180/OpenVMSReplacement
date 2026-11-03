# SR-08 — IMVMGDPSFSC2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | COOP |
| Data Center | DCIAC (Data Center in a Crate) |
| OS | Windows Server 2025 |
| Native / Local Storage Requirement | Minimum 300 GB usable native/local server storage, implemented as hardware RAID 1 (mirrored). Windows Server and locally installed GDPS applications/services reside on native server storage. Shared clustered data remains on separately provisioned recovery SAN storage. |
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

This server is one member of the two-node GDPS COOP Windows Server Failover Cluster replacing the ALPHA10 / DCIAC02 COOP capability. Provide minimum 128 GB RAM, minimum 300 GB usable native/local storage using hardware RAID 1 (mirrored), redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to independent storage paths/fabrics, Windows MPIO support, and shared HPE enterprise recovery storage.

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

Minimum **300 GB usable native/local storage per physical server, hardware RAID 1 (mirrored)**. Windows Server and locally installed GDPS applications/services use native server storage; shared clustered recovery data remains on separately provisioned SAN storage.
