# GDPS Windows File Cluster and SMB Namespace Standard v1.8

## WSFC baseline

TEST, PROD, DR, and COOP are separate two-node Windows Server Failover Clusters.

Each cluster requires:

- two physical nodes
- independent File Share Witness
- HPE enterprise storage for Windows Server / WSFC
- redundant Fibre Channel
- Windows MPIO
- cluster-aware SMB service identities

## SMB staging identities

While Alpha remains active:

- DEV staging identity: alpha0-1
- PROD staging identity: alpha3-1
- DR staging identity: alpha6-1

These are temporary migration/client-access identities, not permanent application UNC names.

## Final SMB identities

After controlled cutover, GDPS assumes the existing application-facing identities:

- alpha0
- alpha3
- alpha6

## Enterprise single-owner rule

At no time may two hosts, clusters, aliases, or service endpoints anywhere in the GPO enterprise namespace simultaneously advertise, register, resolve, or authenticate as the same alpha0, alpha3, or alpha6 SMB client-access identity.

## Witness rule

The File Share Witness contains quorum metadata only and must not reside on clustered GDPS business-data storage.
