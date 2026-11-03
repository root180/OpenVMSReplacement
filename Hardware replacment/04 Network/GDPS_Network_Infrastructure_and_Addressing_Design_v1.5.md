# GDPS Network Infrastructure and Addressing Design v1.5

## Scope

Defines the network placement and source-network traceability for DEV, TEST, PROD, DR, COOP DCIAC02, and COOP DCIAC03.

## Environment placement

| Environment | GDPS placement | Source Alpha placement |
|---|---|---|
| DEV | Existing GPO virtualization; separate virtual design | ALPHA0 source hardware at IMDC |
| TEST | HQ | New environment |
| PROD | HQ | ALPHA3 at HQ |
| DR | IM | ALPHA6 at IM |
| COOP DCIAC02 | DCIAC02 / CRATE | ALPHA10 |
| COOP DCIAC03 | DCIAC03 / CRATE | ALPHA13 |

## Design rules

- TEST and PROD are not stretched clusters.
- DR is a separate two-node recovery cluster at IM.
- COOP consists of **two separate two-node recovery clusters**: DCIAC02 and DCIAC03.
- Exact new GDPS VLAN IDs, IP assignments, gateways, firewall rule IDs, and switch ports remain Network/Security assignments.
- Existing Alpha addresses below are source-system traceability and are not automatic GDPS address reservations.
- One physical Alpha node may expose multiple node/service addresses; one-for-one physical replacement does not mean one-IP-for-one-IP.

## Existing network anchors

### ALPHA3 / PROD source

Subnet mask confirmed: **255.255.255.0 (/24)**.

- N3A: **172.16.35.15, 172.16.35.16**
- N3B: **172.16.35.19 (IE2, primary), 172.16.35.20 (IE3)**
- Cluster/service alias: `alpha3.gpo.gov`

N3B addresses were confirmed from the source node. N3A uses the remaining two addresses in the Alpha3 DNS set.

### ALPHA6 / DR source

- Cluster/service DNS set: **172.19.128.41, .42, .43, .44**
- Subnet: **/24**
- N6A has been observed using .41 and .43; final per-node split should be confirmed on the source nodes before address reuse/cutover decisions.

### ALPHA10 / COOP DCIAC02 source

- ALPHA11: **172.23.5.42, 172.23.5.43**
- ALPHA12: **172.23.5.44, 172.23.5.45**
- Cluster/service name: `alpha10.gpo.gov`

### ALPHA13 / COOP DCIAC03 source

- Cluster/service DNS set: **172.23.6.42, .43, .44, .45**
- Individual source-node names and address split remain to be confirmed from ALPHA13.

### ALPHA0 / DEV source

- Source cluster DNS set: **172.23.4.42, .43, .44, .45**
- Source hardware placement: **IMDC**
- DEV replacement is virtual and is outside the 10 physical-server request set.

## Storage network

TEST, PROD, DR, COOP DCIAC02, and COOP DCIAC03 each require redundant Fibre Channel connectivity independent of normal SMB/client-access networking.

- ST-01 TEST: 14.4 TB minimum
- ST-02 PROD: 14.4 TB minimum
- ST-03 DR: 14.4 TB minimum
- ST-04 COOP DCIAC02: 14.4 TB minimum
- ST-05 COOP DCIAC03: 21.4 TB minimum

## Availability and maintenance boundary

Peer nodes of a cluster must not be rebooted simultaneously. PROD, DR, and COOP maintenance windows must be arranged so recovery capability is not intentionally removed at the same time as PROD service.
