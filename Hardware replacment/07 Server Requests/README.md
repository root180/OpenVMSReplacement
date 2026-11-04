# Server Requests

This folder contains the authoritative GDPS physical-server request set.

Current controlled set:

- `v8 10-Node Physical Server Tickets/`

That folder contains:

- 10 current ServiceNow server-request documents
- the authoritative placement and replacement matrix
- the controlled set README

## Physical server count

- TEST: 2 new physical nodes
- PROD: 2 replacement physical nodes
- DR: 2 replacement physical nodes
- COOP IM: 2 replacement physical nodes
- COOP HQ: 2 replacement physical nodes
- **Total: 10 physical GDPS servers**

## Replacement rule

TEST is the only new physical cluster.

PROD replaces ALPHA3:
- N3A
- N3B

DR replaces ALPHA6:
- N6A
- N6B

COOP IM replaces ALPHA10:
- ALPH11
- ALPH12

COOP HQ replaces N13A and N13B, the two confirmed physical ALPHA13 nodes.

ALPHA0 is handled separately by the DEV virtualization design and is not part of this physical-server request set.

## Storage request alignment

- SR-01/SR-02 -> ST-01
- SR-03/SR-04 -> ST-02
- SR-05/SR-06 -> ST-03
- SR-07/SR-08 -> ST-04
- SR-09/SR-10 -> ST-05

Server names are architecture-controlled identifiers and must not be changed during provisioning without architecture reconciliation.
