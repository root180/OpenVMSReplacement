# ST-02 - GDPS PROD Storage Request

## Request

- System: GDPS
- Environment: PROD
- Location: HQ
- Connected nodes: HQVMGDPSFSP1, HQVMGDPSFSP2
- Storage platform: HPE Enterprise Storage supported for Windows Server 2025 / WSFC; exact model TBD by HPE/CDW-G
- Minimum usable capacity: **>= 14.4 TB**
- Connectivity: redundant Fibre Channel fabrics + Windows MPIO
- Purpose: provide authoritative shared enterprise storage for the two-node GDPS PROD Windows Server Failover Cluster at HQ.

## LUN minimums

| LUN | Minimum Capacity | Current Used Baseline |
|---|---:|---:|
| LUN00 | >= 300 GB | 150 GB |
| LUN01 | >= 500 GB | 400 GB |
| LUN02 | >= 600 GB | 485 GB |
| LUN03 | >= 100 GB | 50 GB |
| LUN04 | >= 50 GB | 20 GB |
| LUN05 | >= 100 GB | 20 GB |
| LUN06 | >= 100 GB | 60 GB |
| LUN07 | >= 50 GB | 5 GB |
| LUN08 | >= 50 GB | 10 GB |
| LUN09 | >= 100 GB | 5 GB |

Minimum mapped allocation: **>= 1,950 GB**  
Current used baseline: **1,205 GB**

## Sizing rule

Capacity may be larger but must not be smaller. Every mapped LUN must meet or exceed its controlled minimum.

## Replication

PROD is the authoritative replication source to GDPS DR and GDPS COOP using the HPE-supported replication technology selected during engineering.

## Engineering requirements

- HPE Windows Server / WSFC support
- redundant FC fabrics and HBAs
- Windows MPIO
- zoning and LUN masking
- controller/protection policy
- replication licensing and technology
- monitoring and support
- independent File Share Witness; do not host witness on clustered business-data storage

## Controlled references

- GDPS Hardware Master v4.3
- GDPS Hardware Acquisition SOW - CDW-G v1.9
- GDPS Storage Architecture and LUN Design v1.1
- GDPS Windows File Cluster and SMB Namespace Standard v1.8
