# GDPS Storage Architecture and LUN Design v1.1

## Storage platform

GDPS TEST, PROD, DR, and COOP use HPE enterprise storage supported for Windows Server and WSFC.

Exact HPE model remains subject to HPE/CDW-G engineering validation.

DEV remains on the existing GPO Enterprise NAS.

## Environment capacity minimums

| Environment | Storage | Minimum Capacity |
|---|---|---:|
| DEV | Existing GPO Enterprise NAS | 2 TB |
| TEST | HPE Enterprise Storage for Windows / WSFC | 14.4 TB usable |
| PROD | HPE Enterprise Storage for Windows / WSFC | 14.4 TB usable |
| DR | HPE Enterprise Storage for Windows / WSFC | 14.4 TB usable |
| COOP | HPE Enterprise Recovery Storage for Windows / WSFC | 21.4 TB usable |

## GDPS LUNs

| GDPS LUN | Minimum Allocated Capacity | Current Used Baseline | Baseline Free | Source Mapping |
|---|---:|---:|---:|---|
| LUN00 | >= 300 GB | 150 GB | 150 GB | RAIDSET00 |
| LUN01 | >= 500 GB | 400 GB | 100 GB | RAIDSET01 |
| LUN02 | >= 600 GB | 485 GB | 115 GB | RAIDSET02 |
| LUN03 | >= 100 GB | 50 GB | 50 GB | RAIDSET03 |
| LUN04 | >= 50 GB | 20 GB | 30 GB | RAIDSET04 |
| LUN05 | >= 100 GB | 20 GB | 80 GB | RAIDSET05 |
| LUN06 | >= 100 GB | 60 GB | 40 GB | RAIDSET06 |
| LUN07 | >= 50 GB | 5 GB | 45 GB | RAIDSET07 |
| LUN08 | >= 50 GB | 10 GB | 40 GB | RAIDSET08 |
| LUN09 | >= 100 GB | 5 GB | 95 GB | RAIDSET09 |
| **Total** | **>= 1,950 GB** | **1,205 GB** | **745 GB baseline** | |

## Sizing rule

Each GDPS LUN shall be provisioned at or above the corresponding minimum allocated capacity. No mapped LUN may be smaller. Larger allocations are permitted for growth, alignment, storage efficiency, or HPE/CDW-G engineering recommendations.

## Connectivity

- redundant Fibre Channel fabrics
- redundant HBAs
- Windows MPIO
- WSFC shared-storage support

## Replication

- PROD -> DR
- PROD -> COOP

## Naming rule

The GDPS storage objects are LUN00-LUN09. RAIDSET00-RAIDSET09 appear only as source mapping values for migration traceability.
