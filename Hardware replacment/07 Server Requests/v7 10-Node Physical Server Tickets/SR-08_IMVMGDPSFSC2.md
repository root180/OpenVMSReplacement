# SR-08 — IMVMGDPSFSC2

## ServiceNow New Server Request

| Field | Required value |
|---|---|
| Platform | Physical Server |
| Business Unit | GOVERNMENT INTEGRATED PRINT SERVICES |
| System Environment | COOP |
| Data Center | DCIAC (Data Center in a Crate) |
| OS | Windows Server 2025 |
| Data Drive Requirements | N/A — no authoritative GDPS business data on local disk |
| Memory | 128 GB minimum |
| Server Network | Server Distribution |
| Purpose | GDPS COOP / DCIAC physical recovery cluster node replacing ALPHA12. Requested hostname: IMVMGDPSFSC2. |
| Existing Server Being Replaced | ALPHA12 - ALPHA10 / DCIAC02 COOP Cluster node. |
| Existing Alpha DNS / IP Traceability | alpha12.gpo.gov - 172.23.5.45, 172.23.5.44 |
| RDP Access | Matthew Taylor |
| Patching Group | SCCM_Server_Patching_General_D — Server Reboots 4th Friday 11 am–2 pm, subject to cluster-safe sequential reboot coordination |
| Affinity Rule | N/A / None — physical server |
| Description | IMVMGDPSFSC2 — GDPS COOP / DCIAC physical recovery cluster node replacing ALPHA12. |
| Watchlist | Muyiwa Aniyikaye |

## Special Requirements

Provision this physical server with hostname **IMVMGDPSFSC2**. Do not rename without an approved architecture change.

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
