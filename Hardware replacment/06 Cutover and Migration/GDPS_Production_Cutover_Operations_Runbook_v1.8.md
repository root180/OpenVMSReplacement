# GDPS Production Cutover Operations Runbook v1.8

## Pre-cutover gates

Before production cutover:

- TEST rehearsal completed
- PROD cluster healthy
- File Share Witness healthy
- redundant FC/MPIO paths validated
- LUN00-LUN09 healthy and at or above minimum capacities
- final data synchronization completed
- SMB identity ownership plan approved
- rollback authority identified

## Cutover sequence

1. Freeze writes on the current production owner.
2. Complete final delta synchronization and reconciliation.
3. Disable current SMB publication.
4. Release DNS, NetBIOS, AD computer object/SPN, cluster/service registrations as applicable.
5. Prove the old owner is absent GPO-wide.
6. Activate the GDPS clustered SMB identity using the original application-facing name.
7. Register final DNS/authentication identity.
8. Validate unchanged UNC paths.
9. Validate critical application workflows.
10. Authorize GDPS writes.
11. Begin stabilization monitoring.

## Storage readiness

No destination LUN may be smaller than its controlled minimum.

## Rollback

Before GDPS authoritative writes, rollback may restore the previous owner after GDPS identity is disabled and proven absent.

After GDPS authoritative writes, data reconciliation is required before any reverse cutover.
