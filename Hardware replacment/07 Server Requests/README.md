# Server Requests

This folder contains the **single authoritative GDPS physical-server request set**.

Current controlled set:

- `v7 10-Node Physical Server Tickets/`

That folder contains:

- 10 current ServiceNow server-request documents
- the authoritative placement and replacement matrix
- the controlled set README

## Physical server count

- TEST: 2 new physical nodes
- PROD: 2 replacement physical nodes
- DR: 2 replacement physical nodes
- COOP: 4 replacement physical nodes
- **Total: 10 physical GDPS servers**

## Replacement rule

TEST is the only new physical cluster.

PROD replaces ALPHA3:
- N3A
- N3B

DR replaces ALPHA6:
- N6A
- N6B

COOP remains in the DCIAC Data Center in a Crate and replaces both existing COOP clusters:

ALPHA10:
- ALPHA11
- ALPHA12

ALPHA13:
- N13A
- N13B

ALPHA0 is handled separately by the DEV virtualization design and is not part of this physical-server request set.

Server names are architecture-controlled identifiers and must not be changed during provisioning without architecture reconciliation.
