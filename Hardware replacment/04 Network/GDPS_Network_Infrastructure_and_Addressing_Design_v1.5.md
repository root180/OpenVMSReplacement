# GDPS Network Infrastructure and Addressing Design v1.5

## Scope

Defines the network placement and security boundaries for DEV, TEST, PROD, DR, and COOP.

## Environment placement

- DEV: existing GPO virtualization at HQ
- TEST: HQ
- PROD: HQ
- DR: IM
- COOP: DCIAC / CRATE

## Design rules

- TEST and PROD are not stretched clusters.
- DR is a separate two-node recovery cluster at IM.
- COOP is a separate two-node recovery cluster in the crate.
- Network/security zones shall be separated with explicit routing and firewall policy.
- Exact VLAN IDs, IPs, gateways, firewall rule IDs, and switch ports remain Network/Security TBD.

## Existing network anchors

- Alpha0: 172.23.4.42 / 172.23.4.0/25 / gateway 172.23.4.1
- Alpha3: observed 172.16.35.15; exact subnet/gateway TBD
- Alpha6: 172.19.128.41 and 172.19.128.42 /24 / gateway 172.19.128.1
- Alpha10: observed 172.23.5.43; subnet/gateway TBD
- Alpha13: observed 172.23.6.45; subnet/gateway TBD

## Storage network

TEST, PROD, DR, and COOP use redundant Fibre Channel fabrics independent of normal SMB/client-access networking.

Storage capacities shown in network diagrams are minimums and may be increased but not reduced.
