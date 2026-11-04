# Current Controlled Hardware Library

| Folder | Controlled artifact | Current version / baseline |
|---|---|---|
| 02 New Acquisition | GDPS_Hardware_Master_v4.3.md | v4.3 — synchronized to 10 physical servers |
| 02 New Acquisition | GDPS_Hardware_Acquisition_SOW_CDWG_v1.9.md | v1.9 — synchronized to 10 physical servers |
| 02 New Acquisition | GDPS_CDWG_Costing_and_Acquisition_List_v11.md | v11 — ten-server acquisition baseline |
| 02 New Acquisition | GDPS_Memory_RAM_Requirement_Justification_v1.0.md | v1.0 — 128 GB per physical node justification |
| 03 Storage | GDPS_Storage_Architecture_and_LUN_Design_v1.1.md | v1.1 — current Alpha3 baseline |
| 03 Storage / Storage Requests | ST-01 through ST-05 | Five controlled storage requests |
| 04 Network | GDPS_Network_Infrastructure_and_Addressing_Design_v1.5.md | v1.5 — confirmed source anchors |
| 05 Cluster and SMB | GDPS_Windows_File_Cluster_and_SMB_Namespace_Standard_v1.8.md | v1.8 — five two-node clusters |
| 06 Cutover and Migration | GDPS Production Cutover Operations Runbook | v1.8 — unchanged |
| 06 Cutover and Migration | GDPS SMB Namespace Migration and Cutover Plan | v1.3 — unchanged |
| 07 Server Requests | v8 10-Node Physical Server Tickets | **v8 — 10 server request forms** |
| 08 Diagrams | GDPS Diagram Register | current register requires two COOP sites |
| 10 Library Index | GDPS_Hardware_Library_Tracking_Index_v1.0.md | v1.0 |

## Authoritative physical-server baseline

- TEST: 2
- PROD: 2
- DR: 2
- COOP IM: 2
- COOP HQ: 2
- **Total physical servers: 10**

DEV is a separate virtual-server replacement and is not part of the physical acquisition count.

## Authoritative storage baseline

- ST-01 TEST: >=14.4 TB
- ST-02 PROD: >=14.4 TB
- ST-03 DR: >=14.4 TB
- ST-04 COOP IM: >=14.4 TB
- ST-05 COOP HQ: >=21.4 TB
- current RAIDSET00-RAIDSET09 used baseline: ≈1,290 GB
- controlled mapped minimum: >=2,050 GB
- LUN01 minimum: >=600 GB
- nine additional ALPHA3 source volumes require explicit disposition

## Native physical-server storage

Every physical node:

- C:\ = 200 GB
- D:\ = 300 GB
- 500 GB usable total
- hardware RAID 1 mirrored

## Existing-hardware evidence to retain

- ALPHA Systems Storage Information (08AUG2025).pptx
- COOP2026_Senatechecklist_draft2.docx
- May 2026_InternalDryRun_Checklist.docx

## Reference and standards material to retain

- 040ADV-25-C-0020 HPE Servers.pdf
- APDMS_Security_Design_Document_SDD_v1.0(1).docx
- Alpha_APDMS_Architecture_Principles_Standards_and_Guardrails_v1.1(1).docx

## Implementation rule

Use the versions and baselines identified above for procurement, implementation, and new server/storage requests.
