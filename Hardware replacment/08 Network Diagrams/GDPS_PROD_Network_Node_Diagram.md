# GDPS PROD Network Node Diagram

Location: **HQ**. ServiceNow environment: **PROD**. Replaces the two physical nodes of **ALPHA3**.

```mermaid
flowchart TB
subgraph P["HQ - PROD cluster replacing ALPHA3"]
direction TB
PN["Server Distribution Network"]
P1["HQGIPSDPSFSP1 | SR-03
Replaces: N3A - ALPHA3"]
P2["HQGIPSDPSFSP2 | SR-04
Replaces: N3B - ALPHA3"]
PA["Fibre Channel fabric A"]
PB["Fibre Channel fabric B"]
PS[("PROD shared SAN - 14.4 TB usable minimum")]
PW["Independent File Share Witness
Third system - host/share TBD"]
PN --- P1
PN --- P2
P1 <-.->|Active/active pair| P2
P1 --- PA
P1 --- PB
P2 --- PA
P2 --- PB
PA --- PS
PB --- PS
PN -. Quorum access .- PW
end
```

These are logical node and connectivity diagrams. Each server box contains both the new hostname and its replacement relationship. Network links represent redundant Server Distribution connectivity; storage paths use two independent Fibre Channel fabrics with Windows MPIO. The witness resides on a third independent system, outside the cluster nodes and their shared storage. Assigned network IPs, VLANs, switch ports, WWPNs and zoning remain with the infrastructure teams.

Storage request: **ST-02**. COOP replication sources, targets, direction, topology, technology, and schedule are to be determined by GPO network engineers.

Source: [current physical server tickets](../07%20Server%20Requests/v8%2010-Node%20Physical%20Server%20Tickets/).
