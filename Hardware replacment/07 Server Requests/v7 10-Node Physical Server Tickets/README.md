# GDPS 10-Node Physical Server Request Set — v7

This folder is the controlled ServiceNow physical-server request set for the GDPS Alpha replacement.

## Governing rule

The physical deployment follows the existing Alpha setup. This is a technology replacement, not a redesign of the business or recovery model.

- **TEST** is the only new physical cluster.
- **PROD** replaces ALPHA3 at HQ.
- **DR** replaces ALPHA6 at IM.
- **COOP** replaces both existing COOP clusters in the **DCIAC Data Center in a Crate (CRATE)**.
- **ALPHA0** is handled separately by the DEV virtualization design and does not generate a physical-server request in this set.

## Authoritative node mapping

| Ticket | GDPS Server | Environment | Location | Existing Alpha node replaced |
|---|---|---|---|---|
| SR-01 | HQVMGDPSFST1 | TEST | HQ | N/A — new TEST |
| SR-02 | HQVMGDPSFST2 | TEST | HQ | N/A — new TEST |
| SR-03 | HQVMGDPSFSP1 | PROD | HQ | N3A — ALPHA3 |
| SR-04 | HQVMGDPSFSP2 | PROD | HQ | N3B — ALPHA3 |
| SR-05 | IMVMGDPSFSD1 | DR | IM | N6A — ALPHA6 |
| SR-06 | IMVMGDPSFSD2 | DR | IM | N6B — ALPHA6 |
| SR-07 | IMVMGDPSFSC1 | COOP | DCIAC / CRATE | ALPHA11 — ALPHA10 |
| SR-08 | IMVMGDPSFSC2 | COOP | DCIAC / CRATE | ALPHA12 — ALPHA10 |
| SR-09 | IMVMGDPSFSC3 | COOP | DCIAC / CRATE | N13A — ALPHA13 |
| SR-10 | IMVMGDPSFSC4 | COOP | DCIAC / CRATE | N13B — ALPHA13 |

## Count

- 2 new TEST physical servers
- 8 one-for-one physical Alpha replacements
- **10 physical GDPS server requests total**

## Physical node and network replacement principle

One physical Alpha server is replaced by one physical GDPS server. A one-for-one physical replacement does **not** imply a one-IP-for-one-IP design.

The existing Alpha physical nodes can have multiple IP addresses and network interfaces, and the replacement GDPS physical nodes may likewise require multiple IP addresses and interfaces to reproduce the existing network functions. Depending on the existing role, those functions may include:

- primary server or management connectivity;
- cluster/private connectivity;
- service-facing connectivity;
- storage-related network connectivity where applicable; and
- clustered client-access or service IPs that belong to the cluster/service identity rather than to the physical node itself.

The objective is to preserve the existing network function and availability behavior, not to blindly copy every Alpha address onto the replacement server.

For build and cutover:

1. Replace each existing Alpha physical node with its mapped GDPS physical node.
2. Provision the GDPS node with the network interfaces and IP addresses required to reproduce the existing node role.
3. Keep cluster/service identities distinct from physical-node identities.
4. Treat existing Alpha IP information in the ticket set as source-system traceability unless an address is explicitly approved for reuse.
5. Move any legacy clustered service, DNS, SMB, or client-access identity only after the prior Alpha owner has been released and the cutover plan authorizes activation on GDPS.

Therefore, **one physical Alpha server replacing one physical GDPS server may legitimately involve multiple IP addresses on the replacement server**, where the existing configuration requires them.

## Placement control

HQ and IM are used for the normal TEST/PROD/DR infrastructure according to the existing deployment pattern. COOP remains in the **DCIAC Data Center in a Crate** and must not be reclassified as an ordinary IM server deployment merely because the hostname uses the IM site prefix.

## ServiceNow submission

Use the exact dropdown labels available in the live ServiceNow catalog. For COOP, select **COOP** for environment and **DCIAC (Data Center in a Crate)** for data center, matching the existing COOP request form.
