# GDPS SMB Namespace Migration and Cutover Plan v1.3

## Goal

Preserve existing application UNC paths while preventing duplicate SMB ownership anywhere in the GPO enterprise namespace.

## Pre-cutover

Current owner:

- alpha0
- alpha3
- alpha6

GDPS staging identities:

- alpha0-1
- alpha3-1
- alpha6-1

## Cutover principle

The old owner must be disabled, released, and proven absent before GDPS activates the original application-facing identity.

## Final application contract

Applications continue using:

- \\alpha0\...
- \\alpha3\...
- \\alpha6\...

Applications are not permanently changed to the -1 staging identities.

## DR / COOP transfer

PROD normally owns the production SMB service identity. DR or COOP may assume that identity only after the current owner is disabled and released. Returning service to PROD is another controlled identity transfer.

## Storage dependency

Destination HPE Windows/WSFC storage and LUN00-LUN09 must be healthy and synchronized before SMB identity ownership is transferred. Each LUN must meet or exceed its controlled minimum capacity.
