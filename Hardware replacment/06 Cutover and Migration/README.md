# Cutover and Migration

Current controlled artifacts:
- GDPS Production Cutover Operations Runbook v1.8
- GDPS SMB Namespace Migration and Cutover Plan v1.3

Core cutover sequence:
1. Freeze writes.
2. Complete final synchronization.
3. Disable/release the existing SMB identity.
4. Verify the old owner is absent GPO-wide.
5. Activate the GDPS final identity.
6. Register/validate DNS and authentication identity.
7. Validate original UNC paths.
8. Validate application workflows.
9. Authorize GDPS writes.

Existing applications continue to use the original UNC paths after cutover.
