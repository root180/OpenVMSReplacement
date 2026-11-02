# Alpha Hardware and Storage Baseline

## Purpose

This document records the current Alpha/OpenVMS hardware and storage baseline that the GDPS replacement must preserve functionally.

## Environment topology

| Environment | Nodes | Site | Storage |
|---|---:|---|---|
| Alpha0 DEV | ALPHA1, ALPHA2 | HQ | HPE 3PAR 7200 |
| Alpha3 PROD | N3A, N3B | HQ | HPE 3PAR 8200 |
| Alpha6 Production Backup / DR | N6A, N6B | IM | HPE 3PAR 8200 |
| Alpha10 DCIAC02 | ALPHA11, ALPHA12 | Recovery | HPE 3PAR 8200 |
| Alpha13 DCIAC03 / CRATE | N13A, N13B | Recovery | HPE Primera |

## Storage platform capacities

- Alpha3 / PROD array baseline: **14.4 TB**
- Alpha13 / COOP / CRATE array baseline: **21.4 TB**

## Mapped logical volumes

| Source Volume | Used Baseline | Allocated Capacity |
|---|---:|---:|
| RAIDSET00 | 150 GB | 300 GB |
| RAIDSET01 | 400 GB | 500 GB |
| RAIDSET02 | 485 GB | 600 GB |
| RAIDSET03 | 50 GB | 100 GB |
| RAIDSET04 | 20 GB | 50 GB |
| RAIDSET05 | 20 GB | 100 GB |
| RAIDSET06 | 60 GB | 100 GB |
| RAIDSET07 | 5 GB | 50 GB |
| RAIDSET08 | 10 GB | 50 GB |
| RAIDSET09 | 5 GB | 100 GB |
| **Total** | **1,205 GB** | **1,950 GB** |

## Replacement rule

GDPS may increase capacity but must not reduce any mapped logical volume below the corresponding Alpha allocation. Current used-space values remain the migration baseline.

## Architecture principle

POLLVAX remains the business-behavior authority. The replacement is a technology port and must not redesign business rules.
