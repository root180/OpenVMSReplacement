# GDPS Hardware Replacement Library

This folder is the controlled repository for GDPS hardware replacement architecture, acquisition, storage, network, clustering, migration, and supporting evidence.

## Current acquisition baseline

- **10 physical GDPS servers**
- five separate two-node physical WSFC clusters
- TEST: 2 nodes at HQ
- PROD: 2 nodes at HQ
- DR: 2 nodes at IM
- COOP IM: 2 nodes
- COOP HQ: 2 nodes
- DEV: separate virtual-server replacement

## Per-node native storage

Every physical node:

- C:\ = 200 GB
- D:\ = 300 GB
- 500 GB usable total
- hardware RAID 1 mirrored
- minimum 128 GB RAM

## Shared storage

- ST-01 TEST >=14.4 TB
- ST-02 PROD >=14.4 TB
- ST-03 DR >=14.4 TB
- ST-04 COOP IM >=14.4 TB
- ST-05 COOP HQ >=21.4 TB

Current RAIDSET00-RAIDSET09 used baseline is approximately 1,290 GB. Controlled mapped minimum is >=2,050 GB, including LUN01 >=600 GB. Nine additional ALPHA3 source volumes require explicit disposition.

## Folder structure

- `01 Existing Hardware/` — source Alpha/OpenVMS evidence and verified baseline
- `02 New Acquisition/` — Hardware Master, CDW-G SOW, costing/BOM
- `03 Storage/` — storage architecture and ST-01 through ST-05
- `04 Network/` — network architecture and source addressing anchors
- `05 Cluster and SMB/` — five-cluster WSFC and SMB standards
- `06 Cutover and Migration/` — migration and cutover procedures
- `07 Server Requests/` — authoritative v8 10-server request set
- `08 Diagrams/` — controlled figure register
- `09 Reference and Standards/` — supporting references
- `10 Library Index/` — controlled-document register

## Locked SMB cutover rule

During migration GDPS uses alpha0-1, alpha3-1, and alpha6-1. At authorized cutover the old owner is disabled/released before GDPS assumes alpha0, alpha3, or alpha6. Duplicate ownership of those SMB client-access identities is prohibited anywhere in the GPO enterprise namespace.

## Procurement authority

Use `10 Library Index/CURRENT_CONTROLLED_DOCUMENTS.md` to determine the current implementation and procurement baseline. Older files retained for history are not current acquisition authority.
