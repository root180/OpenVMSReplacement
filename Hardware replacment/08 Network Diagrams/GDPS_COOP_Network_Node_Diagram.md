# GDPS COOP Network Node Diagram

ServiceNow environment: **COOP** for all six nodes. The ALPHA6 replacement pair resides at **IM**; the ALPHA10 replacement pair is at **IM**, and the ALPHA13 replacement pair is at **HQ**. These are three separate two-node clusters.

```mermaid
flowchart TB
subgraph I["IM - COOP cluster replacing ALPHA6"]
direction TB
IN["Server Distribution Network"]
I1["IMGIPSDPSFSD1 | SR-05
Replaces: N6A - ALPHA6"]
I2["IMGIPSDPSFSD2 | SR-06
Replaces: N6B - ALPHA6"]
IA["Fibre Channel fabric A"]
IB["Fibre Channel fabric B"]
IS[("IM shared SAN - 14.4 TB usable minimum")]
IW["Independent File Share Witness
Third system - host/share TBD"]
IN --- I1
IN --- I2
I1 <-.->|Active/active pair| I2
I1 --- IA
I1 --- IB
I2 --- IA
I2 --- IB
IA --- IS
IB --- IS
IN -. Quorum access .- IW
end
subgraph C2["IM - COOP cluster replacing ALPHA10"]
direction TB
C2N["Server Distribution Network"]
C21["IMGIPSDPSFSC1 | SR-07
Replaces: ALPH11 - ALPHA10"]
C22["IMGIPSDPSFSC2 | SR-08
Replaces: ALPH12 - ALPHA10"]
C2A["Fibre Channel fabric A"]
C2B["Fibre Channel fabric B"]
C2S[("IM COOP shared SAN - 14.4 TB usable minimum")]
C2W["Independent File Share Witness
Third system - host/share TBD"]
C2N --- C21
C2N --- C22
C21 <-.->|Active/active pair| C22
C21 --- C2A
C21 --- C2B
C22 --- C2A
C22 --- C2B
C2A --- C2S
C2B --- C2S
C2N -. Quorum access .- C2W
end
subgraph C3["HQ - COOP cluster replacing ALPHA13"]
direction TB
C3N["Server Distribution Network"]
C31["HQGIPSDPSFSC3 | SR-09
Replaces: N13A - ALPHA13"]
C32["HQGIPSDPSFSC4 | SR-10
Replaces: N13B - ALPHA13"]
C3A["Fibre Channel fabric A"]
C3B["Fibre Channel fabric B"]
C3S[("HQ COOP shared SAN - 21.4 TB usable minimum")]
C3W["Independent File Share Witness
Third system - host/share TBD"]
C3N --- C31
C3N --- C32
C31 <-.->|Active/active pair| C32
C31 --- C3A
C31 --- C3B
C32 --- C3A
C32 --- C3B
C3A --- C3S
C3B --- C3S
C3N -. Quorum access .- C3W
end
```

These are logical node and connectivity diagrams. Each server box contains both the new hostname and its replacement relationship. Network links represent redundant Server Distribution connectivity; storage paths use two independent Fibre Channel fabrics with Windows MPIO. The witness resides on a third independent system, outside the cluster nodes and their shared storage. Assigned network IPs, VLANs, switch ports, WWPNs and zoning remain with the infrastructure teams.

COOP replication sources, targets, direction, topology, technology, and schedule are to be determined by GPO network engineers. Each cluster requires its own independent witness share; witness host placement is TBD.

| Replacement cluster | Location | Storage request | Shared SAN baseline |
|---|---|---|---|
| ALPHA6 replacement | IM | ST-03 | 14.4 TB usable minimum |
| ALPHA10 replacement | IM | ST-04 | 14.4 TB usable minimum |
| ALPHA13 replacement | HQ | ST-05 | 21.4 TB usable minimum |

ALPHA13 members N13A and N13B are confirmed by `SHOW CLUSTER`; their interfaces are confirmed by `TCPIP SHOW INTERFACE`. The approved new hostnames containing `FSD` remain unchanged even though the ServiceNow environment is COOP.

Source: [current physical server tickets](../07%20Server%20Requests/v8%2010-Node%20Physical%20Server%20Tickets/).
