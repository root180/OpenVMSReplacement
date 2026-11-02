# GDPS 10-Ticket Placement and Replacement Matrix

This matrix is the authoritative placement and replacement reference for the ten GDPS physical-server ServiceNow requests.

The deployment follows the existing Alpha setup. TEST is the only new physical cluster. PROD, DR, and COOP preserve the existing physical replacement relationships and site model.

| Ticket | New GDPS Node | Environment | New Node Location | Existing Alpha System | Existing Node Replaced | Replacement Status |
|---|---|---|---|---|---|---|
| SR-01 | HQVMGDPSFST1 | TEST | HQ | None | N/A | New TEST node; no existing Alpha replacement |
| SR-02 | HQVMGDPSFST2 | TEST | HQ | None | N/A | New TEST node; no existing Alpha replacement |
| SR-03 | HQVMGDPSFSP1 | PROD | HQ | ALPHA3 | N3A | Direct physical replacement |
| SR-04 | HQVMGDPSFSP2 | PROD | HQ | ALPHA3 | N3B | Direct physical replacement |
| SR-05 | IMVMGDPSFSD1 | DR | IM | ALPHA6 | N6A | Direct physical replacement |
| SR-06 | IMVMGDPSFSD2 | DR | IM | ALPHA6 | N6B | Direct physical replacement |
| SR-07 | IMVMGDPSFSC1 | COOP | DCIAC / Data Center in a Crate | ALPHA10 | ALPHA11 | Direct physical COOP replacement |
| SR-08 | IMVMGDPSFSC2 | COOP | DCIAC / Data Center in a Crate | ALPHA10 | ALPHA12 | Direct physical COOP replacement |
| SR-09 | IMVMGDPSFSC3 | COOP | DCIAC / Data Center in a Crate | ALPHA13 | N13A | Direct physical COOP replacement |
| SR-10 | IMVMGDPSFSC4 | COOP | DCIAC / Data Center in a Crate | ALPHA13 | N13B | Direct physical COOP replacement |

## Physical-server count

- TEST: 2 new physical nodes
- PROD: 2 replacement physical nodes
- DR: 2 replacement physical nodes
- COOP: 4 replacement physical nodes
- Total: **10 physical GDPS server requests**

## DEV / ALPHA0 disposition

ALPHA0 is not part of this physical-server request set. Its existing physical nodes, ALPHA1 and ALPHA2, are accounted for separately through the GDPS DEV virtualization design.

## Placement rule

- TEST: HQ
- PROD: HQ
- DR: IM
- COOP: DCIAC / Data Center in a Crate

COOP remains the DCIAC / CRATE recovery environment and is not treated as an ordinary IM server deployment merely because the GDPS COOP hostnames use the IM site prefix.
