# Cluster and SMB

Current controlled artifact:
- GDPS Windows File Cluster and SMB Namespace Standard v1.8

Track:
- two-node WSFC design for TEST / PROD / DR / COOP
- independent File Share Witness for each cluster
- HPE shared storage presented through redundant FC paths
- SMB service identities
- temporary migration names: alpha0-1, alpha3-1, alpha6-1
- final application-facing names: alpha0, alpha3, alpha6
- GPO-wide single-owner rule
