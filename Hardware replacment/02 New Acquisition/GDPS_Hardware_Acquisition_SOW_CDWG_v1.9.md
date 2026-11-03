# GDPS Hardware Acquisition SOW - CDW-G v1.9

## Objective

Provide an engineered bill of materials and implementation-ready hardware configuration for the GDPS replacement platform.

## Required physical infrastructure

- **10 physical Windows Server / WSFC nodes**
- 2 TEST nodes at HQ
- 2 PROD nodes at HQ
- 2 DR nodes at IM
- 2 COOP nodes at DCIAC02
- 2 COOP nodes at DCIAC03
- minimum 128 GB RAM per node
- per-node native/local storage: **C:\ 200 GB + D:\ 300 GB = 500 GB usable, hardware RAID 1 mirrored**
- redundant Fibre Channel HBAs per node
- two independent FC fabrics for each storage-connected cluster
- Windows MPIO
- independent third-system File Share Witness capability for each of the five two-node clusters

No silent substitution of virtual servers for required physical nodes is permitted.

## Storage requirements

HPE is the preferred enterprise storage vendor based on current GPO storage lineage and procurement path. Exact replacement storage model and array protection policy remain subject to HPE/CDW-G engineering, but the controlled minimum usable capacities may not be reduced.

| Environment / site | Storage request | Minimum usable capacity | Existing parity |
|---|---|---:|---|
| TEST / HQ | ST-01 | 14.4 TB | Production-equivalent |
| PROD / HQ | ST-02 | 14.4 TB | ALPHA3 3PAR |
| DR / IM | ST-03 | 14.4 TB | ALPHA6 3PAR |
| COOP / DCIAC02 | ST-04 | 14.4 TB | ALPHA10 3PAR |
| COOP / DCIAC03 | ST-05 | 21.4 TB | ALPHA13 Primera |

## Native/local disk requirement

Every physical server shall be quoted with:

- **C:\ = 200 GB usable**
- **D:\ = 300 GB usable**
- **500 GB usable total**
- hardware **RAID 1 mirrored**

This is the controlled Windows replacement of the ALPHA3 sizing basis: 200 GB system role plus 300 GB local role. Shared clustered business data remains on SAN.

## LUN and source-volume requirements

The engineered storage design shall preserve the required Alpha business-data functions without silently omitting source volumes.

RAIDSET00-RAIDSET09 remain the controlled mapped baseline. Current measured use across those ten source volumes is approximately **1,290 GB**.

**RAIDSET01 is approximately 488 GB used on a 500 GB source allocation and is approximately 98% full. Its replacement minimum shall be increased above 500 GB; the controlled planning floor is 600 GB unless HPE/CDW-G recommends a larger value.**

The following additional ALPHA3 source volumes also require an explicit migration disposition before final LUN presentation is approved:

- T4DATA
- OPS_DISK
- CIFS_DATA
- CIFS_LOCK
- CIFS_LOGS
- DATA_COPY
- ADMIN
- USER
- SCRATCH

Each shall be marked either **carry forward to a defined Windows/SAN target** or **retire with approved rationale**. They shall not be silently omitted from engineering.

ALPHA3SYS is not a shared-data carry-forward LUN because its system role moves to the controlled local Windows C:\ volume.

## Replication

The solution shall support:

- PROD -> DR
- PROD -> COOP DCIAC02
- PROD -> COOP DCIAC03

DR and both COOP targets must remain independently recoverable.

## Vendor response requirements

CDW-G/HPE shall identify:

- exact server SKU/configuration for all 10 physical nodes
- local RAID/controller configuration supporting C:\ 200 GB and D:\ 300 GB usable
- exact HPE storage model for each environment/site
- controller and array protection policy
- FC switch/fabric requirements including DCIAC03
- HBA count and models for all 10 nodes
- optics and cabling
- MPIO requirements
- replication technology and licensing
- support and professional services
- crate integration for DCIAC02 and DCIAC03
- recommended replacement LUN sizing, including growth headroom for RAIDSET01
- disposition mapping for the nine additional ALPHA3 source volumes

No reduction below the controlled server count, site count, native disk layout, or storage-capacity floors is permitted without an approved architecture change.
