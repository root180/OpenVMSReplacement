# Storage

Current controlled storage artifact:

- GDPS Storage Architecture and LUN Design v1.1

## Environment storage

- TEST / ST-01: >= 14.4 TB usable
- PROD / ST-02: >= 14.4 TB usable
- DR / ST-03: >= 14.4 TB usable
- COOP DCIAC02 / ST-04: >= 14.4 TB usable
- COOP DCIAC03 / ST-05: >= 21.4 TB usable
- DEV: existing GPO Enterprise NAS, >= 2 TB allocation

All physical storage environments require redundant Fibre Channel fabrics and Windows MPIO.

## Replication

- PROD -> DR
- PROD -> COOP DCIAC02
- PROD -> COOP DCIAC03

## LUN rule

- Current RAIDSET00-RAIDSET09 used baseline: **≈ 1,290 GB**
- Controlled minimum mapped allocation: **>= 2,050 GB**
- LUN01 minimum is **>= 600 GB** because the source 500 GB RAIDSET01 is approximately 488 GB used (~98% full)
- Larger is permitted; smaller is prohibited
- Nine additional ALPHA3 source volumes require explicit carry-forward or approved-retirement disposition before final storage presentation
