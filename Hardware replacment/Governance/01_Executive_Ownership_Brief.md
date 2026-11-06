# Executive Decision Brief — Alpha Platform Operational Ownership

**Decision requested:** Approve an **immediate** transfer of application-platform operational ownership and coordination to **GIPS Application Support** for the existing Alpha/OpenVMS environment and the Windows-based GDPS replacement program.  
**Audience:** Ravinder Birdi (Managing Director), Sam (CIO), Nadine (IT Operations Chief).  
**Date:** November 6, 2026 | **Status:** Proposed; not yet approved.

## Decision statement
Upon approval, **GIPS Application Support shall be the single accountable operational owner and coordination point for Alpha application-platform activities**, including service requests, server and storage acquisition requests, application configuration, COOP/DR coordination, access-impact reviews, change visibility, incident ownership, and modernization alignment.

**IT Infrastructure** remains responsible for physical installation, compute/storage/network provisioning, operating-system infrastructure and implementation of assigned infrastructure changes. **IT Security** retains security policy, independent security approvals, directory/security-group administration, and enforcement. **Business departments** own business processes, business requirements, workflow rules, acceptance criteria and business validation. They will request assistance through GIPS Application Support rather than independently ordering equipment or initiating platform modifications.

This is a change to **operational governance**, not a redesign of business processing. POLLVAX continues to govern the business behavior ported to APDMS.

## Why immediate
- **Duplicate spending risk:** The Windows replacement procurement is underway while separate requests to replace aging Alpha hardware have also been initiated.
- **Uncoordinated changes:** A security-boundary/group change reportedly affected access without sufficient application support visibility, leading to user login and mapped-drive incidents. The circumstances and authorization require verification.
- **Service accountability gap:** Users report availability/access problems to application support, but relevant infrastructure and security changes may be undertaken elsewhere without timely coordination.

## Executive responsibility diagram

```mermaid
flowchart TD
    LEAD["CIO / Executive Management<br/>Policy and decision authority"]
    APP["GIPS Application Support<br/>Single Alpha platform operational owner<br/>Requests, coordination, incident lead, change visibility"]
    BIZ["Business Department<br/>Business rules, requirements, workflows,<br/>acceptance and validation"]
    INF["IT Infrastructure / Operations<br/>Install, provision and maintain<br/>servers, storage, network and OS"]
    SEC["IT Security<br/>Security policy, approval, enforcement,<br/>directory and boundary changes"]
    LEAD --> APP
    LEAD --> INF
    LEAD --> SEC
    BIZ -->|"Business needs / impact / validation"| APP
    APP -->|"Approved technical work requests"| INF
    APP -->|"Security coordination & impact review"| SEC
    INF -->|"Status, completion, incident notice"| APP
    SEC -->|"Advance notice, approvals, results"| APP
    APP -->|"Business status and service outcomes"| BIZ
```

## Three-layer service ownership diagram — GDPS

The replacement application is named **GIPS Document Processing Service (GDPS)**, also known as the **Alpha Replacement System** (formerly called **Alpha**). **GDPS** is the forward-looking name; `Alpha` is used only when identifying the legacy OpenVMS environment or an established historical interface.

```mermaid
flowchart TB
    subgraph L1["LAYER 1 — APPLICATION / BUSINESS ACCESS"]
       direction TB
       BU["Business units and authorized users<br/>Access GDPS; own business requirements,<br/>rules, workflows and acceptance"]
       APP["GIPS Document Processing Service (GDPS)<br/>AKA Alpha Replacement System<br/>(formerly Alpha)"]
       BU -->|"Application access / business operations"| APP
    end
    subgraph L2["LAYER 2 — APPLICATION PLATFORM"]
       direction TB
       PLATFORM["Windows Server application platform<br/>(replacement for current OpenVMS environment)<br/>GDPS hosting and application runtime"]
       GIPS["GIPS Application Support Department<br/>Platform operational owner<br/>Application configuration, service incidents,<br/>change coordination and platform oversight"]
       GIPS -->|"Manages and coordinates"| PLATFORM
    end
    subgraph L3["LAYER 3 — UNDERLYING INFRASTRUCTURE"]
       direction TB
       INFRA["Physical and virtual compute, storage/disks,<br/>clusters, network, operating-system infrastructure,<br/>data center and COOP/DR infrastructure"]
       IT["GPO IT Infrastructure / IT Operations<br/>Installs, provisions and maintains infrastructure"]
       SECURITY["GPO IT Security<br/>Security policy, identity/boundary controls,<br/>security approval and implementation"]
       IT -->|"Implements and maintains"| INFRA
       SECURITY -->|"Secures and governs"| INFRA
    end
    APP -->|"Runs on"| PLATFORM
    PLATFORM -->|"Hosted by / depends on"| INFRA
```

**Ownership distinction:** Business units use the GDPS application and determine its business requirements; GIPS Application Support manages the application platform and is the single operational coordination point; GPO IT Infrastructure provides and maintains the underlying infrastructure, while GPO IT Security governs and implements applicable security controls. Planned changes affecting GDPS access, drives, service accounts or security boundaries must be coordinated with GIPS Application Support; emergency security action remains within IT Security authority with prompt notice.

**Core rule:** GIPS Application Support is accountable for coordination and application-service outcomes; supporting technical organizations execute their own authorized functions. No technical approval, emergency security authority, or segregation-of-duties control is bypassed.

## Immediate leadership directions proposed
1. Designate GIPS Application Support the Alpha platform point of entry for **all new legacy and replacement environment requests**, effective upon authorization.
2. Direct business units to **stop independently initiating Alpha hardware purchases, storage changes or security/configuration requests**; route them through Application Support. Review existing orders individually rather than cancelling automatically.
3. Reconcile existing Alpha maintenance/replacement requests with the GDPS Windows procurement program and identify duplicate or unnecessary expenditure before further commitments.
4. Direct IT Infrastructure and IT Security to notify and coordinate **planned Alpha-impacting changes** with Application Support before implementation, with documented exceptions for urgent security incidents and mandatory controls; communicate emergency actions promptly.
5. Establish a current inventory of Alpha service accounts, security groups/boundaries, access paths, dependent drives/shares, COOP/DR obligations, and service-request owners.
6. Approve the detailed operating model, fill role-based contacts and announce the ownership decision to all stakeholders.

## Existing replacement baseline
The hardware library states **10 physical Windows servers**, arranged in five two-node clusters for **TEST, PROD, DR, COOP IM, and COOP HQ**. **DEV** is a separate virtual-server replacement. The authoritative request set is in `Hardware replacment/07 Server Requests/v8 10-Node Physical Server Tickets/`; the controlled-document register governs procurement. This governance change covers **the existing Alpha system immediately**, not only the future Windows environment.

## Approval record
- Managing Director, Ravinder Birdi — Decision/endorsement: **[Pending]**
- CIO, Sam — Authorization: **[Pending]**
- IT Operations Chief, Nadine — Infrastructure operations acknowledgment: **[Pending]**
- GIPS Application Support platform lead — Named owner: **[To assign]**
- Effective timestamp and communication record: **[Pending]**

See [Detailed Operating Model](02_Detailed_Operating_Model.md) and [Contacts Matrix](03_Contacts_and_Responsibility_Matrix.md).
