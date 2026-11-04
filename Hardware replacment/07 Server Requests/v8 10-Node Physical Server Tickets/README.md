# GDPS 10-Node Physical Server Request Set — v8

This folder is the controlled ServiceNow physical-server request set for the GDPS Alpha replacement.

## Governing rule

The physical deployment follows the existing Alpha setup. This is a technology replacement, not a redesign of the business or recovery model.

- **TEST** is the only new physical cluster.
- **PROD** replaces ALPHA3 at HQ.
- **DR** replaces ALPHA6 at IM.
- **COOP** replaces both existing COOP clusters. SR-09/10 are the selected HQ pair replacing N13A/N13B from ALPHA13 / DCIAC03; SR-07/08 retain their submitted IM names.
- **ALPHA0** is handled separately by the DEV virtualization design and does not generate a physical-server request in this set.

## Authoritative node mapping

| Ticket | GDPS Server | Environment | Location | Existing Alpha node replaced |
|---|---|---|---|---|
| SR-01 | HQGIPSDPSFST1 | TEST | HQ | N/A — new TEST |
| SR-02 | HQGIPSDPSFST2 | TEST | HQ | N/A — new TEST |
| SR-03 | HQGIPSDPSFSP1 | PROD | HQ | N3A — ALPHA3 |
| SR-04 | HQGIPSDPSFSP2 | PROD | HQ | N3B — ALPHA3 |
| SR-05 | IMGIPSDPSFSD1 | DR | IM | N6A — ALPHA6 |
| SR-06 | IMGIPSDPSFSD2 | DR | IM | N6B — ALPHA6 |
| SR-07 | IMGIPSDPSFSC1 | COOP | DCIAC02 / CRATE | ALPHA11 — ALPHA10 |
| SR-08 | IMGIPSDPSFSC2 | COOP | DCIAC02 / CRATE | ALPHA12 — ALPHA10 |
| SR-09 | HQGIPSDPSFSC3 | COOP | HQ | N13A — ALPHA13 / DCIAC03 |
| SR-10 | HQGIPSDPSFSC4 | COOP | HQ | N13B — ALPHA13 / DCIAC03 |

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

SR-09 and SR-10 are located at **HQ**, a new placement decision for the ALPHA13 replacement pair. SR-07 and SR-08 retain their submitted IM names. Legacy DCIAC labels identify replacement sources and do not establish the new servers' physical destinations.

## ServiceNow submission

Use the exact dropdown labels available in the live ServiceNow catalog. For COOP, select **COOP** for environment and **DCIAC (Data Center in a Crate)** for data center, matching the existing COOP request form.

## ServiceNow field mapping

Every ticket follows the live form order, includes a clear environment-specific Purpose, and states the paired hostname and peer ticket in Description. The 128 GB RAM quantity is stated in Purpose and Special Requirements because the memory dropdown has no quantity box.

## Changes in v8

This folder supersedes **v7 10-Node Physical Server Tickets**. All ten tickets now use one consistent template:

- **Patching:** Mondays only, with separate non-overlapping windows for peer nodes; DR and COOP must not overlap PROD. Exact catalog group, week and time are confirmed with IT.
- **Traceability:** N3A (172.16.35.15, .16) derived from the confirmed N3B split; N6A observed on .41 and .43; ALPHA13 node names and split marked for confirmation.
- **Storage:** 14.4 TB baseline for TEST, PROD, DR and DCIAC02 (3PAR parity); **21.4 TB for DCIAC03** (Primera parity); DR and COOP replication from PROD stated.
- **Cluster:** active/active, dual independent fabrics, File Share Witness on a third system.
- **Memory:** 128 GB RAM minimum is explicitly stated in Purpose and Special Requirements. The dropdown selects the applicable catalog approval category.
- **Native storage:** C:\ 200 GB + D:\ 300 GB, 500 GB usable, hardware RAID 1, justified one-to-one against ALPHA3.

## Storage request alignment

- ST-01 — TEST / HQ — >=14.4 TB
- ST-02 — PROD / HQ — >=14.4 TB
- ST-03 — DR / IM — >=14.4 TB
- ST-04 — COOP DCIAC02 — >=14.4 TB
- ST-05 — COOP DCIAC03 — >=21.4 TB
