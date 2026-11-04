# Cluster and SMB

Current controlled artifact:

- GDPS Windows File Cluster and SMB Namespace Standard v1.8

Track:

- five separate two-node WSFC clusters: TEST, PROD, DR, COOP IM, COOP HQ
- 10 physical WSFC nodes total
- independent File Share Witness on a third system for each cluster
- HPE shared storage presented through redundant FC paths
- non-overlapping peer-node patch windows
- DR/COOP maintenance separated from PROD
- SMB service identities
- temporary migration names: alpha0-1, alpha3-1, alpha6-1
- final application-facing names: alpha0, alpha3, alpha6
- GPO-wide single-owner rule
