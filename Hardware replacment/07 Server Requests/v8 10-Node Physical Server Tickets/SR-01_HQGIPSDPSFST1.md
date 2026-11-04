# SR-01 — HQGIPSDPSFST1

## ServiceNow New Server Request

Fields below follow the order of the ServiceNow form. Copy each value into its matching field.

### What is the platform for this Request?

Physical Server

### What Business Unit will this server support?

GOVERNMENT INTEGRATED PRINT SERVICES

### Please select system environment for this request:

Test

### Data center where server will be located:

HQ

### Choose OS type for server:

Windows Server 2025

### DATA DRIVE REQUIREMENTS:

C:\ = 200 GB; D:\ = 300 GB. Total 500 GB usable native/local storage, hardware RAID 1. Shared business data resides on separately provisioned SAN storage.

### Memory Requirements: Select the amount of memory needed:

Select the approval-required memory option available in the catalog. The requested quantity is 128 GB RAM minimum, stated in Purpose and Special Requirements.

### Select the server network:

Server Distribution

### Please list the purpose for this Server as well as what service the Server will support?

GDPS TEST physical file/service cluster node 1, paired with HQGIPSDPSFST2 (SR-02). Reproduces the existing Alpha two-node production cluster pattern to validate production-equivalent clustering, shared SAN storage, failover, and recovery before release. Requested hostname: HQGIPSDPSFST1. Required memory: 128 GB RAM minimum.

### If this request is to replace an existing server, please list the name of the server being replaced. Please note to enter N/A if not replacing existing server.

N/A - new GDPS TEST environment; no existing Alpha node is being replaced.

### Please add Active Directory Users that will need RDP Access to the Server.

Matthew Taylor

### List any special requirements that IT needs to be aware of regarding the Server request.

Provision this physical server with a minimum of 128 GB RAM.

Provision this request as a **physical server** with hostname **HQGIPSDPSFST1**. This server is one member of the two-node GDPS TEST Windows Server Failover Cluster with peer node **HQGIPSDPSFST2** (SR-02). Both nodes are active (active/active), matching the existing Alpha clusters. Provide minimum 128 GB RAM, native/local Windows storage with C:\ = 200 GB and D:\ = 300 GB (500 GB total, hardware RAID 1), redundant hot-plug power, redundant Server Distribution network connectivity, redundant Fibre Channel HBA connectivity to two independent fabrics (as the dual Brocade fabrics on the Alpha clusters), Windows MPIO support, and shared HPE enterprise storage.

TEST shared SAN storage baseline: **14.4 TB usable minimum** (parity with the ALPHA3 production HPE 3PAR array), with final LUN presentation per the controlled GDPS storage design and storage request ST-01.

Use an independent File Share Witness for WSFC quorum. The witness must reside on a third independent system: not on either TEST cluster node and not on the TEST cluster's own shared storage. It holds quorum metadata only.

Peer nodes must never be rebooted together. SR-01 and SR-02 must be in different, non-overlapping approved patch groups/windows.

Final IP, DNS, VLAN, firewall, Fibre Channel zoning, LUN masking, WWPN, and other infrastructure values are assigned by the appropriate GPO infrastructure teams.

Native / local storage requirement: C:\ = 200 GB. D:\ = 300 GB. Total native/local storage = 500 GB usable, hardware RAID 1 (mirrored). Shared clustered business data remains on separately provisioned SAN storage.

Existing Alpha DNS / IP traceability: N/A - TEST is new and has no existing Alpha node/IP replacement.

Patching: Mondays only. Assign separate, non-overlapping approved Monday patch windows to peer nodes. DR and COOP windows must not overlap PROD. Select the exact Monday catalog group available in ServiceNow; IT must confirm the week and time. SR-01 must not overlap SR-02.

### Please choose the patching group that best fits the schedule of the server.

Mondays only. Assign separate, non-overlapping approved Monday patch windows to peer nodes. DR and COOP windows must not overlap PROD. Select the exact Monday catalog group available in ServiceNow; IT must confirm the week and time. SR-01 must not overlap SR-02.

### If these VMs are to be a redundant or clustered pair, pick the Affinity rule for the VMs if needed.

N/A / None — physical server

### Description

HQGIPSDPSFST1 — GDPS TEST physical file/service cluster node 1, paired with HQGIPSDPSFST2 (SR-02). Follows the existing Alpha two-node production cluster pattern to validate production-equivalent clustering, storage, failover, and recovery before release.

### Watchlist

Muyiwa Aniyikaye

## Replacement Control

TEST is the only new physical cluster and does not replace an existing Alpha environment. Its design follows the Alpha two-node production cluster pattern for production-equivalent validation.

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
