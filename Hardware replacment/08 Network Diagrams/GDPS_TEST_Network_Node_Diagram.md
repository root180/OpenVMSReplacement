# GDPS TEST Network Node Diagram

Location: **HQ**. ServiceNow environment: **Test**. Both physical nodes are new; neither replaces an existing Alpha node.

```mermaid
flowchart TB
subgraph T["HQ - TEST cluster"]
direction TB
TN["Server Distribution Network"]
T1["HQGIPSDPSFST1 | SR-01
Replaces: N/A - new TEST node"]
T2["HQGIPSDPSFST2 | SR-02
Replaces: N/A - new TEST node"]
TA["Fibre Channel fabric A"]
TB["Fibre Channel fabric B"]
TS[("TEST shared SAN - 14.4 TB usable minimum")]
TW["Independent File Share Witness
Third system - host/share TBD"]
TN --- T1
TN --- T2
T1 <-.->|Active/active pair| T2
T1 --- TA
T1 --- TB
T2 --- TA
T2 --- TB
TA --- TS
TB --- TS
TN -. Quorum access .- TW
end
```

These are logical node and connectivity diagrams. Each server box contains both the new hostname and its replacement relationship. Network links represent redundant Server Distribution connectivity; storage paths use two independent Fibre Channel fabrics with Windows MPIO. The witness resides on a third independent system, outside the cluster nodes and their shared storage. Assigned network IPs, VLANs, switch ports, WWPNs and zoning remain with the infrastructure teams.

Storage request: **ST-01**. TEST validates the existing Alpha production cluster, storage, failover and recovery behavior before release.

Source: [current physical server tickets](../07%20Server%20Requests/v8%2010-Node%20Physical%20Server%20Tickets/).
