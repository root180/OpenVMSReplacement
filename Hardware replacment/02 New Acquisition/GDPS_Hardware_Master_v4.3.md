# GDPS Hardware Master v4.3

## Controlled baseline

This document defines the current GDPS hardware replacement topology and is synchronized to the v8 physical-server request set.

## Environment model

| Environment | Server Count | Server Names | Site | Source Alpha capability |
|---|---:|---|---|---|
| DEV | 0 physical | Virtual GDPS DEV servers | Existing GPO virtualization | ALPHA0; separate virtual replacement |
| TEST | 2 | HQVMGDPSFST1, HQVMGDPSFST2 | HQ | New TEST cluster based on production two-node pattern |
| PROD | 2 | HQVMGDPSFSP1, HQVMGDPSFSP2 | HQ | ALPHA3 / N3A + N3B |
| DR | 2 | IMVMGDPSFSD1, IMVMGDPSFSD2 | IM | ALPHA6 / N6A + N6B |
| COOP DCIAC02 | 2 | IMVMGDPSFSC1, IMVMGDPSFSC2 | DCIAC02 / CRATE | ALPHA10 / ALPHA11 + ALPHA12 |
| COOP DCIAC03 | 2 | IMVMGDPSFSC3, IMVMGDPSFSC4 | DCIAC03 / CRATE | ALPHA13 / two physical nodes |

**Physical server total: 10.**

## Physical node baseline

Every physical GDPS node requires:

- Windows Server 2025 capable hardware
- minimum **128 GB RAM**
- native/local storage: **C:\ = 200 GB + D:\ = 300 GB**
- **500 GB usable total native/local storage, hardware RAID 1 mirrored**
- redundant hot-plug power
- redundant Server Distribution network connectivity
- redundant Fibre Channel HBAs to two independent fabrics
- Windows MPIO
- WSFC support
- production-grade enterprise support

The native disk sizes match the ALPHA3 production sizing basis one-to-one: 200 GB system role plus 300 GB local role. Shared clustered business data remains on SAN.

## Cluster model

There are **five two-node physical WSFC clusters**:

1. TEST — HQ
2. PROD — HQ
3. DR — IM
4. COOP DCIAC02
5. COOP DCIAC03

Each cluster requires an independent File Share Witness located on a third independent system, not on either peer node and not on that cluster's own shared data storage.

## Storage

| Environment | Storage request | Minimum usable capacity | Existing parity |
|---|---|---:|---|
| DEV | Existing NAS | >= 2 TB | Existing GPO enterprise NAS |
| TEST | ST-01 | >= 14.4 TB | Production-equivalent HPE enterprise storage |
| PROD | ST-02 | >= 14.4 TB | ALPHA3 HPE 3PAR |
| DR | ST-03 | >= 14.4 TB | ALPHA6 HPE 3PAR |
| COOP DCIAC02 | ST-04 | >= 14.4 TB | ALPHA10 HPE 3PAR |
| COOP DCIAC03 | ST-05 | >= 21.4 TB | ALPHA13 HPE Primera |

## Existing Alpha hardware anchors

- ALPHA0: HPE Integrity i2, 2 nodes; DEV; separate virtual replacement.
- ALPHA3: HPE Integrity i6, 2 nodes; HQ; HPE 3PAR 14.4 TB.
- ALPHA6: HPE Integrity i6, 2 nodes; IM; HPE 3PAR 14.4 TB.
- ALPHA10: HPE Integrity i6, 2 nodes; DCIAC02 COOP; HPE 3PAR 14.4 TB.
- ALPHA13: HPE Integrity i6, 2 nodes; DCIAC03 COOP; HPE Primera 21.4 TB.

ALPHA13 individual node names remain subject to confirmation from the source system; the physical two-node ALPHA13 replacement relationship is controlled.

## Recovery

- PROD -> DR
- PROD -> COOP DCIAC02
- PROD -> COOP DCIAC03
- TEST rehearses production-equivalent clustering and recovery behavior with TEST data and identities.

## SMB migration identities

During migration:

- alpha0-1
- alpha3-1
- alpha6-1

Final application-facing names remain alpha0, alpha3, and alpha6 after controlled ownership transfer.

## Hard rule

At no time may two hosts, clusters, aliases, or service endpoints anywhere in the GPO enterprise namespace simultaneously advertise, register, resolve, or authenticate as the same alpha0, alpha3, or alpha6 SMB client-access identity.
