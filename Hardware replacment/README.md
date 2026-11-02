# GDPS Hardware Replacement Library

This folder is the controlled repository for GDPS hardware replacement architecture, acquisition, storage, network, clustering, migration, and supporting evidence.

## Folder structure

- `01 Existing Hardware/` — current Alpha/OpenVMS hardware, storage, DCIAC, and operational evidence.
- `02 New Acquisition/` — GDPS Hardware Master, CDW-G SOW, costing/BOM, and procurement artifacts.
- `03 Storage/` — HPE Windows/WSFC storage architecture, LUN sizing, FC/MPIO, and replication.
- `04 Network/` — GDPS network architecture, addressing, firewall boundaries, and network figures.
- `05 Cluster and SMB/` — WSFC, File Share Witness, SMB namespace, and service-identity standards.
- `06 Cutover and Migration/` — migration plans, production cutover runbooks, rollback, and recovery procedures.
- `07 Server Requests/` — physical server provisioning request forms.
- `08 Diagrams/` — controlled network and storage figures.
- `09 Reference and Standards/` — supporting security, architecture, procurement, and operational references.
- `10 Library Index/` — controlled-document register, version index, and superseded-history tracking.

## Locked storage rule

LUN00-LUN09 capacities are minimum sizing floors. They may be provisioned larger but never smaller than their controlled minimums. Current used-space values remain the migration baseline.

## Locked SMB cutover rule

During migration GDPS uses alpha0-1, alpha3-1, and alpha6-1. At authorized cutover the old owner is disabled/released before GDPS assumes alpha0, alpha3, or alpha6. Duplicate ownership of those SMB client-access identities is prohibited anywhere in the GPO enterprise namespace.
