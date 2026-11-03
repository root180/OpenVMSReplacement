# Alpha Hardware and Storage Baseline

## Purpose

This document records the verified Alpha/OpenVMS hardware, network, and storage baseline used to size and trace the GDPS hardware replacement.

## Environment topology

| Alpha system | Role | Physical nodes | Source hardware | Site | Shared storage |
|---|---|---|---|---|---|
| ALPHA0 | DEV | ALPHA1, ALPHA2 | HPE Integrity i2 | **IMDC** | HPE 3PAR, 14.4 TB class |
| ALPHA3 | PROD | N3A, N3B | HPE Integrity i6 | HQ | HPE 3PAR, 14.4 TB |
| ALPHA6 | Production Backup / DR | N6A, N6B | HPE Integrity i6 | IM | HPE 3PAR, 14.4 TB |
| ALPHA10 | COOP / DCIAC02 | ALPHA11, ALPHA12 | HPE Integrity i6 | DCIAC02 | HPE 3PAR, 14.4 TB |
| ALPHA13 | COOP / DCIAC03 | two physical nodes; individual node names pending confirmation | HPE Integrity i6 | DCIAC03 | HPE Primera, 21.4 TB |

ALPHA0 is replaced separately by the GDPS DEV virtual-server design and is not part of the 10 physical-server request set.

## ALPHA3 node-local/system sizing evidence

### System role

- `ALPHA3SYS`: approximately **200 GB**
- approximately **118 GB used**
- OpenVMS/system software role
- on GDPS this role moves to local **C:\ 200 GB**

### N3B local disk

- device: `$59$DKA0:`
- label: `N3B_PAGE`
- HP logical volume on the server's hardware storage controller
- approximately **300 GB**
- paging/local-node role
- on GDPS this role maps to local **D:\ 300 GB**

Controlled GDPS native/local standard per physical node: **C:\ 200 GB + D:\ 300 GB = 500 GB usable, hardware RAID 1 mirrored**.

## Current ALPHA3 RAIDSET usage

The older August 2025 1,205 GB used baseline is superseded by current production measurements.

| Source volume | Current used | Source allocation |
|---|---:|---:|
| RAIDSET00 | 162.2 GB | 300 GB |
| RAIDSET01 | 488.2 GB | 500 GB |
| RAIDSET02 | 505.4 GB | 600 GB |
| RAIDSET03 | 58.6 GB | 100 GB |
| RAIDSET04 | 20.3 GB | 50 GB |
| RAIDSET05 | 25.7 GB | 100 GB |
| RAIDSET06 | 15.2 GB | 50 GB source allocation |
| RAIDSET07 | 5.6 GB | 100 GB source allocation |
| RAIDSET08 | 9.0 GB | 50 GB source allocation |
| RAIDSET09 | 0.1 GB | 100 GB source allocation |
| **Total used** | **≈ 1,290 GB** | |

RAIDSET01 is approximately 98% full. The GDPS replacement minimum for its mapped LUN is therefore raised to **600 GB**.

## Additional ALPHA3 volumes

These source volumes also exist and require explicit carry-forward or approved-retirement decisions:

| Source volume | Allocated | Used |
|---|---:|---:|
| T4DATA | 50 GB | 27.8 GB |
| OPS_DISK | 10 GB | 5.2 GB |
| CIFS_DATA | 10 GB | 4.7 GB |
| CIFS_LOCK | 5 GB | 0.2 GB |
| CIFS_LOGS | 50 GB | 22.1 GB |
| DATA_COPY | 2,028 GB | 31.8 GB |
| ADMIN | 50 GB | 33.4 GB |
| USER | 25 GB | ~0 GB |
| SCRATCH | 50 GB | 3.2 GB |
| **Total** | **≈ 2,278 GB** | **≈ 128 GB** |

The CIFS volumes require specific disposition review against native Windows SMB. They must not be silently dropped.

## Network traceability

- ALPHA3 / N3A: 172.16.35.15, .16
- ALPHA3 / N3B: 172.16.35.19 (IE2 primary), .20 (IE3)
- ALPHA3 subnet mask: 255.255.255.0 (/24)
- ALPHA6 cluster DNS set: 172.19.128.41-.44
- ALPHA10: ALPHA11 .42/.43; ALPHA12 .44/.45 on 172.23.5.x
- ALPHA13 cluster DNS set: 172.23.6.42-.45; node split pending confirmation

## Replacement rule

The GDPS replacement preserves the existing physical/recovery capability while modernizing the platform. Capacity may increase. Controlled minimum server count, site placement, native-disk sizing, shared-storage capacity, and required source-volume disposition must not be reduced without an approved architecture change.
