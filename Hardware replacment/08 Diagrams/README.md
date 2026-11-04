# GDPS Diagram Register

This folder tracks the controlled architecture figure sets for the hardware replacement library.

## Network figure set - v4 Final

The figure set must represent:

1. Alpha Environment / Network / Recovery Baseline
2. Complete GDPS Enterprise Network Topology
3. GDPS TEST Network
4. GDPS PROD and DR Network
5. GDPS COOP IM Recovery Network
6. GDPS COOP HQ Recovery Network
7. SMB Namespace Migration and Cutover

## Storage figure set - v3 Minimum Capacity

The figure set must represent:

1. GDPS System Environment - Storage Roles
2. GDPS Storage Topology
3. GDPS Storage Architecture and LUN Configuration
4. Separate COOP storage targets: IM >=14.4 TB and HQ >=21.4 TB

## Diagram controls

- physical-server count: **10**
- five separate two-node WSFC clusters
- ST-01 through ST-05
- GDPS controlled mapped LUN minimum: >=2,050 GB
- current RAIDSET00-RAIDSET09 used baseline: ≈1,290 GB
- RAIDSET names appear only as source-mapping references
- storage capacities shown for GDPS are minimum sizing floors unless explicitly stated otherwise
- architecture figures use clean, flat infrastructure styling without shadows
