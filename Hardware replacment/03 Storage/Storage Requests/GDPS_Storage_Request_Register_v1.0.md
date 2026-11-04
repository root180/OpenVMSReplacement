# GDPS Storage Request Register v1.0

| Request | Environment / site | Minimum usable capacity | Connected nodes | Existing parity |
|---|---|---:|---|---|
| ST-01 | TEST / HQ | >= 14.4 TB | HQGIPSDPSFST1, HQGIPSDPSFST2 | Production-equivalent |
| ST-02 | PROD / HQ | >= 14.4 TB | HQGIPSDPSFSP1, HQGIPSDPSFSP2 | ALPHA3 / HPE 3PAR |
| ST-03 | DR / IM | >= 14.4 TB | IMGIPSDPSFSD1, IMGIPSDPSFSD2 | ALPHA6 / HPE 3PAR |
| ST-04 | COOP / IM | >= 14.4 TB | IMGIPSDPSFSC1, IMGIPSDPSFSC2 | ALPHA10 / HPE 3PAR |
| ST-05 | COOP / HQ | >= 21.4 TB | HQGIPSDPSFSC3, HQGIPSDPSFSC4 | ALPHA13 / HPE Primera |

DEV does not require a new SAN acquisition request; it uses the existing GPO Enterprise NAS with a minimum 2 TB allocation.

## Controlled storage baseline

- Current RAIDSET00-RAIDSET09 used baseline: **≈ 1,290 GB**
- Controlled minimum mapped allocation after LUN01 headroom increase: **>= 2,050 GB**
- LUN01 minimum: **>= 600 GB**
- Nine additional ALPHA3 source volumes, approximately 2.3 TB allocated / 128 GB used, require explicit carry-forward or approved-retirement disposition.

## Capacity rule

Environment capacities and controlled LUN minimums are floors. Larger is permitted; smaller is prohibited without approved architecture change.
