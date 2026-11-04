# GDPS Physical File Cluster Nodes - Memory (RAM) Requirement Justification

**Project:** PR-26-GPO-2540 - Alpha System Replacement  
**Organization:** GIPS Application Support  
**Date:** November 3, 2026  
**Applies to:** ServiceNow requests SR-01 through SR-10

## Request summary

GIPS Application Support requests approval for **128 GB RAM on each of the ten GDPS physical file/service cluster nodes**.

This single justification applies to all ten physical-server requests. Eight of the servers replace existing Alpha/OpenVMS physical cluster nodes one-for-one. The two TEST servers are new physical nodes built to the same production-class node standard so TEST can reproduce production-equivalent clustering, failover, storage, and cutover behavior.

## Servers covered

All ten requests are for **physical Windows Server 2025 servers**, each belonging to a two-node Windows Server Failover Cluster.

| Request | GDPS server | Environment | Location | Existing Alpha node / role replaced |
|---|---|---|---|---|
| SR-01 | HQGIPSDPSFST1 | TEST | HQ | None - new TEST node |
| SR-02 | HQGIPSDPSFST2 | TEST | HQ | None - new TEST node |
| SR-03 | HQGIPSDPSFSP1 | PROD | HQ | ALPHA3 - N3A |
| SR-04 | HQGIPSDPSFSP2 | PROD | HQ | ALPHA3 - N3B |
| SR-05 | IMGIPSDPSFSD1 | DR | IM | ALPHA6 - N6A |
| SR-06 | IMGIPSDPSFSD2 | DR | IM | ALPHA6 - N6B |
| SR-07 | IMGIPSDPSFSC1 | COOP | DCIAC02 | ALPHA10 - ALPHA11 |
| SR-08 | IMGIPSDPSFSC2 | COOP | DCIAC02 | ALPHA10 - ALPHA12 |
| SR-09 | IMGIPSDPSFSC3 | COOP | DCIAC03 | ALPHA13 node A - source node name pending confirmation |
| SR-10 | IMGIPSDPSFSC4 | COOP | DCIAC03 | ALPHA13 node B - source node name pending confirmation |

The physical acquisition therefore consists of **five separate two-node clusters and ten physical servers total**.

## Why the 16 GB catalog limit does not fit these servers

The New Server form lists memory selections intended for ordinary general-purpose server requests. These GDPS requests are different:

1. **Dedicated physical hardware.** Memory is purchased with each physical server; it is not drawn from a shared virtualization host pool.
2. **Agency replacement system.** GDPS replaces the Alpha/OpenVMS infrastructure that provides file/service functions supporting Congressional document processing and delivery.
3. **GPO is the system owner.** GDPS is a GPO-built replacement platform, so there is no outside application vendor that defines the memory requirement. This engineering justification is the GPO system-owner requirement. CDW-G/HPE may additionally provide hardware sizing confirmation for the quoted server configuration if required by the approval process.

## Existing Alpha production memory baseline

The current ALPHA3 production cluster provides the direct measured sizing anchor.

On November 3, 2026, the ALPHA3 nodes N3A and N3B were confirmed with approximately **127.99 GB RAM installed per node**. GDPS therefore uses **128 GB RAM per physical node** as the one-for-one production memory baseline.

ALPHA3 is the sizing standard because PROD carries the live workload. TEST mirrors the PROD node configuration for production-equivalent validation. DR and both COOP clusters must be capable of assuming production recovery workload, so their nodes use the same 128 GB memory standard.

## Alpha-to-GDPS replacement baseline

| GDPS cluster | GDPS nodes | Alpha basis | RAM per GDPS node | Reason |
|---|---|---|---:|---|
| TEST | HQGIPSDPSFST1, HQGIPSDPSFST2 | Production-class TEST based on ALPHA3 / GDPS PROD | 128 GB | TEST must reproduce the production node configuration for failover and cutover validation. |
| PROD | HQGIPSDPSFSP1, HQGIPSDPSFSP2 | ALPHA3 N3A/N3B | 128 GB | Direct one-for-one memory match to measured ALPHA3 production nodes. |
| DR | IMGIPSDPSFSD1, IMGIPSDPSFSD2 | ALPHA6 recovery role; sized to ALPHA3 production standard | 128 GB | Either DR node must support production recovery workload within its cluster. |
| COOP DCIAC02 | IMGIPSDPSFSC1, IMGIPSDPSFSC2 | ALPHA10 recovery role; sized to ALPHA3 production standard | 128 GB | DCIAC02 must support production COOP recovery workload. |
| COOP DCIAC03 | IMGIPSDPSFSC3, IMGIPSDPSFSC4 | ALPHA13 recovery role; sized to ALPHA3 production standard | 128 GB | DCIAC03 must support production COOP recovery workload. |

## Why each node needs 128 GB

### 1. Either node must carry the cluster workload after a peer-node failure

Each environment uses a two-node cluster. The memory requirement is not based on each node permanently carrying only half of the workload. Either node must be able to continue the environment's service role when its peer is unavailable.

This is **node-level cluster failover**, not a stretched TEST/PROD design. TEST and PROD are both located at HQ. Site-level recovery is provided by the separate DR and COOP environments.

### 2. File-serving workload benefits directly from system memory

The Alpha/OpenVMS environment uses memory for file-system caching. On Windows Server, SMB/file services likewise use system memory to cache frequently accessed files and directory information. The GDPS replacement also runs the locally installed GDPS services required for its file/service role.

Reducing memory substantially below the measured Alpha3 production-node baseline would remove file-cache and operating headroom from the replacement platform.

### 3. Peak legislative workload must remain supportable during failover

The platform supports Congressional document workflows for the House, Senate, Library of Congress, and GovInfo. Session-day peaks increase file arrival, file-serving, and polling activity. The surviving node of a two-node cluster must absorb that load without the memory reduction becoming a new bottleneck.

### 4. Windows and infrastructure services require additional operating headroom

Each node also supports Windows Server, Windows Server Failover Clustering, storage multipath/MPIO, endpoint/security controls, backup tooling, monitoring, and locally installed GDPS services.

The 128 GB requirement preserves the production memory class being replaced while providing the operating headroom expected of the Windows replacement platform.

### 5. Identical node sizing is required across each cluster and recovery tier

Both nodes in a cluster should be equivalently sized so failover does not move the workload onto a materially smaller server.

TEST uses the same node memory standard as PROD for production-equivalent rehearsal. DR, DCIAC02, and DCIAC03 use the same standard because they are recovery environments for production.

### 6. Physical-server lifecycle

These servers are a capital hardware purchase expected to remain in service for multiple years. Installing the required memory at acquisition avoids creating a known capacity reduction from the Alpha3 baseline and avoids a later outage/change cycle solely to restore memory that should have been included in the original build.

## Relationship to the controlled local-storage standard

The RAM request is independent from, but consistent with, the controlled per-node native-storage requirement:

- **C:\ = 200 GB**
- **D:\ = 300 GB**
- **500 GB usable total**
- **hardware RAID 1 mirrored**

The 200 GB C:\ role replaces the ALPHA3 system-disk capacity. The 300 GB D:\ role replaces the Alpha node-local 300 GB disk role and provides the local volume for installed GDPS services. Shared clustered business data remains on SAN.

## Approval requested

Approve **128 GB RAM per server** for the ten GDPS physical file/service cluster nodes in SR-01 through SR-10.

The 128 GB value is the measured ALPHA3 production-node memory baseline and is applied consistently to PROD, production-equivalent TEST, DR, and both COOP recovery clusters.

## Controlled relationship

This justification is subordinate to and must remain synchronized with:

- `GDPS_Hardware_Master_v4.3.md`
- `GDPS_Hardware_Acquisition_SOW_CDWG_v1.9.md`
- `GDPS_CDWG_Costing_and_Acquisition_List_v11.md`
- `GDPS_Storage_Architecture_and_LUN_Design_v1.1.md`
- `GDPS_Network_Infrastructure_and_Addressing_Design_v1.5.md`
- `GDPS_Windows_File_Cluster_and_SMB_Namespace_Standard_v1.8.md`
- `07 Server Requests/v8 10-Node Physical Server Tickets/`

If any of those controlled artifacts changes the physical server count, placement, or memory standard, this justification must be reviewed at the same time.
