# GDPS 10-Ticket Placement and Replacement Matrix

This matrix is the authoritative placement, replacement, and existing-network traceability reference for the ten GDPS physical-server ServiceNow requests.

The deployment follows the existing Alpha setup. TEST is the only new physical cluster. PROD, DR, and COOP preserve the existing physical replacement relationships and site model.

| Ticket | New GDPS Node | Environment | New Node Location | Existing Alpha System | Existing Node Replaced | Existing Alpha DNS / IP Traceability | Replacement Status |
|---|---|---|---|---|---|---|---|
| SR-01 | HQVMGDPSFST1 | TEST | HQ | None | N/A | N/A | New TEST node; no existing Alpha replacement |
| SR-02 | HQVMGDPSFST2 | TEST | HQ | None | N/A | N/A | New TEST node; no existing Alpha replacement |
| SR-03 | HQVMGDPSFSP1 | PROD | HQ | ALPHA3 | N3A | alpha3.gpo.gov: 172.16.35.16, 172.16.35.15, 172.16.35.20, 172.16.35.19 | Direct physical replacement |
| SR-04 | HQVMGDPSFSP2 | PROD | HQ | ALPHA3 | N3B | N3B: 172.16.35.19 (IE2, primary), 172.16.35.20 (IE3); cluster alias alpha3.gpo.gov | Direct physical replacement |
| SR-05 | IMVMGDPSFSD1 | DR | IM | ALPHA6 | N6A | alpha6.gpo.gov: 172.19.128.44, 172.19.128.43, 172.19.128.42, 172.19.128.41 | Direct physical replacement |
| SR-06 | IMVMGDPSFSD2 | DR | IM | ALPHA6 | N6B | alpha6.gpo.gov: 172.19.128.44, 172.19.128.43, 172.19.128.42, 172.19.128.41 | Direct physical replacement |
| SR-07 | IMVMGDPSFSC1 | COOP | DCIAC02 / Data Center in a Crate | ALPHA10 (COOP / DCIAC02) | ALPHA11 | alpha11.gpo.gov: 172.23.5.42, 172.23.5.43 | Direct physical COOP replacement |
| SR-08 | IMVMGDPSFSC2 | COOP | DCIAC02 / Data Center in a Crate | ALPHA10 (COOP / DCIAC02) | ALPHA12 | alpha12.gpo.gov: 172.23.5.45, 172.23.5.44 | Direct physical COOP replacement |
| SR-09 | IMVMGDPSFSC3 | COOP | DCIAC / Data Center in a Crate | ALPHA13 | N13A | alpha13.gpo.gov: 172.23.6.43, 172.23.6.42, 172.23.6.45, 172.23.6.44 | Direct physical COOP replacement |
| SR-10 | IMVMGDPSFSC4 | COOP | DCIAC / Data Center in a Crate | ALPHA13 | N13B | alpha13.gpo.gov: 172.23.6.43, 172.23.6.42, 172.23.6.45, 172.23.6.44 | Direct physical COOP replacement |

## Network traceability note

The IP addresses above are the current DNS A-record results captured from the GPO network for the existing Alpha names. They are retained for migration and replacement traceability.

They are **not** assignments or reservations for the new GDPS servers. New GDPS IP addresses, DNS records, VLANs, and related network values remain subject to GPO Network/Security assignment.

For ALPHA3, the DNS sweep alone returned the cluster/service address set. Subsequent node-level verification established N3B as 172.16.35.19 (IE2, primary) and 172.16.35.20 (IE3), with alpha3.gpo.gov retained as the cluster alias. N3A remains at cluster-level traceability until separately verified. For ALPHA6 and ALPHA13, the DNS command still does not establish the individual A/B node split, so their full source-cluster address sets are retained rather than inventing node-specific assignments.

ALPHA11 and ALPHA12 resolve independently and therefore their returned addresses are recorded directly against their corresponding COOP replacement tickets.

## DNS discovery command retained for safekeeping

The following PowerShell command was run from the GPO network to capture the current Alpha DNS A records:

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

ALPHA0, ALPHA1, and ALPHA2 are retained in the captured command output for evidentiary completeness, but they are not part of this physical-server request set because ALPHA0 is being replaced by the separate GDPS DEV virtual-server design.

## Physical-server count

- TEST: 2 new physical nodes
- PROD: 2 replacement physical nodes
- DR: 2 replacement physical nodes
- COOP: 4 replacement physical nodes
- Total: **10 physical GDPS server requests**

## Placement rule

- TEST: HQ
- PROD: HQ
- DR: IM
- COOP: DCIAC / Data Center in a Crate

COOP remains the DCIAC / CRATE recovery environment and is not treated as an ordinary IM server deployment merely because the GDPS COOP hostnames use the IM site prefix.

## Confirmed Alpha topology correction

- **ALPHA10 is the COOP cluster in DCIAC02.**
- ALPHA11 and ALPHA12 are the two ALPHA10 COOP nodes.
- SR-07 and SR-08 therefore replace the existing **ALPHA10 / DCIAC02 COOP** physical nodes one-for-one.
- N3B node-level network traceability is confirmed as **172.16.35.19 (IE2, primary)** and **172.16.35.20 (IE3)**; `alpha3.gpo.gov` is the cluster alias.
