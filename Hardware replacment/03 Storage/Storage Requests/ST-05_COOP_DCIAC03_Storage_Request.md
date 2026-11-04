# ST-05 - GDPS COOP / DCIAC03 Storage Request

## Request

- System: GDPS
- Environment: COOP
- Location: DCIAC03 / Data Center in a Crate
- Connected nodes: IMGIPSDPSFSC3, IMGIPSDPSFSC4
- Replaces: ALPHA13 two-node COOP cluster
- Storage platform parity: HPE Primera
- Minimum usable capacity: **>= 21.4 TB**
- Connectivity: redundant Fibre Channel fabrics + Windows MPIO
- Purpose: shared enterprise recovery storage for the two-node GDPS COOP DCIAC03 cluster.

## LUN minimums

| LUN | Minimum Capacity | Current Used Baseline |
|---|---:|---:|
| LUN00 | >= 300 GB | 162.2 GB |
| LUN01 | **>= 600 GB** | **488.2 GB** |
| LUN02 | >= 600 GB | 505.4 GB |
| LUN03 | >= 100 GB | 58.6 GB |
| LUN04 | >= 50 GB | 20.3 GB |
| LUN05 | >= 100 GB | 25.7 GB |
| LUN06 | >= 100 GB | 15.2 GB |
| LUN07 | >= 50 GB | 5.6 GB |
| LUN08 | >= 50 GB | 9.0 GB |
| LUN09 | >= 100 GB | 0.1 GB |

Controlled mapped minimum: **>= 2,050 GB**  
Current RAIDSET00-RAIDSET09 used baseline: **≈ 1,290 GB**

LUN01 is raised from 500 GB to 600 GB because the source RAIDSET01 is approximately 488 GB used (~98% full).

## Sizing rule

Capacity may be larger but must not be smaller. Every retained mapped LUN must meet or exceed its controlled minimum.

## Additional source-volume disposition

The following ALPHA3 source volumes were omitted from the earlier LUN map and require explicit disposition before final storage presentation is approved:

T4DATA, OPS_DISK, CIFS_DATA, CIFS_LOCK, CIFS_LOGS, DATA_COPY, ADMIN, USER, and SCRATCH.

Together they represent approximately **2.3 TB allocated and 128 GB used**. Each must be either mapped to a defined GDPS target or retired with approved rationale. The CIFS volumes require specific review against native Windows SMB before retirement. ALPHA3SYS is not a shared-data carry-forward LUN because its system role moves to local Windows C:\.

## Replication

Configure DCIAC03 as an independent PROD recovery-replication target.

## Engineering requirements

- HPE Windows Server / WSFC support
- redundant FC fabrics and HBAs
- Windows MPIO
- zoning and LUN masking
- controller/protection policy
- replication licensing and technology
- monitoring and support
- DCIAC03 crate integration
- independent File Share Witness on a third system, not on clustered data storage
- COOP patching/maintenance must not overlap PROD maintenance

## Controlled references

- GDPS Hardware Master v4.3
- GDPS Hardware Acquisition SOW - CDW-G v1.9
- GDPS Storage Architecture and LUN Design v1.1
- GDPS Windows File Cluster and SMB Namespace Standard v1.8
- v8 10-Node Physical Server Tickets
