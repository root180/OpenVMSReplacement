# Storage

Current controlled storage artifact:
- GDPS Storage Architecture and LUN Design v1.1

Architecture:
- HPE enterprise storage for Windows Server / WSFC
- TEST / PROD / DR: >= 14.4 TB usable minimum
- COOP: >= 21.4 TB usable minimum
- DEV: existing GPO Enterprise NAS, >= 2 TB allocation
- Redundant Fibre Channel fabrics and MPIO
- PROD -> DR replication
- PROD -> COOP recovery replication

LUN rule:
- GDPS storage objects are LUN00-LUN09
- Minimum mapped allocation: 1,950 GB
- Current used baseline: 1,205 GB
- Baseline free: 745 GB
- Source RAIDSET00-RAIDSET09 values remain in the same mapping table for traceability only
- Any LUN may be larger than its documented minimum; none may be smaller
