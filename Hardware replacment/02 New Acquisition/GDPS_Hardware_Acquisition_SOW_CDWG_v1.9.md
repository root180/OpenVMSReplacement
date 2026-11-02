# GDPS Hardware Acquisition SOW - CDW-G v1.9

## Objective

Provide an engineered bill of materials and implementation-ready hardware configuration for the GDPS replacement platform.

## Required physical infrastructure

- 8 physical Windows Server / WSFC nodes
- Minimum 128 GB RAM per node
- Redundant Fibre Channel connectivity
- Redundant FC fabrics
- Windows MPIO
- Independent File Share Witness capability for TEST, PROD, DR, and COOP

## Storage requirements

HPE is the preferred enterprise storage vendor based on current GPO storage lineage and procurement path.

Exact storage model and array protection policy are **TBD by HPE/CDW-G engineering**.

Minimum usable capacity:

| Environment | Minimum Usable Capacity |
|---|---:|
| TEST | 14.4 TB |
| PROD | 14.4 TB |
| DR | 14.4 TB |
| COOP | 21.4 TB |

## LUN requirements

The engineered storage design shall present GDPS LUN00-LUN09.

Each documented LUN capacity is a **minimum sizing floor**. A LUN may be larger, but no mapped LUN may be smaller than its documented minimum.

## Replication

The solution shall support:

- PROD -> DR replication / production backup
- PROD -> COOP recovery replication

## Vendor response requirements

CDW-G/HPE shall identify:

- exact server SKU and configuration
- exact HPE storage model
- controller configuration
- array protection policy
- FC switch / fabric requirements
- optics and cabling
- MPIO requirements
- replication technology and licensing
- support and professional services
- any larger recommended LUN or array sizing

No silent substitution of virtual servers for required physical nodes is permitted.
