# GDPS Storage Architecture and LUN Design v1.1

## Storage platform

GDPS TEST, PROD, DR, COOP IM, and COOP HQ use HPE enterprise storage supported for Windows Server and WSFC. Exact HPE replacement model remains subject to HPE/CDW-G engineering validation.

DEV remains on the existing GPO Enterprise NAS.

## Environment capacity minimums

| Environment / site | Storage request | Minimum usable capacity | Existing parity |
|---|---|---:|---|
| DEV | Existing GPO NAS | 2 TB | Existing NAS |
| TEST / HQ | ST-01 | 14.4 TB | Production-equivalent |
| PROD / HQ | ST-02 | 14.4 TB | ALPHA3 HPE 3PAR |
| DR / IM | ST-03 | 14.4 TB | ALPHA6 HPE 3PAR |
| COOP / IM | ST-04 | 14.4 TB | ALPHA10 HPE 3PAR |
| COOP / HQ | ST-05 | 21.4 TB | ALPHA13 HPE Primera |

## Native/local Windows storage

Native/local disks are not part of the shared SAN allocation.

Every physical GDPS server uses:

- C:\ = 200 GB
- D:\ = 300 GB
- 500 GB usable total
- hardware RAID 1 mirrored

Shared clustered business data remains on SAN.

## GDPS mapped LUN baseline

Current values were measured from ALPHA3 production.

| GDPS LUN | Minimum allocated capacity | Current used baseline | Source mapping |
|---|---:|---:|---|
| LUN00 | >= 300 GB | 162.2 GB | RAIDSET00 |
| LUN01 | **>= 600 GB** | **488.2 GB** | RAIDSET01 — source is ~98% full at 500 GB |
| LUN02 | >= 600 GB | 505.4 GB | RAIDSET02 |
| LUN03 | >= 100 GB | 58.6 GB | RAIDSET03 |
| LUN04 | >= 50 GB | 20.3 GB | RAIDSET04 |
| LUN05 | >= 100 GB | 25.7 GB | RAIDSET05 |
| LUN06 | >= 100 GB | 15.2 GB | RAIDSET06 |
| LUN07 | >= 50 GB | 5.6 GB | RAIDSET07 |
| LUN08 | >= 50 GB | 9.0 GB | RAIDSET08 |
| LUN09 | >= 100 GB | 0.1 GB | RAIDSET09 |
| **Total** | **>= 2,050 GB** | **≈ 1,290 GB** | |

LUN01 is deliberately raised above the 500 GB source allocation because RAIDSET01 is approximately 488 GB used and cannot be replaced at essentially full capacity.

## Additional ALPHA3 source volumes requiring disposition

The following source volumes exist on ALPHA3 but were absent from the earlier GDPS LUN map. They shall not be silently omitted.

| Source volume | Allocated | Used | Required disposition |
|---|---:|---:|---|
| T4DATA | 50 GB | 27.8 GB | Carry forward to defined target or approve retirement |
| OPS_DISK | 10 GB | 5.2 GB | Carry forward to defined target or approve retirement |
| CIFS_DATA | 10 GB | 4.7 GB | Carry forward or approve retirement after Windows SMB mapping review |
| CIFS_LOCK | 5 GB | 0.2 GB | Carry forward or approve retirement after Windows SMB mapping review |
| CIFS_LOGS | 50 GB | 22.1 GB | Carry forward or approve retirement after Windows SMB mapping review |
| DATA_COPY | 2,028 GB | 31.8 GB | Carry forward to defined target or approve retirement |
| ADMIN | 50 GB | 33.4 GB | Carry forward to defined target or approve retirement |
| USER | 25 GB | ~0 GB | Carry forward to defined target or approve retirement |
| SCRATCH | 50 GB | 3.2 GB | Carry forward to defined target or approve retirement |
| **Total** | **≈ 2,278 GB** | **≈ 128 GB** | |

ALPHA3SYS is not listed here because its system role moves from SAN to the controlled local Windows C:\ volume.

Final Windows LUN numbering for any retained additional source volumes must be assigned in the controlled storage design after disposition approval.

## Sizing rule

Each controlled GDPS LUN shall be provisioned at or above its minimum. Larger allocations are permitted for growth, storage alignment, protection overhead, or HPE/CDW-G recommendation. Smaller allocations are prohibited without approved architecture change.

## Connectivity

- redundant Fibre Channel fabrics
- redundant HBAs
- Windows MPIO
- WSFC shared-storage support
- zoning and LUN masking per environment/site

## Replication

COOP replication sources, targets, direction, topology, technology, and schedule are to be determined by GPO network engineers.

## Naming rule

RAIDSET00-RAIDSET09 remain source mapping identifiers for migration traceability. GDPS uses Windows/HPE storage objects defined by the approved final storage design.
