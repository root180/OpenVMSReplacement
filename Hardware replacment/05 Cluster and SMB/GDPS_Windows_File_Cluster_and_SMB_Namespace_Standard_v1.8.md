# GDPS Windows File Cluster and SMB Namespace Standard v1.8

## WSFC baseline

TEST, PROD, DR, COOP IM, and COOP HQ are five separate two-node Windows Server Failover Clusters. Total physical WSFC nodes: **10**.

Cluster pairs are:

- TEST: HQGIPSDPSFST1 + HQGIPSDPSFST2 at HQ
- PROD: HQGIPSDPSFSP1 + HQGIPSDPSFSP2 at HQ
- DR: IMGIPSDPSFSD1 + IMGIPSDPSFSD2 at IM
- COOP IM: IMGIPSDPSFSC1 + IMGIPSDPSFSC2
- COOP HQ: HQGIPSDPSFSC3 + HQGIPSDPSFSC4

Each cluster requires:

- two physical nodes
- C:\\ 200 GB + D:\\ 300 GB local storage, 500 GB usable total, hardware RAID 1
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

The File Share Witness contains quorum metadata only and must reside on a third independent system. It must not be hosted on either peer node or on that cluster's own shared business-data storage.

## Patching rule

Peer nodes must use non-overlapping reboot windows and must never be rebooted together. DR and either COOP recovery cluster must not be intentionally taken down in the same maintenance window as PROD.
