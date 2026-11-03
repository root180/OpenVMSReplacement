# GDPS CDW-G Costing and Acquisition List v11

## Planning baseline

| Environment / site | Physical Servers | Storage Requirement |
|---|---:|---|
| DEV | 0 | Existing GPO Enterprise NAS >= 2 TB |
| TEST / HQ | 2 | HPE Windows/WSFC storage >= 14.4 TB usable |
| PROD / HQ | 2 | HPE Windows/WSFC storage >= 14.4 TB usable |
| DR / IM | 2 | HPE Windows/WSFC storage >= 14.4 TB usable |
| COOP / DCIAC02 | 2 | HPE recovery storage >= 14.4 TB usable |
| COOP / DCIAC03 | 2 | HPE recovery storage >= 21.4 TB usable |

**Physical server total: 10.**

## Per-server controlled configuration

Each of the 10 physical servers must include:

- minimum 128 GB RAM
- Windows Server 2025 capability
- **C:\ 200 GB + D:\ 300 GB = 500 GB usable native/local storage**
- hardware RAID 1 mirrored local storage
- redundant network interfaces
- redundant FC HBAs
- enterprise support

## Public-price planning references

Previous public-price planning references remain useful only as unit-price placeholders:

- server baseline: approximately $17,156.99 each
- FC switch baseline: approximately $34,236.19 each
- FC HBA baseline: approximately $7,947.07 each
- Windows 16-core license planning baseline: approximately $774.05

The prior **$569,260.40 subtotal was based on eight physical servers and is superseded**. Do not use that subtotal for acquisition approval.

The revised quote must price:

- 10 physical servers, not 8
- HBAs for all 10 physical nodes
- DCIAC03 FC/fabric connectivity in addition to DCIAC02
- five storage targets/allocations: TEST, PROD, DR, DCIAC02 COOP, DCIAC03 COOP
- replication to DR, DCIAC02, and DCIAC03
- required optics/cabling
- licensing
- support
- installation/professional services
- both DCIAC recovery environments

## Storage requests

| Request | Purpose | Minimum usable |
|---|---|---:|
| ST-01 | TEST | 14.4 TB |
| ST-02 | PROD | 14.4 TB |
| ST-03 | DR | 14.4 TB |
| ST-04 | COOP DCIAC02 | 14.4 TB |
| ST-05 | COOP DCIAC03 | 21.4 TB |

## LUN sizing control

Current measured usage across RAIDSET00-RAIDSET09 is approximately **1,290 GB**, not the older 1,205 GB figure.

RAIDSET01 is approximately **488 GB used on a 500 GB allocation**. Its replacement planning floor is **600 GB**, with a larger HPE/CDW-G recommendation permitted.

Nine additional ALPHA3 source volumes require explicit carry-forward or retirement decisions before final storage BOM approval: T4DATA, OPS_DISK, CIFS_DATA, CIFS_LOCK, CIFS_LOGS, DATA_COPY, ADMIN, USER, and SCRATCH.

## Procurement control

Exact HPE storage family, RAID/protection implementation, controller design, replication technology, and support configuration remain subject to HPE/CDW-G engineering validation. No quote based on eight physical servers is current.
