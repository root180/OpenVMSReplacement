# GDPS Hardware Master v4.3

## Controlled baseline

This document defines the current GDPS hardware replacement topology.

## Environment model

| Environment | Server Count | Server Names | Site |
|---|---:|---|---|
| DEV | 0 physical | 4 VMs on existing GPO virtualization | HQ |
| TEST | 2 | HQVMGDPSFST1, HQVMGDPSFST2 | HQ |
| PROD | 2 | HQVMGDPSFSP1, HQVMGDPSFSP2 | HQ |
| DR | 2 | IMVMGDPSFSD1, IMVMGDPSFSD2 | IM |
| COOP | 2 | IMVMGDPSFSC1, IMVMGDPSFSC2 | DCIAC / CRATE |

**Physical server total: 8.**

## Physical node baseline

- Windows Server 2025 capable
- Minimum **128 GB RAM per physical node**
- Redundant network interfaces
- Redundant Fibre Channel HBAs
- Windows MPIO
- WSFC-compatible
- Production-grade enterprise support

## Cluster model

TEST, PROD, DR, and COOP are separate two-node WSFC clusters.

Each cluster requires an independent File Share Witness containing quorum metadata only.

## Storage

- DEV: existing GPO Enterprise NAS, **>= 2 TB**
- TEST: HPE Enterprise Storage for Windows Server / WSFC, **>= 14.4 TB usable**
- PROD: HPE Enterprise Storage for Windows Server / WSFC, **>= 14.4 TB usable**
- DR: HPE Enterprise Storage for Windows Server / WSFC, **>= 14.4 TB usable**
- COOP: HPE Enterprise Recovery Storage for Windows Server / WSFC, **>= 21.4 TB usable**

## Recovery

- PROD -> DR
- PROD -> COOP
- TEST rehearses production-equivalent recovery behavior with TEST data and identities.

## SMB migration identities

During migration:

- alpha0-1
- alpha3-1
- alpha6-1

Final application-facing names remain alpha0, alpha3, and alpha6 after controlled ownership transfer.

## Hard rule

At no time may two hosts, clusters, aliases, or service endpoints anywhere in the GPO enterprise namespace simultaneously advertise, register, resolve, or authenticate as the same alpha0, alpha3, or alpha6 SMB client-access identity.
