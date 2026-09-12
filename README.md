# JFXAI4BPM + JFXAI4MOMS

## Oceanic Mining, Business Process Simulation and Operations Integration

**Architecture proposal · Revision 1.0 · 12 September 2026**

**Deliverables:** this English consolidation and the companion `jfxai4bpm_jfxai4moms_oceanic_integration.drawio`, containing seven editable architecture views.

**Status:** a source-grounded target architecture and implementation backlog. This package does not contain deployed services, executable BPMN, a validated subsea simulator, operating permits, or evidence of physical-system certification. No changes have been committed to either GitHub repository.

## 1. Executive architecture decision

Integrate **JFXAI4MOMS as the mining-domain system of record** within the **JFXAI4BPM multi-domain process and simulation control plane**. Retain JFXAI4MOMS's terrestrial mining and geological capabilities; add an oceanic operating context rather than replacing the existing domain. Retain the other domains already described by JFXAI4BPM.

JFXAI4BPM coordinates cases, approvals, cross-domain workflows, scenarios and process analytics. JFXAI4MOMS owns mining assets, geology, marine missions, material genealogy, environmental observations and mining work orders. Physical equipment remains under independent, locally governed operational-technology (OT) control. The connection uses versioned APIs, events and domain adapters—not a shared operational database.

The first delivery target is **survey-to-evidence in simulation**, followed by supervised shadow operation. Extraction, construction and export are later, separately authorized capabilities. A successful simulation is not permission to operate.

## 2. Verified source baseline

The GitHub snapshots reviewed on 11 September 2026 contain README reference architectures and diagrams/images. Their inspected trees do not contain an application source tree, dependency manifest, deployment package or automated test suite. Therefore, capabilities below are classified as **documented**, **proposed extension**, or **future implementation**, not assumed to be working integrations.

| Repository | Reviewed main-branch commit | Verified architectural direction | Integration implication |
|---|---|---|---|
| JFXAI4BPM | `36a10248e0159deb922700d62f813219197a731e` | Multi-domain orchestration, canonical process/event/command/query contracts, simulation isolation, replaceable engines, process twins and governance | Add a mining domain and adapters without changing existing domain ownership |
| JFXAI4MOMS | `736b4ec3e4b0a27fcc52cc2c6078536c51d2265a` | OpenTwin conceptual core, geology/GIS, mine operations, fleet, subsea exploration, environmental evidence and simulation references | Make its mining records authoritative; expand its subsea business lifecycle |

Sources: [JFXAI4BPM pinned README](https://github.com/robotics-intelligent-systems/jfxai4bpm/blob/36a10248e0159deb922700d62f813219197a731e/README.md), [JFXAI4MOMS pinned README](https://github.com/robotics-intelligent-systems/jfxai4moms/blob/736b4ec3e4b0a27fcc52cc2c6078536c51d2265a/README.md). Repository contents: [BPM snapshot](https://github.com/robotics-intelligent-systems/jfxai4bpm/tree/36a10248e0159deb922700d62f813219197a731e), [MOMS snapshot](https://github.com/robotics-intelligent-systems/jfxai4moms/tree/736b4ec3e4b0a27fcc52cc2c6078536c51d2265a).

The MOMS snapshot already includes an [amphibious mechatronic underwater-infrastructure diagram](https://github.com/robotics-intelligent-systems/jfxai4moms/blob/736b4ec3e4b0a27fcc52cc2c6078536c51d2265a/MBSE/CAS/amphibious_mechatronic_underwater_infrastructure.drawio) and a [MineSim architecture diagram](https://github.com/robotics-intelligent-systems/jfxai4moms/blob/736b4ec3e4b0a27fcc52cc2c6078536c51d2265a/MBSE/CAS/architecture-of-minesim-simulation-testing-system.drawio). These are conceptual references, not proof of vehicle performance or a running simulator.

“OpenTwin” below denotes the conceptual registry/core described by JFXAI4MOMS; it does not assert a particular installed third-party product. The inspected repository roots did not contain a license file; licensing and third-party terms must be resolved before redistribution or deployment. Public source visibility alone is not a verified open-source license.

### 2.1 Preserve, extend and implement

| Preserve from the sources | Add in this proposal | Must still be implemented and verified |
|---|---|---|
| BPM domain ownership and canonical contracts | `oceanic_mining` domain registration and MOMS adapter | Service endpoints, schemas, adapter code and conformance tests |
| BPM simulation registry and process twins | Coupled campaign, environmental, physical and economic scenarios | Calibrated models, co-simulation harness and validation evidence |
| MOMS geology, fleet, environment and OpenTwin model | Campaigns, marine authorization cases, subsea work packages and material custody | Domain transactions, data pipelines and access controls |
| MOMS subsea and amphibious concept diagrams | Business lifecycle for inspection, sampling, repair and modular construction | Qualified hardware, operating procedures and independent acceptance |
| Existing portfolio and optional technology compendia | Explicit cross-domain contracts and release gates | Each external adapter and its owner's approval |

## 3. Scope and non-goals

Included: oceanographic/geological surveys; sample and assay traceability; environmental baseline evidence; campaign simulation; vessel/ROV/AUV readiness; supervised subsea inspection and mechatronic work; maintenance; modular infrastructure fabrication and acceptance; conditional extraction/processing workflows; port handoff; energy and material accounting; business-process KPIs; audit and training evidence.

Excluded from this software architecture: hull or pressure-vessel design, flight or weapon systems, equipment operating envelopes, autonomous extraction authorization, legal permission to mine, certified mineral-reserve statements, and invented production costs. Earlier vehicle and commodity estimates are not adopted as verified inputs. Every physical configuration and operational activity requires its own engineering and authorization basis.

No jurisdiction, operating depth, deposit type, extraction technique, rated production, budget, commodity price or project schedule is assumed. These are versioned scenario inputs with an owner and evidence status.

## 4. Logical architecture and authority

| Layer | Responsibilities | Authoritative records | Forbidden shortcut |
|---|---|---|---|
| Experience | Process designer, GIS/twin viewer, simulation workspace, operations and assurance cockpits | User preferences and saved views only | Treat a visual status as operational approval |
| JFXAI4BPM control plane | Process/case definitions, instances, decisions, human tasks, timers, sagas, scenario orchestration, process mining | Process state, workflow approvals, scenario manifests and orchestration audit | Direct equipment control or independent editing of mining inventory |
| Integration boundary | Authentication, command validation, event normalization, schema compatibility, outbox/inbox, read projections | Delivery/deduplication records and adapter configuration | Shared credentials, shared operational tables or hidden dual writes |
| JFXAI4MOMS domain | Geology, campaigns, mission readiness, mining work orders, environmental observations, lots, energy measurements, OpenTwin | Mining-domain facts and permitted state transitions | Accept a process approval without checking current domain conditions |
| Simulation workers | Discrete-event, system-dynamics, physical, geological, environmental and valuation models | Immutable run artifacts, provenance and uncertainty outputs | Production credentials or mutation of live records |
| OT/edge boundary | Telemetry acquisition, local command admission, operator supervision and independent interlocks | Device/controller state and local safety actions | Depend on BPM, a cloud connection or an LLM for immediate safety |
| Assurance and analytics | Evidence catalog, model governance, security, KPI projections and independent review | Signed review decisions; non-authoritative analytical projections | Reclassify forecasts as measurements or self-certify operational readiness |

MOMS may retain internal domain workflows. BPM owns cross-domain orchestration; each transition has one designated owner. A fleet maintenance case in BPM references a MOMS work order instead of creating a second competing maintenance state machine.

## 5. Portfolio integration without domain replacement

The following mappings extend the portfolio already documented in the [BPM source](https://github.com/robotics-intelligent-systems/jfxai4bpm/blob/36a10248e0159deb922700d62f813219197a731e/README.md). External repositories other than the two baseline repositories were not independently inspected for this package; their integrations remain candidates.

| Domain / proposed source | Oceanic-mining interaction | Boundary |
|---|---|---|
| Mining / `jfxai4moms` | Campaigns, geology, marine assets, work orders, monitoring and lots | Mining facts and domain decisions stay in MOMS |
| Microfactory / `jfxosms` | Fabrication, repairable assemblies, serialized modules and inspection evidence | Manufacturing owner releases conformity; MOMS accepts installation |
| Procurement / `jfxai4ohs` | Requisitions, supplier responses, spare parts and shipment references | Commercial order stays with procurement |
| Fleet / `fleet-management` | Road transport from port to warehouse/processor | Land-fleet scheduling is not subsea control |
| Learning / `jfxlms` | Training assignments, simulator exercises and competence evidence | Training completion is not operating authorization |
| Collaboration / `jfxcms` | Requirements, change requests, reviews and engineering evidence | Versioned engineering artifacts, not fleet dispatch |
| Recruitment / `jfxai4rts` | Approved staffing requests and role qualifications | Transfer minimum job-relevant data only |
| Strategy / `jfxbsc` | Process, energy, material and environmental KPI projections | Read-only metrics; does not edit operational records |
| Open banking / `jfxai4obs` | Optional approved financial handoffs after verified contractual events | No automatic settlement in the MVP |
| Trading / `jfxai4ats` | Optional price-scenario input or risk analysis | No autonomous trades or assumed liquidity |
| Travel / `jfxotbs`; hospitality / `jfxai4crm` | Optional crew travel and accommodation coordination | Administrative travel is not marine mission dispatch |
| Other existing domains | Farms, restaurants, tourism/social capabilities and contests remain registered | No mining-related access to unrelated personal data |

### 5.1 Proposed domain registration

```yaml
domain:
  id: oceanic_mining
  source_repository: robotics-intelligent-systems/jfxai4moms
  system_of_record: jfxai4moms
  adapter: moms_oceanic_v1
  process_owner: jfxai4bpm
  domain_owner_role: mining_operations_owner
  contexts: [terrestrial, marine_survey, subsea_infrastructure, oceanic_mining]
  modes: [SIMULATE, SHADOW, HIL, LIVE]
  default_mode: SIMULATE
  automation_enabled: false
  required_gates: [data_quality, model_review, domain_authority]
```

This entry is additive to the existing registry. `automation_enabled: false` is the safe initial configuration; future live enablement is per process, scope and identity, not one portfolio-wide switch.

## 6. Oceanic business-process catalog

All process definitions are versioned. Long-running marine activities use explicit deadlines, cancellation/recovery paths and evidence-based completion. A generic business approval does not replace an activity-specific permit, competent operator or equipment readiness assessment.

| ID / process | Trigger and principal steps | Required evidence / completion | Exceptions |
|---|---|---|---|
| P01 Campaign-to-authorized-plan | Proposal → area/activity scope → baseline and authorization review → scenario comparison → campaign approval | Scope, dates, evidence references and approved plan revision | Missing/expired authority, data gap or rejected scenario → hold/rework |
| P02 Survey-to-geological-evidence | Survey request → readiness → mission → observations/samples → QA/QC → geological review | Georeferenced observations, custody, assay revision and reviewed interpretation | Position uncertainty, contamination or QA failure → quarantine/re-survey |
| P03 Mission-to-evidence | Approved work package → reserve assets/crew → readiness recheck → supervised dispatch → monitor → recover → close | Domain acceptance, mission log, asset state and recovery evidence | Weather/data freshness/health change → reassess or local safe response |
| P04 Sample-to-assay | Collect → identify/seal → custody transfers → laboratory receipt → QA/QC → accept/reject result | Sample lineage, method, units, QA status and qualified review | Broken custody, duplicate ID or failed control → quarantine |
| P05 Authorized-pilot-to-reconciled-lot | Separately authorized pilot → bounded work package → recovery → weighing/moisture → assay/processing → lot reconciliation | Activity-specific authority, mass basis, recovery evidence and reconciled genealogy | Exceedance, loss, grade uncertainty or imbalance → stop/hold investigation |
| P06 Subsea-work-order-to-acceptance | Inspect → specify repair/construction → simulate work sequence → review → execute under local control → inspect → accept | Tool/module compatibility, serialized parts, work evidence and as-built twin revision | Non-conformance → isolate/rework; physical work is not rolled back by a saga |
| P07 Condition-to-return-to-service | Health event → triage → work order → spares/fabrication → repair → independent checks → release | Maintenance records and designated technical sign-off | Failed acceptance → asset remains unavailable |
| P08 Environmental-alert-to-case-closure | Threshold or quality alert → evidence capture → local response + process hold → investigation → authorized disposition | Observation provenance, applicable rule version, corrective action and review | Unknown/stale data is not a normal reading; reopening needs explicit approval |
| P09 Lot-to-port-handoff | Released lot → custody manifest → capacity/reservation → shipment → receipt reconciliation | Qualified quantity/grade basis, custody, commercial and authorization checks | Lost custody, mismatch or invalid authorization → shipment hold |
| P10 Energy-period-to-reconciliation | Meter period close → quality checks → balance → allocation → review | Meter boundaries, signed convention, uncertainty and allocation rule | Missing meter data or double-counted transfer → provisional period |
| P11 Module-design-to-series-release | Requirements → design baseline → procurement/fabrication → first article → lot/serial production → QA → delivery | Configuration/BOM revision, serial genealogy, inspection and MOMS acceptance | Material substitution/change → technical review before release |
| P12 Campaign-closeout-to-monitoring | Recover assets → reconcile samples/lots/energy → obligations review → monitoring handoff → archive | Open-obligation register, evidence package and continuing monitoring owner | Unclosed environmental or maintenance cases remain active |

### 6.1 Representative orchestrated lifecycle

The principal case is `oceanic_campaign_to_evidence`: P01 opens a campaign; P02/P04 establish reviewed evidence; scenario analysis feeds a human decision. P03 can authorize a specific survey or inspection work package only after MOMS rechecks the current domain conditions. P05 requires its own authorization and is not automatically unlocked by a survey approval. P06, P07 and P11 share assets and engineering evidence but have independent acceptance gates. P08 is active throughout; P09 follows reconciled and released lots; P10 and P12 close the accounting/evidence loop.

The Draw.io process page is an architecture-level workflow view, **not executable or BPMN-conformance-tested XML**. Executable process interchange should target a selected engine profile and [OMG BPMN 2.0.2](https://www.omg.org/spec/BPMN/2.0.2/), with separately tested mappings for user tasks, timers and compensation.

### 6.2 Saga and compensation rules

Reservations can be released, work requests canceled before acceptance, and purchase requests amended subject to their owning system's rules. A timed-out response does not prove that a mission command failed: query the existing command ID before retrying. After physical execution, compensation means a new recovery, inspection, reconciliation or remediation case—not reversing telemetry, deleting a sample or pretending material returned to the seabed.

## 7. OpenTwin and domain data model

Extend the source's twin registry, asset graph, state/history/events and provenance model. Do not collapse a measured physical state, a planned state and a simulated state into one mutable field. The inherited model is described in the [MOMS OpenTwin section](https://github.com/robotics-intelligent-systems/jfxai4moms/blob/736b4ec3e4b0a27fcc52cc2c6078536c51d2265a/README.md#opentwin-mining-model).

| Entity group | Proposed records and relationships | Essential controls |
|---|---|---|
| Campaign and authority | `Campaign`, `OperatingArea`, `ActivityAuthorization`, `WorkPackage`; scope and validity references | Activity, jurisdiction/context, geometry, validity interval, conditions, evidence hash and reviewer |
| Geological evidence | `Survey`, `Sample`, `CustodyTransfer`, `Assay`, `GeologicalModelRevision` | Coordinate reference system, vertical datum, units, uncertainty, methods and QA/QC |
| Marine assets | `SurfaceVessel`, `ROV`, `AUV`, optional `AmphibiousPlatform`, `Manipulator`, `Tool`, `Sensor` | Configuration/version, compatibility, readiness, calibration and technical limits by reference |
| Modular infrastructure | `Module`, `Interface`, `Installation`, `Inspection`, `AsBuiltRevision` | Serial identity, engineering baseline, location, installation evidence and acceptance status |
| Operations and maintenance | `Mission`, `WorkOrder`, `Reservation`, `ReadinessAssessment`, `MaintenanceRelease` | One authoritative lifecycle; approved revision and current asset conditions |
| Environment | `BaselineDataset`, `Observation`, `QualityFlag`, `RuleSet`, `Alert`, `EnvironmentalCase` | Spatial/temporal coverage, freshness, detection limits, calibration and responsible reviewer |
| Materials | `MaterialLot`, `Transformation`, `Stockpile`, `Shipment`, `CustodyTransfer` | Wet/dry basis, assay revision, parent-child genealogy and reconciliation status |
| Energy | `Meter`, `EnergyInterval`, `StorageState`, `Allocation`, optional `AttributeCertificateRef` | Physical boundary, period, source/quality, no double counting and separate certificate ownership |
| Digital evidence | `ModelVersion`, `ScenarioRunRef`, `Approval`, `EvidenceArtifact`, `ProcessInstanceRef` | Content hash, access scope, provenance and immutable supersession links |

Common keys: `tenant_id`, `campaign_id`, immutable entity ID, domain version, event time, ingestion time and evidence references. Spatial data must identify horizontal CRS, vertical datum, depth/elevation sign convention and positional uncertainty. Time series identify units, calibration and quality; a missing value is not zero.

Large sonar, video, GIS and model files remain in governed object storage. Events carry bounded metadata and authorized artifact references, not bulk payloads or embedded access secrets. BPM stores references and minimal read projections; MOMS remains the owner of domain facts. Retention and access policies are defined for observations, personnel information, commercially sensitive geology and audit evidence separately.

## 8. API and event integration contract

### 8.1 Proposed interfaces—not existing endpoints

| Interface | Owner / purpose | Required behavior |
|---|---|---|
| `POST /v1/process-instances` | BPM: start a versioned business process | Validate domain/scope/mode; return process ID |
| `POST /v1/simulation-runs` | BPM simulation coordinator: queue an immutable run manifest | Return run ID and asynchronous status location |
| `GET /v1/simulation-runs/{id}` | BPM: read status and result references | Distinguish completed, canceled, invalid and failed runs |
| `GET /v1/campaigns/{id}` | MOMS: authorized campaign projection | Include revision, freshness and domain status |
| `GET /v1/twins/{id}` | MOMS: scoped state/evidence projection | Mark measured, estimated and planned fields separately |
| `POST /v1/commands` | MOMS: request an allowed domain transition | Authenticate caller; validate expected version, idempotency, scope, expiry and approvals |
| `GET /v1/commands/{id}` | MOMS: inspect accepted/rejected/running/completed/failed outcome | Acceptance is not physical completion |
| Event subscription | Domain outbox → broker → BPM/analytics inbox | At-least-once delivery; consumer deduplication and bounded replay |

No public hostname or authentication scheme is implied by these relative routes. OpenAPI/AsyncAPI artifacts, scopes, schemas, error codes and retention policy are backlog items.

### 8.2 Canonical event profile

Preserve BPM's canonical envelope through a compatibility adapter. Use a CloudEvents 1.0-compatible envelope for new integrations: required identity/source/type/spec-version attributes, time and subject when applicable, and an application-owned data schema. The profile and extensions below are proposed, not fields already supplied by either repository. [CloudEvents specification, v1.0.2](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md).

```json
{
  "specversion": "1.0",
  "id": "evt-demo-0001",
  "source": "urn:jfxai4moms:demo:marine-operations",
  "type": "org.ris.moms.mission.completed.v1",
  "subject": "missions/mission-demo-001",
  "time": "2026-09-11T12:00:00Z",
  "datacontenttype": "application/json",
  "dataschema": "urn:ris:schema:moms:mission-completed:1",
  "tenantid": "demo",
  "correlationid": "campaign-demo-001",
  "causationid": "cmd-demo-0001",
  "executionmode": "SIMULATE",
  "data": {
    "campaign_id": "campaign-demo-001",
    "process_id": "proc-demo-001",
    "mission_id": "mission-demo-001",
    "entity_version": 7,
    "evidence_status": "synthetic",
    "scenario_run_id": "run-demo-001",
    "evidence_refs": ["urn:demo:evidence:mission-log-001"]
  }
}
```

Example only; IDs, time and evidence are synthetic. `executionmode` is routing metadata, not an authorization mechanism. Broker permissions and separate identities enforce isolation independently.

| Existing BPM field | Proposed mapping | Migration rule |
|---|---|---|
| `event.id`, `type`, `source`, `occurred_at` | `id`, namespaced `type`, URI `source`, `time` | Preserve original identifiers and source metadata in the adapter audit |
| `correlation_id` | `correlationid` | Keep correlation distinct from causation |
| Structured `subject` | String `subject` plus domain reference in `data` | No loss of entity type or ID |
| `domain`, `data` | Domain routing/profile metadata and `data` | Version payload schemas; do not break existing consumers |
| Process `simulation` boolean | Compatibility projection of richer execution mode | Existing simulated instances stay isolated; do not infer LIVE from an absent flag |

### 8.3 Event and command semantics

The MOMS README already gives events such as `sample.assay.received`, `auv.mission.started`, `maintenance.required` and `environmental.threshold.exceeded`. Map these to a new envelope without claiming the new namespace is already implemented. [MOMS data/event architecture](https://github.com/robotics-intelligent-systems/jfxai4moms/blob/736b4ec3e4b0a27fcc52cc2c6078536c51d2265a/README.md#data-and-event-architecture).

| Event fact / proposed new type suffix | BPM reaction | Allowed command and owner |
|---|---|---|
| Existing `sample.assay.received` / `sample.assay.received.v1` | Open QA/review task | Request assay review in MOMS; never overwrite a laboratory result |
| Existing `auv.mission.started` / `mission.started.v1` | Update monitoring case | Query MOMS status; do not treat event as permission for another mission |
| Existing `maintenance.required` / `maintenance.required.v1` | Create/associate maintenance case | `RequestMaintenanceWorkOrder` in MOMS |
| Existing `environmental.threshold.exceeded` / `environmental.threshold.exceeded.v1` | Record alert, hold dependent business steps, escalate | `RequestOperationalHold` in MOMS; immediate physical response remains local |
| New `simulation.run.completed.v1` | Compare validated scenario results | Create human review task in BPM |
| New `material.lot.reconciled.v1` | Check release and shipment prerequisites | `RequestShipmentPreparation` in the owning domain |
| New `infrastructure.installation.accepted.v1` | Close accepted work-package stage | Refresh projections; no independent twin rewrite |
| New `energy.period.reconciled.v1` | Publish qualified metrics | Refresh BSC projection; no certificate creation implied |

Full MOMS event types use `org.ris.moms.`; simulation coordinator events use `org.ris.bpm.`. A fact is immutable; corrections issue a new event with a supersession reference.

Every command carries `command_id`, `idempotency_key`, target, actor, process/correlation IDs, execution mode, expected entity version, approved work-package revision, expiration and evidence references. The authenticated gateway supplies tenant/scope; it does not trust caller-supplied identity fields. Replay after expiry or against a changed plan is rejected. A duplicate key with a different payload is a conflict; an identical retry returns the original command outcome.

Use a transactional outbox at the record owner and a durable inbox per consumer. Ordering is per domain aggregate, not global. Consumers handle duplicates, out-of-order versions, schema evolution and late telemetry. Retry transient transport failures with bounds; route persistent failures to a dead-letter workflow. Never promise exactly-once physical execution from a message broker. Retain deduplication records through the maximum supported replay window.

## 9. Simulation architecture

JFXAI4BPM owns run orchestration and comparison; MOMS supplies governed snapshots and domain model references. A process twin models workflow state, queues and resources; an asset/environment twin models relevant physical or observed state. They are linked by IDs and time mappings, not assumed to be the same model.

### 9.1 Model responsibilities

| Model class | Oceanic question | Inputs / outputs | Validation boundary |
|---|---|---|---|
| Discrete-event simulation | Can campaigns, maintenance, laboratories and port handoffs meet demand? | Calendars, task distributions and resource constraints → lead time, queues, utilization, throughput | Land-mine dispatch models may inform structure, not validated subsea performance |
| System dynamics | How do capacity, maintenance backlog, workforce and energy constraints evolve? | Aggregated stocks/flows and policies → medium/long-horizon scenarios | Does not replace task-level dispatch or physical dynamics |
| Physical / FMU adapter | How do modeled equipment and energy limits affect work-package feasibility? | Reviewed equipment/environment models → bounded response and resource estimates | Requires qualified models and numerical checks; no operational limits invented here |
| Geology / uncertainty ensemble | How sensitive are plans to sampling and interpretation uncertainty? | Versioned evidence and hypotheses → scenario distributions | No automatic conversion from model output to certified reserves |
| Environmental model adapter | What monitoring/impact uncertainties constrain the campaign? | Baseline, quality/freshness, boundary conditions → reviewed scenario outputs | Model plausibility is not proof of environmental acceptability |
| Economic / resource-accounting model | How do yield, energy, availability and valuation assumptions affect options? | Reconciled/synthetic ledgers and price scenarios → ranges and sensitivities | Separate accounting identities from forecasts and real quotations |

FMI is an interface for model exchange/co-simulation, not a guarantee of model validity. Declare the exact supported FMI version, interface type, platform and capabilities for each FMU; reject incompatible combinations. The [FMI 3.0.2 specification](https://fmi-standard.org/docs/3.0.2/) is a reference profile, not a claim that either repository already implements it.

### 9.2 Run manifest and execution

A run manifest records scenario/run IDs; purpose; execution mode; process, rule and model versions; container/artifact hashes; input snapshot IDs and hashes; calibration/validation status; units/CRS; simulated epoch/horizon; step policy; replication count and seeds; solver tolerances; hardware/platform profile; failure/cancellation policy; and requested outputs. All values must be supplied or explicitly defaulted by a reviewed scenario template.

The coordinator checks compatibility, snapshots inputs, starts workers, tracks progress, stores results and emits completion/failure events. Large runs are asynchronous and cancellable. Partial or invalid results cannot silently enter the approved comparison set. Identical runs should be reproducible within declared numerical tolerance; stochastic models report replication uncertainty, and nondeterministic solvers must disclose their limits.

For coupled runs, explicitly map DES events to the physical model's simulation clock, define synchronization points and unit conversions, and state the handling of discontinuities, latency, failed workers and early stop. Conservation checks and step-size/convergence tests precede decision use. Land-based models in the MOMS compendium remain research inputs until marine calibration is demonstrated.

### 9.3 Separate modes and promotion gates

| Mode | Data and credentials | Permitted outputs | Exit gate |
|---|---|---|---|
| SIMULATE | Synthetic or authorized immutable snapshots; isolated credentials, topics and stores | Scenario artifacts and synthetic domain events only | Model/data review and contract/isolation tests |
| SHADOW | Approved read-only copy of operational data; its own identities and topics | Comparisons and recommendations; no operational commands | Evidence of alignment, drift/freshness handling and operator review |
| HIL | Controlled hardware-in-the-loop test bench with dedicated test authority | Test-bench effects only; no field deployment | Independent bench acceptance and safety/security review |
| LIVE | Scoped production identities, explicit activity authority and current readiness | Accepted domain requests through the supervised OT boundary | Continuous monitoring, audit and controlled change management |

SHADOW is not a production command channel. HIL is not a field environment. Promotion approves a versioned release/configuration; it never replays synthetic events or transfers simulation command credentials into LIVE. Production telemetry may feed a sanitized, read-only mirror; no reverse write route exists.

## 10. Mechatronics and modular subsea infrastructure

Extend the existing amphibious/mechatronic concept at the work-package and evidence level. Relevant jobs include inspection, sampling, manipulation, component exchange, repair and installation of modular infrastructure. Excavation or extraction is a distinct activity type with its own authorization; a general manipulator capability does not grant it.

| Capability | MOMS responsibilities | BPM responsibilities | Acceptance evidence |
|---|---|---|---|
| Manipulation and sampling | Tool/asset compatibility and domain work-package lifecycle | Crew, sample/laboratory and reservation coordination | Tool identity, operator log, sample custody and inspection |
| Repair and component exchange | Defect, asset configuration, maintenance and technical release | Spares/procurement/fabrication and approval tasks | Replaced serial IDs, checks and approved return to service |
| Modular construction | Installation plan reference, interfaces and as-built twin | Module production, shipment, work sequence and acceptance case | Fabrication release, installation inspection and final configuration |
| Amphibious deployment option | Configuration-specific readiness and environmental constraints | Transport and recovery readiness cases | Qualified configuration and deployment/recovery evidence |

Industrial alternatives must be assessed for the intended environment and function. “High strength” and “open architecture” do not establish subsea suitability. Substitution reviews cover material traceability, corrosion/compatibility, sealing, electrical and pressure/environmental qualification, maintainability, supplier data and safety relevance. This document provides no design ratings or interchangeability claim.

Series production is modeled through design/BOM revisions, first-article acceptance, lot and serial genealogy, calibrated inspection, non-conformance, supplier changes and configuration-controlled release. MOMS links installed serials to their manufacturing evidence; BPM coordinates the manufacturing owner rather than becoming an MES.

## 11. Energy, minerals and resource-equivalent valuation

Use **three separate ledgers**: (1) material quantities and custody, (2) energy measurements/allocations, and (3) scenario valuation. A fourth optional register tracks energy/environmental certificates; it must not be confused with physical production. No live metal price or forecast cost is asserted here.

### 11.1 Physical accounting

For an explicitly defined material boundary and period:

`opening_stock + receipts + production = shipments + consumption + measured_losses + closing_stock + residual`

Record wet/dry basis and uncertainty consistently. Internal transformations use paired consumption/production entries; internal transfers cancel when consolidating the boundary. Moisture fraction `w` on a wet-mass basis gives `dry_mass = wet_mass × (1 − w)`. For a hypothetical feed and metal `i`, `contained_metal_i = dry_feed_mass × grade_i`; forecast recovered metal multiplies this by a recovery fraction. Recovered product mass and contained metal are different quantities. Laboratory results, processing measurements and model forecasts retain separate evidence labels.

For electricity within one declared metering boundary and interval, with storage state change positive when stored energy increases:

`generated + imported = process_use + auxiliaries + exported + losses + storage_increase + residual`

Storage discharge appears as a negative storage increase in this convention; do not count it again as primary generation. Keep fuel input and electricity output as distinct carrier accounts before any efficiency conversion. A reconciliation residual carries measurement uncertainty and is investigated against a configured tolerance; it is not silently classified as a loss.

### 11.2 Commodity and energy equivalence—not purchasing power parity

Commodity-equivalent accounting is **not macroeconomic purchasing power parity (PPP)**. It expresses one scenario value in a selected reference commodity or energy unit. It does not establish barter availability, financeability, domestic affordability or the feasibility of manufacturing aerospace/subsea components from raw metal.

If a scenario cost `C` and a reference price `P_i` use the same valuation date, currency basis and delivery/quality basis, then `equivalent_quantity_i = C / P_i`. Likewise, `equivalent_MWh = C / P_energy`. Monetary values can remain internal scenario inputs while the user-facing output displays tonnes or MWh. Without a common valuation basis or agreed exchange ratios, unlike commodities cannot be added into a meaningful total.

Net realizable export value is a separate scenario: gross payable product value minus explicitly defined processing/refining, transport, insurance and other applicable charges/obligations. Store quantity, grade, payability, recovery, quality penalties, settlement terms and assumptions separately. Do not substitute gross in-situ resource value for export revenue or free cash flow.

Steel and aluminum have grade/product-dependent prices; copper feed, concentrate and refined copper are not the same product. Carbon fiber and finished composites are manufactured materials, not mineral export categories; include processing, resin, layup, yield, qualification and manufacturing labor in a fabrication scenario. Do not sum “copper-equivalent tonnes” and “steel-equivalent tonnes” as independent sources of value: they are alternative denominations of the same scenario.

### 11.3 Decision metrics and BSC projections

| Metric | Definition / owner | Required qualification |
|---|---|---|
| Campaign lead time | Approved process start to accepted closeout / BPM | Calendar, pause policy and process version |
| Asset availability | Available hours / eligible scheduled hours / MOMS | Maintenance and operational exclusion rules |
| Energy intensity | Boundary-specific energy / dry processed or shipped mass / MOMS | Denominator, carrier, interval and quality status |
| Material reconciliation residual | Unexplained balance difference / MOMS | Wet/dry basis, measurement uncertainty and threshold |
| Custody completeness | Lots/samples with complete required custody / eligible lots/samples | Evidence checks, not merely nonempty IDs |
| Environmental case status | Open cases, response times and overdue actions / MOMS + BPM | No unsupported claim of impact absence or universal compliance |
| Scenario robustness | Feasibility across declared uncertainty/availability cases / BPM | Input ranges and model validity domain |
| Export/resource-equivalent outlook | Qualified scenario value in selected reference units / valuation owner | Common basis, assumptions and sensitivity; not a live price |
| Engineering and training readiness | Accepted configuration/competence evidence / domain owners | Required independent authorizations remain separate |

BSC receives versioned metric projections with source, timestamp, unit, quality and formula version. Observed, simulated and forecast series are visually and logically distinguishable. Denominator changes trigger a new metric version or explicit restatement.

## 12. AI, automation and human authority

AI may assist with requirements drafting, process/model scaffolding, test generation, document retrieval, anomaly triage and explanation of scenario results. It must cite the accessed evidence, distinguish inference from fact and preserve provenance. AI-generated changes enter normal code review, tests and model governance; their authorship does not reduce acceptance requirements.

An optional local inference adapter may preserve the earlier gpt-oss concept. The earlier “Work GPT Astra Max” label is treated only as a project-proposed connector name: no official product, installed plugin, API contract or availability has been verified in these repositories. It is not an MVP dependency. Any such connector must implement the same read-only/suggestion contracts, access scopes, audit and human approval boundaries as other assistants.

Retrieved documents, sensor annotations and model outputs are untrusted data, not executable instructions. Tool access uses allowlists, least privilege and tenant/campaign scopes. The assistant cannot grant permits, change geological certifications, authorize extraction, alter environmental rules, execute payments, dispatch equipment directly or approve its own recommendations. Inference may be disabled without interrupting safety-critical local behavior or core process execution.

AI-assisted development is a delivery option, not an evidenced schedule multiplier. Track review effort, defects, rework, model validity and accepted scope alongside throughput; do not promise a development duration or production cost without a staffed plan and quotations.

## 13. Safety, environment, security and resilience

| Control | Required design behavior | Evidence before promotion |
|---|---|---|
| Activity authorization | Verify area, activity, dates, conditions and designated authority at work-package approval and acceptance | Positive, expired, wrong-area, wrong-activity and revoked cases |
| Environmental/data gate | Evaluate governed rule versions and quality/freshness; unknown data cannot satisfy readiness | Stale/missing sensor, calibration and exceedance scenarios |
| Independent local safety | Immediate response and interlocks remain local and independent of BPM/AI/connectivity | Relevant engineering assurance and test evidence supplied by qualified owners |
| Human control | Named roles for campaign approval, environmental review, technical release and operations; no self-approval | Separation-of-duty and delegation/expiry tests |
| IT/OT separation | Narrow authenticated gateways; no direct LLM/browser/broker path to actuators | Network-policy, credential and attempted bypass tests |
| Intermittent connectivity | Edge buffering, bounded commands, expiry checks and reconciliation after reconnect | Duplicate, delayed and lost-message tests; no stale command replay |
| Integrity and provenance | Signed releases, versioned rules/models, calibrated sources, append-only evidence revisions | Hash/signature checks and traceability audit |
| Access and recovery | Scoped identities, managed secrets, tenant isolation, tested backup/restore and incident process | Isolation tests; recovery objectives agreed for each service |
| Change control | Approved process, adapter, rule, model and physical-configuration compatibility | Staged rollout, rollback of software and safe handling of in-flight cases |

The applicable jurisdiction and authorization regime are unresolved inputs. This proposal specifies an evidence gate; it makes no claim that any oceanic activity is legally permitted or environmentally acceptable. Rules and numerical limits must be set by the responsible authorities and qualified project owners, not generated by an LLM.

## 14. Candidate implementation profile

The [BPM source](https://github.com/robotics-intelligent-systems/jfxai4bpm/blob/36a10248e0159deb922700d62f813219197a731e/README.md#153-engine-selection-profiles) presents alternative engine profiles, while the [MOMS source](https://github.com/robotics-intelligent-systems/jfxai4moms/blob/736b4ec3e4b0a27fcc52cc2c6078536c51d2265a/README.md#dependencies) separates selected implementation dependencies from optional integrations and research references. Keep that distinction.

| Capability | Candidate initial choice | Alternative / later expansion |
|---|---|---|
| Process runtime | Evaluate the source's lean Flowable profile | Bonita for a human-centric profile; select one, not both by default |
| Domain integration | Thin authenticated REST/event adapter with contract tests | Zato where its integration capabilities justify the added service |
| Data | PostgreSQL; evaluate PostGIS for spatial records | Separate stores or schemas/roles per owner; time-series extension after measurement |
| Messaging | One broker, with RabbitMQ from the BPM profile as a candidate | Another broker only after documented delivery/operations requirements |
| Artifact registry | Governed object storage plus model/evidence metadata | Dedicated model registry when scale/governance requires it |
| Simulation | One DES worker and recorded/mock MOMS adapter for the first slice | PySD, Modelica/FMU and validated marine/environmental adapters later |
| Observability | Correlated structured logs and metrics | OpenTelemetry instrumentation and traces |
| AI | Optional evidence-retrieval and suggestion service | Local inference/agent adapters after tool-governance testing |

These are selection candidates, not verified installed dependencies or a version compatibility matrix. A selection ADR must record exact versions, licenses, support assumptions, security posture, deployment cost and tested interoperability. The MOMS compendium is not a requirement to install every cited project.

### 14.1 Proposed repository placement

| Repository | Proposed path | Purpose |
|---|---|---|
| JFXAI4BPM | `docs/integrations/oceanic-mining.md` | This consolidation, adapted to project conventions |
| JFXAI4BPM | `MBSE/CAS/Drawio/oceanic-mining-integration.drawio` | Seven-view architecture package |
| JFXAI4BPM | `contracts/oceanic-mining/` | Process, command, event and simulation schemas |
| JFXAI4BPM | `processes/oceanic-mining/` | Executable BPMN/decision artifacts once implemented |
| JFXAI4BPM | `adapters/jfxai4moms/` | Anti-corruption/compatibility layer and contract tests |
| JFXAI4BPM | `simulation/oceanic-mining/` | Run manifests, worker adapters and validation cases |
| JFXAI4MOMS | `docs/integrations/jfxai4bpm.md` | Domain-side ownership and interface specification |
| JFXAI4MOMS | `contracts/oceanic-mining/` | Authoritative domain schemas and adapter fixtures |
| JFXAI4MOMS | `modules/oceanic-operations/` | Future domain implementation and data migrations |
| Both | `tests/integration/oceanic-mining/` | Cross-repository compatibility and release evidence |

These paths are proposed, not created in the remote repositories by this delivery. A later implementation must preserve unrelated changes and pin compatible releases across the two repositories.

## 15. Incremental implementation and acceptance

| Stage | Deliverable | Gate / dependencies |
|---|---|---|
| G0 Baseline and contracts | Owners, scope, licensing decisions, domain registry, schema examples and ADRs | Approved boundary; no unresolved ownership of a transition |
| G1 Simulation vertical slice | P02/P04 with synthetic samples, mock MOMS, one BPM engine, DES worker and evidence viewer | Contract, unit/CRS, provenance, deduplication and SIM/LIVE separation tests |
| G2 Read-only shadow | Real authorized observations mirrored into isolated stores; comparison cockpit | Quality/freshness monitoring, privacy controls and drift assessment |
| G3 Qualified test bench | HIL and maintenance/modular-work cases with controlled test hardware | Independent technical/safety acceptance; test credentials remain isolated |
| G4 Restricted supervised pilot | Explicitly authorized activity scope, current readiness, trained operators and monitored gateways | Permit/authority evidence, security, recovery drills and local safety readiness |
| G5 Portfolio and scale | Procurement/fabrication/port/BSC adapters, lot/energy reconciliation and series-production traceability | Validated capacity, configuration management and acceptance for each expansion |

No duration is assigned: team capacity, selected runtime, hardware readiness, model maturity and external reviews are unspecified. Software throughput improvements cannot eliminate laboratory, marine, procurement or independent review lead times.

### 15.1 Requirements-to-test traceability

| Requirement | Acceptance test / evidence | Gate |
|---|---|---|
| R01 Single domain authority | BPM request cannot mutate a MOMS-owned table; stale domain version is rejected | G1 |
| R02 Simulation isolation | Synthetic event, stolen simulation token and mislabelled mode all fail to create a LIVE command | G1, repeated at every release |
| R03 Idempotent integration | Duplicate/out-of-order messages produce one accepted transition; payload mismatch conflicts | G1 |
| R04 Authorization and freshness | Expired/revoked/wrong-scope approval or stale readiness blocks command acceptance | G3 before G4 |
| R05 Material genealogy | Demonstrate split/merge, custody break, assay correction and wet/dry balance handling | G1 synthetic; G5 measured |
| R06 Energy accounting | Storage discharge, meter gaps and cross-boundary transfers do not double count generation | G1 synthetic; G5 measured |
| R07 Reproducible simulations | Manifest/hash/seed replay within declared tolerance; invalid model/version rejected | G1; each new model |
| R08 Environmental assurance | Bad-quality data and threshold event open the correct case; BPM outage cannot disable local safeguards | G2/G3 before G4 |
| R09 Intermittent links | Delayed/expired command rejected after reconnect; buffered telemetry retains event time/quality | G3 |
| R10 Configuration traceability | Installed serial maps to approved BOM, fabrication release, inspection and as-built revision | G3/G5 |
| R11 Accountable AI | Retrieved prompt injection, excess scope and self-approval attempts are blocked; recommendations remain advisory | Before any AI tool enablement |
| R12 Recovery and tenant isolation | Restore evidence/state consistently; demonstrate no cross-tenant read/write or credential leakage | G2/G3 |
| R13 Case compensation | Timeout after domain acceptance queries original command; physical completion opens recovery, not fictitious rollback | G1/G3 |
| R14 Qualified KPIs | Every dashboard value exposes source, period, unit, mode, quality and formula version | G1/G5 |

## 16. Draw.io view index

| Tab | View | Primary purpose |
|---|---|---|
| 01 Architecture | Integrated control plane, domain, simulation and OT boundaries | Where responsibilities and writes belong |
| 02 Delivery gates | Staged expansion from contracts to portfolio integration | What must be proven before each expansion |
| 03 Processes | Survey-first campaign lifecycle with conditional work and exception paths | How orchestration and assurance interact |
| 04 Data and contracts | Ownership, command admission, domain transactions and event projections | Prevent duplicate state and ambiguous execution |
| 05 Simulation and AI | Model/run provenance, isolated modes and advisory AI | Prevent simulation or agent access to physical control |
| 06 Resources and value | Material, energy and valuation ledgers with KPI qualification | Prevent double counting and false PPP claims |
| 07 Sources and assurance | Pinned baselines, inherited/added boundaries and requirements | Trace the proposal back to evidence and acceptance gates |

The diagram is native, uncompressed Draw.io XML with editable shapes and connectors. It is not a CAD model, an executable process package or an operational interface. Open the `.drawio` file in diagrams.net and use the seven page tabs; source cards include pinned GitHub links.

Package checks cover XML parsing, seven page definitions, unique cell IDs, connector references, page/text bounds and a visual review of locally rendered geometry. The file has not been exercised in the diagrams.net application, and no executable BPM engine or end-to-end service integration was tested. These artifact checks do not satisfy the implementation acceptance tests above.

## 17. Decisions still required

Confirm the operating context and permitted activities; nominate process/domain/assurance owners; select one initial runtime profile; resolve project and dependency licensing; define data access, retention and jurisdiction; obtain actual hardware and marine-model validation evidence; approve the MVP acceptance criteria; and select the first real external adapter. These decisions precede live deployment and any reliable budget/schedule estimate.

**Final principle:** simulate and review in JFXAI4BPM; preserve mining truth in JFXAI4MOMS; admit only authorized domain requests; retain physical safety and control locally; and make every metric and decision traceable to its evidence.
