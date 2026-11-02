# GDPS Physical Server Request Register v6

## Current ticket set

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

## Baseline

Each physical node has a minimum memory baseline of 128 GB and participates in a separate two-node WSFC cluster for its environment.

- TEST and PROD are both two-node HQ clusters.
- DR is a separate two-node IM cluster.
- COOP / DCIAC is a separate two-node recovery cluster.
- The VM token in the established hostname convention does not mean these physical nodes are virtual machines.
- Cluster peers must not be rebooted simultaneously.
- LUN00-LUN09 and environment storage capacities are minimum sizing floors: larger is permitted, smaller is prohibited.

See: `v6 Corrected Tickets/` for the eight current ticket documents.
