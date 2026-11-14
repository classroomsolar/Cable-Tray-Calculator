# Cable_Tray_Calculator_prompt
## Conduit, Raceway, Cable Tray & Electrical Routing Calculator

| Item | Detail |
|---|---|
| Calculator | **Cable_Tray_Calculator** |
| Status | Existing calculator — continue and complete on the website |
| Website page | `/routing` (tray, conduit and raceway fill, cleats, segregation, bonding, pulling, routes, schedules) |
| Master Prompt V5.0 scope | Group 7 — Conduit, Raceway, Cable Tray and Electrical Routing (R141–R164) + shared engine IDs R180, R181, R182, R274, R275, R276 |
| Project types | P1 utility fixed-tilt, P2 utility single-axis tracker, P3 commercial carport, P4 commercial/industrial rooftop, P5 residential rooftop — applicability recorded per requirement (REQUIRED / CONDITIONAL / NOT APPLICABLE / UNSUPPORTED, Section 19) |
| Revision | Final — 14 November 2026 |

## 0. About this file

- This is the **only** project document for this calculator. It replaces every earlier README, prompt, handoff and requirement document; everything still needed from them is written here.
- Governing specification: **Master Prompt V5.0** (Integrated Electrical PV Design Engineering Platform, 9 November 2026). Give the AI both this file and the Master Prompt at the start of every session. If the two ever disagree, the Master Prompt wins.
- The calculator is part of **one integrated public website** (Master Prompt Sections 2, 43, 80): its own route/page, shared project data, shared equipment database, shared reports.
- Reply to the owner in **Hinglish** (simple Hindi–English). Write code, reports and documents in English.
- The owner is an electrical / PV design engineer, not a software developer. The AI does the research, design, coding, testing, debugging and documentation itself (Master Prompt Sections 1–4).


## 1. What this calculator does

Conduit size, fill and conductor capacity, raceway sizing, conduit ampacity derating, grouping and separation, cable-tray width, electrical fill, arrangement, circuit segregation, barriers, covers, cleat selection and short-circuit cleat spacing, tray and raceway bonding, bend radius, pulling tension, sidewall pressure, pull points, routing length and quantity, routing segregation, compliance checks and routing/tray/conduit schedules (Group 7, R141–R164). It owns the **shared cable-pulling engine** used for underground and MV cables too (R180–R182, R274–R276).

**Scope boundary:** Never build, anywhere in this calculator: generator sources or sizing, HV / EHV equipment or studies (above the 35 kV class), substation engineering, field testing / measurement / commissioning, structural / civil / mechanical calculations, and any financial or cost calculation (equipment prices, CAPEX, OPEX, LCOE, tariffs). BESS is deferred (Master Prompt Section 18): do not build it now, but keep data models ready for it. Everything is built on the public website — no spreadsheets, no VBA, no desktop tools.


## 2. Requirements of this calculator


### 2.1 Functional requirements from Master Prompt V5.0

Every requirement below must end up implemented and verified, or marked NOT APPLICABLE / NOT SUPPORTED with a written reason. "Current state" is the starting point found in the earlier work; confirm it in Phase 0.


**Group 7 — Conduit, Raceway, Cable Tray and Electrical Routing (R141–R164, 24 active)**

| ID | Requirement (Master Prompt V5.0, verbatim) | Current state |
|---|---|---|
| R141 | Conduit size calculation. | Partly built — complete |
| R142 | Conduit conductor-fill calculation. | Partly built — complete |
| R143 | Conduit conductor-capacity verification. | Partly built — complete |
| R144 | Raceway sizing and fill assessment. | Partly built — complete |
| R145 | Conduit ampacity adjustment and derating. | Partly built — complete |
| R146 | Raceway grouping and conductor-separation assessment. | Partly built — complete |
| R147 | Cable-tray width calculation. | Built earlier — verify |
| R148 | Cable-tray electrical fill assessment. | Built earlier — verify |
| R149 | Cable-tray conductor and cable arrangement. | Built earlier — verify |
| R150 | Cable-tray circuit segregation assessment. | Built earlier — verify |
| R151 | Cable-tray electrical barrier assessment. | Built earlier — verify |
| R152 | Cable-tray cover and enclosure applicability assessment. | Partly built — complete |
| R153 | Cable-cleat selection assessment. | Built earlier — verify |
| R154 | Electrical short-circuit cleat-spacing assessment. | Built earlier — verify |
| R155 | Cable-tray bonding and grounding assessment. | Built earlier — verify |
| R156 | Raceway bonding and grounding assessment. | Not built — build new |
| R157 | Cable bend-radius compliance checks. | Partly built — complete · shared engine: Cable pulling tension, sidewall pressure and bend radius |
| R158 | Cable-pulling tension calculation. | Partly built — complete · shared engine: Cable pulling tension, sidewall pressure and bend radius |
| R159 | Cable sidewall-pressure calculation. | Partly built — complete · shared engine: Cable pulling tension, sidewall pressure and bend radius |
| R160 | Cable-pulling length and pull-point assessment. | Partly built — complete |
| R161 | Cable-routing length and quantity calculation. | Built earlier — verify |
| R162 | Electrical routing segregation and separation assessment. | Partly built — complete |
| R163 | Cable-tray and raceway electrical compliance checks. | Built earlier — verify |
| R164 | Electrical routing, tray and conduit schedules. | Built earlier — verify |

**Shared engine built here and used by other calculators (Master Prompt Section 23)**

| ID | Requirement (verbatim) | Listed in the group of |
|---|---|---|
| R180 | Underground cable-pulling tension calculation. | Cable_Thermal_Calculator |
| R181 | Underground cable sidewall-pressure calculation. | Cable_Thermal_Calculator |
| R182 | Underground cable bend-radius and pulling assessment. | Cable_Thermal_Calculator |
| R274 | MV cable-pulling tension calculation. | MV_Electrical_Design_Calculator |
| R275 | MV cable sidewall-pressure calculation. | MV_Electrical_Design_Calculator |
| R276 | MV cable bend-radius and pulling assessment. | MV_Electrical_Design_Calculator |

### 2.2 Additional requirements from this calculator's earlier documents

These came from the earlier README / prompt / requirement documents and are kept because they match Master Prompt V5.0.

| # | Requirement | Matches V5.0 |
|---|---|---|
| D01 | Tray fill LV/MV/DC/AC; single/multiconductor; trefoil/flat; spacing; width/depth optimisation | R147–R149 |
| D02 | Barrier rules, fibre segregation | R150–R151, R162 |
| D03 | EGC placement/sizing; tray bonding/grounding | R155, R186 |
| D04 | Multiple circuits / parallel sets | R149, R072, R095 |
| D05 | Ampacity derating handoff (NEC 2020/2023 edition-specific) | R145; conductor ampacity owners are DC_Cable / Inverter_LV_AC / MV_Electrical |
| D06 | Electromagnetic force during fault; cleat force/spacing; trefoil cleat selection | R153–R154 (fault data from Fault_Current_Studio) |
| D07 | Outdoor/corrosion material selection | R132-type environmental rating; tray material selection is electrical-installation data |
| D08 | Bend/tee/cross/reducer checks; route fittings; route quantities | R157, R161 |
| D09 | BOM; tray schedule; automatic section view; code-check report | R163–R164, R415, R424 |
| D10 | Pull plan: pulling tension, sidewall pressure, forward/reverse | R157–R159 shared pulling engine |
| D11 | Product optimiser (ranks qualified products only) | Section 65 opportunity |
| D12 | Conduit/tray fill, barriers, cleats, EGC (from the earlier Production_Calculator documents) | Group 7, R186 |
| D13 | Entry/exit orientation; pulling direction; pulling tension; sidewall pressure; jam ratio; bend accumulation; maximum pulling length; reel/pull-section planning (from the earlier Vault_Calculator documents) | R157–R160, R180–R182 shared pulling engine |
| D14 | Conductor routing, route network, shortest path, route segmentation (from the earlier Vault_Calculator documents) | R161 routing quantities |
| D15 | Conduit fill; spare conduits; future expansion reserve (from the earlier Vault_Calculator documents) | R142, R177 |

### 2.3 Engineering method and verification requirements (Master Prompt Part 7)

Apply Master Prompt Section 40 in full, plus:

- Fill calculations per the selected code edition and tray type (ladder, ventilated trough, solid bottom, channel), single vs multiconductor, with exact table/provision references.
- Cleat short-circuit force from a published method with peak current from Fault_Current_Studio (not RMS) and its stated assumptions.
- Pulling tension and sidewall pressure with friction coefficients and limits from manufacturer data; bend direction effects; boundary tests at limits.
- Ampacity derating feedback: changing the tray arrangement must mark the dependent cable-sizing results STALE.


### 2.4 Shared engines and connections to other calculators (Sections 23, 45, 49)

- **Owns:** conduit/raceway fill engine, tray fill/width/arrangement engine, segregation and barrier rules, cleat engine, routing service, and the **shared cable-pulling engine** (R157–R159, R180–R182, R274–R276).
- **Uses:** cable lists from the cable calculators and the Master Database; peak fault current and duration from Fault_Current_Studio (R154); bonding rules from Grounding.
- **Gives:** grouping/derating conditions back to the conductor engine (STALE-tracked); pulling results to Vault, Cable_Thermal and MV_Electrical_Design; tray/conduit schedules and BOM quantities to Documentation_Schedules_QA.

| Direction | Data | From / to |
|---|---|---|
| In | Cable list with sizes, ODs, weights, bend radii, voltage class | the DC calculators (PV_String_MPPT, DC_Protection_Combiner, DC_Cable_Connector) / the LV AC calculators (Inverter_LV_AC, LV_Interconnection_Metering) / the MV calculators (MV_Electrical_Design, Transformer_POI) + Master DB |
| In | Fault current and clearing time per circuit | Fault_Current_Studio |
| In | Bonding / EGC requirements | Grounding_Calculator |
| Out | Tray/conduit selection, fill, arrangement | Documentation_Schedules_QA_Calculator schedules (R414, R415) |
| Out | Grouping/derating condition per circuit | the DC calculators (PV_String_MPPT, DC_Protection_Combiner, DC_Cable_Connector) / the LV AC calculators (Inverter_LV_AC, LV_Interconnection_Metering) / the MV calculators (MV_Electrical_Design, Transformer_POI) ampacity (feedback loop — must be STALE-tracked, Section 50) |
| Out | Pulling results | Vault_Calculator, Cable_Thermal_Calculator, the MV calculators (MV_Electrical_Design, Transformer_POI) |
| Out | Route lengths and quantities | Documentation_Schedules_QA_Calculator BOM (R424), Production_Calculator losses via the DC and LV AC calculators |

Every connection is a typed, versioned contract; a changed upstream result marks this calculator's dependent results STALE.


## 3. Work already done

**Status:** the previous version of this calculator (retired) implemented the following tray functions. It is rebuilt on the website from this specification.

**Functions specified and previously built:** tray fill for LV/MV/DC/AC; multiconductor and single-conductor logic; trefoil and flat arrangements; spacing engine; barrier rules; fibre segregation; EGC placement and sizing; multiple circuits and parallel sets; tray width and depth optimisation; ampacity derating handoff (NEC 2020 and 2023, edition-specific, no cross-edition fallback); cable OD/weight/bend database; thermal impact screening; electromagnetic force during a fault; cleat force/spacing and trefoil cleat selection; tray bonding/grounding; outdoor and corrosion material selection; bend/tee/cross/reducer checks; route fittings and quantities; tray schedule; automatic section view; code-check report; voltage drop (supplemental); adiabatic short-circuit withstand (supplemental); forward/reverse pull plan; product ranking among qualified products. Normal workflow: easy input → results → report, advanced inputs separate. Input-sanity gates: AC/DC vs frequency and phase, design temperature range, route geometry, whole-number parallel sets, positive fault duration.


## 4. Functions still to be added

- [ ] R141–R146 conduit and raceway engine: conduit size, fill, conductor capacity, raceway sizing, derating and grouping, separation.
- [ ] R156 raceway bonding and grounding.
- [ ] R157–R160 and R180–R182, R274–R276 the single shared pulling engine: bend radius, segment tension forward/reverse, sidewall pressure, jam ratio, cumulative bends, maximum pulling length, pull points and pull-section/reel planning (the Vault_Calculator pull functions are the reference specification).
- [ ] R161–R162 routing length/quantity service and route segregation checks.
- [ ] R154 cleat checks using peak fault current and duration from Fault_Current_Studio (not typed-in values).

**Requirements with no implementation yet (build new):**

- [ ] R156 Raceway bonding and grounding assessment

## 5. Earlier work still to be completed

- [ ] Rebuild every function listed in Section 3 as a website engine (Group 7).
- [ ] Tray equipment data move into the Master Database.
- [ ] Rebuild the 100-tool research register and the 200-case adversarial test set on the website project.

**Partly built — complete them:**

- [ ] R141 Conduit size calculation
- [ ] R142 Conduit conductor-fill calculation
- [ ] R143 Conduit conductor-capacity verification
- [ ] R144 Raceway sizing and fill assessment
- [ ] R145 Conduit ampacity adjustment and derating
- [ ] R146 Raceway grouping and conductor-separation assessment
- [ ] R152 Cable-tray cover and enclosure applicability assessment
- [ ] R157 Cable bend-radius compliance checks
- [ ] R158 Cable-pulling tension calculation
- [ ] R159 Cable sidewall-pressure calculation
- [ ] R160 Cable-pulling length and pull-point assessment
- [ ] R162 Electrical routing segregation and separation assessment

**Built earlier — rebuild/carry over to the website and prove with tests:**

- [ ] R147 Cable-tray width calculation
- [ ] R148 Cable-tray electrical fill assessment
- [ ] R149 Cable-tray conductor and cable arrangement
- [ ] R150 Cable-tray circuit segregation assessment
- [ ] R151 Cable-tray electrical barrier assessment
- [ ] R153 Cable-cleat selection assessment
- [ ] R154 Electrical short-circuit cleat-spacing assessment
- [ ] R155 Cable-tray bonding and grounding assessment
- [ ] R161 Cable-routing length and quantity calculation
- [ ] R163 Cable-tray and raceway electrical compliance checks
- [ ] R164 Electrical routing, tray and conduit schedules

## 6. Checks and audits still to be done

- [ ] Fill calculations per the adopted code edition for every tray type (ladder, ventilated trough, solid bottom, channel) and conduit type, with exact provisions.
- [ ] Pulling tension and sidewall pressure hand calculations with manufacturer friction coefficients and limits; forward vs reverse.
- [ ] Cleat-force calculation against a published method using peak current.
- [ ] STALE test: changing tray arrangement marks dependent cable sizing STALE.
- [ ] Engineering and software audit; challenge campaign of 200 cases.
- [ ] Engineering audit (Section 72): methods, editions, equations, assumptions, units, correction factors, limits, source applicability, independent results, unsupported conditions, false PASS results.
- [ ] Software audit: logic, architecture, types, validation, error handling, edge cases, duplication, hard-coded values, feature preservation.
- [ ] Data audit: units, types, sources, revisions, duplicates, conflicts, missing values, overrides.
- [ ] Integration audit: schemas, IDs, dependencies, STALE results, unit and method compatibility with connected calculators.
- [ ] UI/UX audit: workflow, labels, units, help, warnings, responsiveness (desktop/tablet/mobile), WCAG 2.2 AA accessibility, diagram accuracy, persistence.
- [ ] Security audit: authentication, authorisation, private/public separation, secrets, input validation, dependencies.
- [ ] Requirements coverage audit: every ID in Section 2 traced to code and tests.
- [ ] Research register and benchmark matrix (Section 11): relevant calculators, manufacturer tools and papers actually reviewed (count only real sources).

## 7. Process to follow to finish everything

This is the Master Prompt V5.0 development process applied to this calculator. Follow it for every task.

### 7.1 Rules that never change (Master Prompt Sections 5, 6, 27, 34)
- Never invent a standard, clause, formula, coefficient, equipment rating, curve, clearing time, test result or repository state. Missing critical input → **INPUT REQUIRED**; never a guessed value.
- Every numerical result comes from a deterministic, tested calculation engine — never from AI text.
- Every result shows a status: PASS, FAIL, REVIEW REQUIRED, INPUT REQUIRED, NOT APPLICABLE, NOT VERIFIED, NOT SUPPORTED or STALE. Never PASS when inputs, sources, methods or validation are missing. Every warning says what is wrong, why it matters, which input to check and how to fix it.
- Never claim "complete", "100 %", "certified" or "compliant" without the evidence of Section 8 of this file.
- Preserve working calculations and verified results; change a validated method only with a documented reason and tests (Sections 52, 58).
- No paid service, subscription or usage-based dependency without the owner's approval (Section 84). No credentials, secrets or private data in code or Git (Sections 6, 60, 82).

### 7.2 Execution cycle for every task (Master Prompt Section 7)
**A Inspect** existing code, data, tests and behaviour → **B Research** primary standards, editions, manufacturer documents, papers and benchmark tools → **C Design** inputs, outputs, units, equations, sequence, error states, tests → **D Implement** the deterministic engine first, then UI, diagrams, data and integration, in small reversible changes → **E Test** (unit, golden, independent, boundary, invalid input, regression, UI, export, security, end-to-end) → **F Audit and fix** (separate engineering and software reviews; repeat until no critical/high defect) → **G Improve** (low-risk improvements; scope expansion only with approval) → **H Report** (files changed, tests run, results, limitations, next step). Do not stop after a plan, a draft or a good-looking screen.

### 7.3 Phases (Master Prompt Section 62)
| Phase | Work for this calculator | Done when |
|---|---|---|
| 0 Inventory (read-only) | Write the master specification of every function in Section 3; map R141–R164 and the pulling IDs. | Phase 0 report delivered: inventory, current state of every requirement with evidence, risks, batch plan, single best next task |
| 1 Engine | Build tray, conduit/raceway, cleat, segregation, bonding, routing and the shared pulling engines. | Every engine has a master specification, version ID, typed contract and test harness, separate from UI |
| 2 Functional verification | Inputs, units, defaults, overrides, sequence, equations, intermediate values, invalid inputs, lookups, warnings, repeatability | All found defects fixed and retested |
| 3 Challenge and independent validation | Hand calculations, published examples, challenge campaign. | Golden and independent checks pass within justified tolerances; real challenge-case count reported |
| 4 Customer workflow | Which inputs are visible, auto-filled from the database, inherited from other calculators, optional or advanced | Workflow specification written |
| 5 UX/UI | Tray and conduit cross-sections and route views from engine data. | Screens use the shared design system; visuals come from the same data as the calculation |
| 6 Integration | Grouping/derating to the conductor engine; pulling results to Vault, Cable_Thermal and MV_Electrical_Design; schedules to Documentation_Schedules_QA. | End-to-end tests pass; STALE tracking works |
| 7 Release | Staging and public-URL tests, monitoring, backup/restore, rollback | Owner approves the production release |

### 7.4 Engineering rules for every engine (Master Prompt Sections 28–33, 46–48)
- Before coding: master specification (purpose, inputs with units and sources, outputs, standard and edition, equations, assumptions, valid range, warnings, test cases) and data-dictionary entries with stable names (no "Value1", "Factor2").
- Engine: defined inputs/outputs/units, equations with variable definitions, source references (standard, edition, clause/table/equation), assumptions, valid range, input validation, numerical precision/convergence, version ID; identical results for identical inputs; handles zero/negative/huge/tiny/missing values; never shows a failed calculation as a normal result; separate from the UI.
- Units: one central unit service; SI internally; feet/inches and metric display; never mix units silently; full precision internally, round only for display.
- Assumptions classified CONFIRMED / DEFAULT / ENGINEERING ASSUMPTION / NEEDS USER CONFIRMATION / REFERENCE-DERIVED. Show DATABASE VALUE, USER OVERRIDE and VALUE USED IN CALCULATION for every overridable value, with an audit trail.
- Equipment data only from the Master Engineering Database (Section 44), auto-populated from the selected record, with the database revision stored with every result.
- Traceability chain for every important result: user input → database value → intermediate values → correction factors → equation/method → final result, with the limit used, status, warnings, sources and engine version.
- Results passed to other calculators go through typed, versioned contracts; changed upstream inputs mark downstream results **STALE** (Sections 47–50). Never propagate a result whose study case, topology, voltage level or assumptions do not match.

### 7.5 Testing rules (Master Prompt Sections 66–71)
- Golden tests with source of expected values; independent hand calculations or separate scripts (never only against code that shares the implementation); tolerances justified, never chosen to make a test pass.
- Boundary, invalid-input, unit-conversion, unsupported-case and regression tests; end-to-end tests for every applicable project type P1–P5.
- Challenge campaign toward **200 meaningful cases** designed to make the calculator fail; report the real number completed.
- Every reported defect: reproduce → trace UI → validation → lookup → calculation → result → saved state → fix the root cause → add a regression test → rerun all golden tests.

### 7.6 Working method
- GitHub is the home of the code (Section 60): tag the known-good state before work, feature branch, small commits, pull request for engineering/data/security changes, tests run before merge, tagged releases with rollback points.
- Work in controlled batches (Section 61); after each batch give the delivery report of Section 87 (requested, done, requirement IDs, preserved, files changed, sources, tests run with results, remaining gaps, next step).
- Keep these records up to date in the repository (Section 85): REQUIREMENTS.md (traceability for every ID in Section 2), MASTER_SPECIFICATION.md, DATA_DICTIONARY.md, DECISIONS.md, SOURCE_REGISTER.md, TEST_MATRIX.md, ISSUES.md, PROGRESS.md, CHANGELOG.md.
- Ask the owner only when a decision changes safety, correctness, scope, cost, privacy or is irreversible (Section 5). The only open items the Master Prompt leaves to the owner are: jurisdiction and code editions to target first, hosting provider and budget, which calculator becomes the first fully verified reference module, whether 35 kV stays the MV limit (Appendix F) — plus approval of production releases and paid services.

### 7.7 Calculator-specific rules carried over from the earlier documents
- Normal workflow EASY_INPUT → RESULTS → REPORT; advanced inputs separate
- Expansion splice requirements → **Decided: expansion-splice mechanics excluded (Sections 16–17); bonding across expansion splices stays in scope (R155).**
- Release hierarchy FAIL > INPUT REQUIRED > REVIEW REQUIRED > PASS; procurement/IFC review separate from calculation release
- Input sanity gates (AC/DC vs frequency/phase, temperatures, route geometry, parallel sets, fault duration)


## 8. Final result — what "finished" looks like

- Verified tray, conduit and raceway design on the website with fill, arrangement, segregation, cleats, bonding, routes and schedules.
- One shared pulling engine used by every calculator that pulls cable.
- **Every requirement in Section 2** is implemented, or marked NOT APPLICABLE / NOT SUPPORTED with a written reason, with evidence in REQUIREMENTS.md (file, function, test). Status per requirement follows Section 57 (IMPLEMENTED — NOT VERIFIED → SOFTWARE TESTED → ENGINEERING VALIDATED → DEPLOYED → APPROVED).
- **Module completion checklist (Master Prompt Section 94) fully satisfied:** scope documented; existing behaviour preserved; methods and standard editions verified or flagged; deterministic engine separated from UI; inputs/outputs/units/assumptions/overrides/limits traceable; equipment data from the Master Database with revision recorded; golden and independent checks pass within justified tolerances; boundary, invalid-input, unsupported-case and regression tests pass; engineering and software reviews recorded; integration and STALE control work; UI and diagrams match the engine; reports and exports reproduce the screen; security and privacy satisfied; limitations disclosed; no known critical or high-severity defect.
- **Website acceptance (Section 95):** works on the public domain over HTTPS; its route opens directly and after refresh; desktop, tablet and mobile; private projects stay private; save/load/scenarios/recovery work; tested through the real public URL.
- **Reports and exports (Sections 77–78):** PDF calculation package, CSV, JSON (and schedules where applicable) containing inputs, units, equipment and database revision, method and standard edition, intermediate values, results with status, assumptions, warnings, sources and engine version — identical to the screen.
- **Honest status:** a final delivery report (Section 87) states exactly what is complete, what is not, and why.


## 9. Plugins and tools

| Capability (Master Prompt Section 8) | Use it for | Example plugin / tool |
|---|---|---|
| Git repository connector | Branches, commits, pull requests, issues, diffs | GitHub connector |
| Coding agent + execution environment | Write code, run builds and tests, debug | Coding agent with terminal (e.g. Claude Code / similar), Node.js, Python |
| Web research and browser | Official standards information, manufacturer datasheets, benchmark tool documentation | Web search, web fetch, browser |
| PDF / OCR document reader | Read code books, datasheets, manuals, papers page by page | PDF reader with OCR |
| Owner's document storage | The owner's books and reference PDFs (for example the NEC books kept in Dropbox) | Google Drive / Dropbox connector |
| Academic research search | Peer-reviewed papers and DOIs | Semantic Scholar / Google Scholar / IEEE Xplore search |
| Independent maths check | Hand-check equations and reference values | Python (NumPy, SciPy, SymPy), Wolfram |
| Browser / UI automation | End-to-end tests on desktop and mobile, downloads, console errors | Playwright (Chromium, Firefox, WebKit) |
| Accessibility check | WCAG 2.2 AA audit | axe-core / Lighthouse |
| UI / diagram design | Wireframes, screen flows, engineering diagrams | Figma or similar design tool |
| Database connector | Schemas, migrations, records, permissions | Connector for the chosen database |
| Hosting / deployment connector | Deployments, logs, domains, rollback | Connector for the chosen host (Wix connector only for the existing live sites) |
| Security analysis | Dependency, secret and code scanning | Dependabot / npm audit / pip-audit, CodeQL, secret scanning |

Use a tool only when it has a real role, check access/permissions/quota/cost first, never claim a tool ran when it did not (Sections 8–9). Do not use Formula Genius or Coursera. When delegation is available, split work into specialist reviews — standards, independent calculation, equipment data, code/architecture, UX, security, testing — and have an independent checker that never sees the builder's code (Section 9).

**Specific to this calculator:**

| Purpose | Tool |
|---|---|
| Pulling / fill verification | Python NumPy/SciPy, Wolfram |
| Feature benchmarking only | Southwire and Polywater pulling calculators, Legrand/Eaton tray fill tools (documentation) |

Benchmark tools are used to compare features and results only — never copy their code, data or methods without checking them (Section 12).


## 10. First task and first reply

1. Reply in Hinglish: confirm that Master Prompt V5.0 governs and that this is **Cable_Tray_Calculator**; say what you can and cannot access.
2. Do Phase 0 only (read-only): inventory, current state of every requirement in Section 2 with evidence, risks, batch plan for Phases 1–3, and the single best next task.
3. Wait for the owner to approve the Phase 0 report, then work through Sections 4, 5 and 6 using the process of Section 7 until Section 8 is true.
