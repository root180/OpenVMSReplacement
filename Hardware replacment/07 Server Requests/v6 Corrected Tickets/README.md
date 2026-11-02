# GDPS Server Request Tickets - v6 Corrected

This folder contains the current eight-server request set aligned to the GDPS Hardware Master v4.3.

| Ticket | Server | Environment | Site |
|---|---|---|---|
| SR-01 | HQVMGDPSFST1 | TEST | HQ |
| SR-02 | HQVMGDPSFST2 | TEST | HQ |
| SR-03 | HQVMGDPSFSP1 | PROD | HQ |
| SR-04 | HQVMGDPSFSP2 | PROD | HQ |
| SR-05 | IMVMGDPSFSD1 | DR | IM |
| SR-06 | IMVMGDPSFSD2 | DR | IM |
| SR-07 | IMVMGDPSFSC1 | COOP / DCIAC | IM / CRATE |
| SR-08 | IMVMGDPSFSC2 | COOP / DCIAC | IM / CRATE |

## Corrections incorporated

- TEST is a two-node HQ cluster; no stretched HQ/IM TEST cluster.
- PROD is a two-node HQ cluster; no stretched HQ/IM PROD cluster.
- DR is a separate two-node IM cluster.
- COOP / DCIAC is a separate two-node recovery cluster.
- HPE Windows/WSFC storage minimums are 14.4 TB for TEST/PROD/DR and 21.4 TB for COOP.
- LUN00-LUN09 capacities are minimum sizing floors; larger is allowed, smaller is prohibited.
- Cluster peers must not be rebooted simultaneously.
- Controlled document references are Hardware Master v4.3, Acquisition SOW v1.9, Storage Architecture v1.1, and File Cluster/SMB Standard v1.8.

The ServiceNow live form may use exact dropdown labels that differ from the descriptive wording in these worksheets; use the exact catalog value available at submission time.
