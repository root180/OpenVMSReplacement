# GDPS 10-Ticket Placement and Replacement Matrix — v8

This matrix is the authoritative placement, replacement, and existing-network traceability reference for the ten GDPS physical-server ServiceNow requests.

The deployment follows the existing Alpha setup. TEST is the only new physical cluster. PROD, DR, and COOP preserve the existing physical replacement relationships and site model. Every existing Alpha cluster is two HPE Integrity servers (active/active) with dual Brocade Fibre Channel switches and shared HPE storage.

## Replacement matrix

| Ticket | New GDPS Node | Environment | New Node Location | Existing Alpha System | Existing Node Replaced | Existing Alpha DNS / IP Traceability | Replacement Status |
|---|---|---|---|---|---|---|---|
| SR-01 | HQVMGDPSFST1 | TEST | HQ | None | N/A | N/A | New TEST node; no existing Alpha replacement |
| SR-02 | HQVMGDPSFST2 | TEST | HQ | None | N/A | N/A | New TEST node; no existing Alpha replacement |
| SR-03 | HQVMGDPSFSP1 | PROD | HQ | ALPHA3 | N3A | 172.16.35.15, 172.16.35.16 (the alpha3 addresses not held by N3B); cluster alias alpha3.gpo.gov | Direct physical replacement |
| SR-04 | HQVMGDPSFSP2 | PROD | HQ | ALPHA3 | N3B | 172.16.35.19 (IE2, primary), 172.16.35.20 (IE3) (cluster alias alpha3.gpo.gov) | Direct physical replacement |
| SR-05 | IMVMGDPSFSD1 | DR | IM | ALPHA6 | N6A | alpha6.gpo.gov: 172.19.128.41–.44; N6A observed connecting from .41 and .43 | Direct physical replacement |
| SR-06 | IMVMGDPSFSD2 | DR | IM | ALPHA6 | N6B | alpha6.gpo.gov: 172.19.128.41–.44; node split to be confirmed | Direct physical replacement |
| SR-07 | IMVMGDPSFSC1 | COOP | DCIAC02 (Data Center in a Crate) | ALPHA10 | ALPHA11 | alpha11.gpo.gov: 172.23.5.42, 172.23.5.43 | Direct physical COOP replacement |
| SR-08 | IMVMGDPSFSC2 | COOP | DCIAC02 (Data Center in a Crate) | ALPHA10 | ALPHA12 | alpha12.gpo.gov: 172.23.5.44, 172.23.5.45 | Direct physical COOP replacement |
| SR-09 | IMVMGDPSFSC3 | COOP | DCIAC03 (Data Center in a Crate) | ALPHA13 | N13A (node name to be confirmed) | alpha13.gpo.gov: 172.23.6.42–.45; node split to be confirmed | Direct physical COOP replacement |
| SR-10 | IMVMGDPSFSC4 | COOP | DCIAC03 (Data Center in a Crate) | ALPHA13 | N13B (node name to be confirmed) | alpha13.gpo.gov: 172.23.6.42–.45; node split to be confirmed | Direct physical COOP replacement |

## Existing Alpha estate (hardware inventory)

| Alpha cluster | Role | Hardware | Shared storage | Site | Replacement |
|---|---|---|---|---|---|
| ALPHA3 | Production | HPE Integrity i6, 2 nodes | HPE 3PAR, 14.4 TB | HQ | SR-03, SR-04 (physical) |
| ALPHA6 | DR (labelled "Backup System" in Figure 2) | HPE Integrity i6, 2 nodes | HPE 3PAR, 14.4 TB | IMDC | SR-05, SR-06 (physical) |
| ALPHA10 | COOP, DCIAC02 | HPE Integrity i6, 2 nodes | HPE 3PAR, 14.4 TB | DCIAC02 | SR-07, SR-08 (physical) |
| ALPHA13 | COOP, DCIAC03 | HPE Integrity i6, 2 nodes | HPE Primera, 21.4 TB | DCIAC03 | SR-09, SR-10 (physical) |
| ALPHA0 | Development | HPE Integrity i2, 2 nodes (alpha1, alpha2) | HPE 3PAR, 14.4 TB | IMDC | GDPS DEV virtual-server design (not in this request set) |

Controlled recovery replication is PROD -> DR, PROD -> COOP DCIAC02, and PROD -> COOP DCIAC03. DEV/ALPHA0 is not treated as a production recovery target in this acquisition baseline.

Physical count: 5 clusters × 2 nodes = 10 existing Integrity nodes. ALPHA0 moves to virtual servers, so 8 existing nodes are replaced physically, plus 2 new TEST nodes = **10 physical GDPS server requests**.

## Not in scope

| Name | DNS | Status |
|---|---|---|
| alpha7.gpo.gov | 172.19.128.15–.18 | Not in the hardware inventory. DNS record only; presumed retired. Confirm and request DNS cleanup. |
| alpha8.gpo.gov | 172.19.128.19–.22 | Not in the hardware inventory. DNS record only; presumed retired. Confirm and request DNS cleanup. |
| alpha4, alpha5, alpha9, alpha14–20 | Not found | Do not exist. |

## Native storage standard (per physical server)

Sized one-to-one against the ALPHA3 production node (N3B):

| Windows drive | Size | Replaces on ALPHA3 | ALPHA3 size |
|---|---|---|---|
| C:\ | 200 GB | System disk ALPHA3SYS (`$1$DGA1`) | 200 GB (118 GB used) |
| D:\ | 300 GB | Local disk N3B_PAGE (`$59$DKA0`, HP logical volume) | 300 GB |
| **Total** | **500 GB usable, hardware RAID 1 (mirrored)** | | 500 GB |

On ALPHA3 the system disk is on SAN and the local disk holds paging. On Windows both roles move to local storage. Shared clustered business data remains on SAN.

## SAN storage baseline (ALPHA3 production, current)

Captured from N3B with `SHOW DEVICE D/FULL`. GB = 1,073,741,824 bytes.

| Volume | Used (GB) | Total (GB) |
|---|---|---|
| ALPHA3SYS (OpenVMS system disk; not carried over) | 118.4 | 200 |
| T4DATA | 27.8 | 50 |
| OPS_DISK | 5.2 | 10 |
| CIFS_DATA | 4.7 | 10 |
| CIFS_LOCK | 0.2 | 5 |
| CIFS_LOGS | 22.1 | 50 |
| DATA_COPY | 31.8 | 2,028 |
| ADMIN | 33.4 | 50 |
| USER | 0.0 | 25 |
| SCRATCH | 3.2 | 50 |
| RAIDSET00 | 162.2 | 300 |
| RAIDSET01 | 488.2 | 500 (98% used) |
| RAIDSET02 | 505.4 | 600 |
| RAIDSET03 | 58.6 | 100 |
| RAIDSET04 | 20.3 | 50 |
| RAIDSET05 | 25.7 | 100 |
| RAIDSET06 | 15.2 | 50 |
| RAIDSET07 | 5.6 | 100 |
| RAIDSET08 | 9.0 | 50 |
| RAIDSET09 | 0.1 | 100 |
| **Total** | **≈ 1,537** | **≈ 4,428** |

ALPHA3 is the sizing standard for all replacement environments.

## SAN baseline per ticket

| Tickets | Environment | Baseline (parity with existing array) | Storage request |
|---|---|---|---|
| SR-01, SR-02 | TEST | 14.4 TB usable minimum | ST-01 |
| SR-03, SR-04 | PROD | 14.4 TB usable minimum (ALPHA3 3PAR) | ST-02 |
| SR-05, SR-06 | DR | 14.4 TB usable minimum (ALPHA6 3PAR) | ST-03 |
| SR-07, SR-08 | COOP DCIAC02 | 14.4 TB usable minimum (ALPHA10 3PAR) | ST-04 |
| SR-09, SR-10 | COOP DCIAC03 | 21.4 TB usable minimum (ALPHA13 Primera) | ST-05 |

## Network traceability note

The IP addresses above are current DNS A-record results and interface listings for the existing Alpha names. They are retained for migration and replacement traceability only.

They are **not** assignments or reservations for the new GDPS servers. New GDPS IP addresses, DNS records, VLANs, and related network values remain subject to GPO Network/Security assignment.

Node-level IP sources:

- ALPHA3: N3B addresses confirmed with `TCPIP SHOW INTERFACE` on N3B (IE2 172.16.35.19, IE3 172.16.35.20). N3A holds the remaining two addresses of alpha3.gpo.gov (172.16.35.15, .16); `alpha3.gpo.gov` is the cluster alias.
- ALPHA6: full set retained on both tickets; N6A has been observed connecting from .41 and .43. Confirm with `TCPIP SHOW INTERFACE` on each node.
- ALPHA10: alpha11 and alpha12 resolve independently; their addresses are recorded directly.
- ALPHA13: full set retained on both tickets; node names and split to be confirmed with `SHOW CLUSTER` and `TCPIP SHOW INTERFACE`.

## DNS discovery command retained for safekeeping

```powershell
0..20 | ForEach-Object { $n="alpha$_.gpo.gov"; try { $ip=(Resolve-DnsName $n -Type A -ErrorAction Stop).IPAddress -join ', '; "{0,-18} {1}" -f $n,$ip } catch { "{0,-18} NOT FOUND" -f $n } }
```

### Captured results

```text
alpha0.gpo.gov     172.23.4.43, 172.23.4.42, 172.23.4.45, 172.23.4.44
alpha1.gpo.gov     172.23.4.43, 172.23.4.42
alpha2.gpo.gov     172.23.4.45, 172.23.4.44
alpha3.gpo.gov     172.16.35.16, 172.16.35.15, 172.16.35.20, 172.16.35.19
alpha4.gpo.gov     NOT FOUND
alpha5.gpo.gov     NOT FOUND
alpha6.gpo.gov     172.19.128.44, 172.19.128.43, 172.19.128.42, 172.19.128.41
alpha7.gpo.gov     172.19.128.18, 172.19.128.15, 172.19.128.16, 172.19.128.17
alpha8.gpo.gov     172.19.128.22, 172.19.128.19, 172.19.128.20, 172.19.128.21
alpha9.gpo.gov     NOT FOUND
alpha10.gpo.gov    172.23.5.45, 172.23.5.42, 172.23.5.44, 172.23.5.43
alpha11.gpo.gov    172.23.5.42, 172.23.5.43
alpha12.gpo.gov    172.23.5.45, 172.23.5.44
alpha13.gpo.gov    172.23.6.43, 172.23.6.42, 172.23.6.45, 172.23.6.44
alpha14.gpo.gov    NOT FOUND
alpha15.gpo.gov    NOT FOUND
alpha16.gpo.gov    NOT FOUND
alpha17.gpo.gov    NOT FOUND
alpha18.gpo.gov    NOT FOUND
alpha19.gpo.gov    NOT FOUND
alpha20.gpo.gov    NOT FOUND
```

## Placement rule

- TEST: HQ
- PROD: HQ
- DR: IM
- COOP: DCIAC / Data Center in a Crate (DCIAC02 for ALPHA10 replacements, DCIAC03 for ALPHA13 replacements)

COOP remains the DCIAC / CRATE recovery environment and is not treated as an ordinary IM server deployment merely because the GDPS COOP hostnames use the IM site prefix.

## Patching rule

- The two nodes of each cluster are assigned different patching groups or windows and are never rebooted together.
- COOP and DR are never patched in the same window as PROD.

## Version history

- **v8:** all ten tickets made consistent: N3A addresses derived from the confirmed N3B split; ALPHA6 N6A observations recorded; SR-09/SR-10 placed at DCIAC03 with the HPE Primera 21.4 TB baseline; every node in its own non-overlapping patch window, with DR and COOP never sharing the PROD window; active/active and dual-fabric requirements stated; File Share Witness on a third system; 128 GB memory flagged for ISB approval; DR/COOP replication from PROD stated; hardware inventory, Alpha7/Alpha8 scope note, and ALPHA3 SAN baseline added.
- **v7:** previous controlled set.
