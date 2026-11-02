# GDPS CDW-G Costing and Acquisition List v11

## Planning baseline

| Environment | Physical Servers | Storage Requirement |
|---|---:|---|
| DEV | 0 | Existing GPO Enterprise NAS >= 2 TB |
| TEST | 2 | HPE Windows/WSFC storage >= 14.4 TB usable |
| PROD | 2 | HPE Windows/WSFC storage >= 14.4 TB usable |
| DR | 2 | HPE Windows/WSFC storage >= 14.4 TB usable |
| COOP | 2 | HPE Windows/WSFC recovery storage >= 21.4 TB usable |

**Physical server total: 8.**

## Public-price planning references

- Server baseline: approximately $17,156.99 each
- FC switch baseline: approximately $34,236.19 each
- FC HBA baseline: approximately $7,947.07 each
- Windows 16-core license planning baseline: approximately $774.05
- Known-priced planning subtotal before storage/support/services: approximately **$569,260.40**

## Quote-required items

- HPE enterprise storage arrays
- replication licensing
- support
- optics/cabling
- installation and professional services
- crate integration for COOP

## LUN sizing rule

LUN00-LUN09 capacities are minimum sizing floors. HPE/CDW-G may recommend larger LUN or array capacity, but no mapped LUN may be quoted or provisioned below its controlled minimum.

Minimum mapped allocation: **1,950 GB**

Current used-data baseline: **1,205 GB**

Baseline free capacity: **745 GB**

## Procurement control

Exact HPE storage family, RAID/protection implementation, controller design, replication technology, and support configuration remain subject to HPE/CDW-G engineering validation.
