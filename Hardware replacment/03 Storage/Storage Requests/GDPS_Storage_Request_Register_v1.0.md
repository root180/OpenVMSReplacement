# GDPS Storage Request Register v1.0

| Request | Environment | Site | Minimum Usable Capacity | Connected Nodes |
|---|---|---|---:|---|
| ST-01 | TEST | HQ | >= 14.4 TB | HQVMGDPSFST1, HQVMGDPSFST2 |
| ST-02 | PROD | HQ | >= 14.4 TB | HQVMGDPSFSP1, HQVMGDPSFSP2 |
| ST-03 | DR | IM | >= 14.4 TB | IMVMGDPSFSD1, IMVMGDPSFSD2 |
| ST-04 | COOP / DCIAC | IM / CRATE | >= 21.4 TB | IMVMGDPSFSC1, IMVMGDPSFSC2 |

DEV does not require a new SAN/storage acquisition request; it uses the existing GPO Enterprise NAS with a minimum 2 TB allocation.

## Locked capacity rule

All environment capacities and LUN00-LUN09 capacities are minimum sizing floors. Larger is permitted; smaller is prohibited.

Current used-space baseline across the mapped LUNs: **1,205 GB**.

Minimum mapped LUN allocation: **1,950 GB**.
