# Test Plan — Web Progress V2.0.3

[← Back to case study](../README.md)

| | |
|---|---|
| **Product** | Web Progress: Installer, Data Migration Tool, Web site |
| **Build** | V2.0.3 (baseline V2.0.2) |
| **Author** | Abdelrahman Ali, SQA Engineer |
| **Test basis** | Product user manual (v2.0.2), defect tracker (38 defects), requirements register (WP-01 … WP-06) |

## 1. Objective
Confirm that V2.0.3 can be installed in both deployment modes, uploads survey data correctly, shows correct progress to clients, and delivers requirements WP-01 … WP-06 without bringing back any of the 21 defects fixed in earlier releases.

## 2. Scope

**In scope**

| Area | Coverage |
|---|---|
| Prerequisites installer | Windows features, IIS, URL Rewrite, DB restore, verification script |
| Web Progress installer | Data Uploader / Web Server / Both options, validation, DB creation, scope selection |
| Data Migration Tool | Pipeline & Structure settings, divided pipes, KP/PosLog units, events source, profiles, logs, upload cycles, multi-vessel |
| Web site | Login, Main, Pipeline (Progress, All Pipes, Trends, Findings), Structure (Progress, Findings, Tasks, 3D model), Reports, Users, Notifications |
| Online (remote) mode | Server real-IP configuration, vessel upload over the internet, third-party viewing |
| New requirements | WP-01 … WP-06 acceptance tests |

**Out of scope:** load and performance testing, security penetration testing, 3D model conversion (done by tech support), licence generation.

## 3. Test approach

| Level / type | What | Suite |
|---|---|---|
| Smoke | Build acceptance: install → upload → dashboards → reports → remote view | 12 cases |
| Functional | Features, negative cases, boundary values, requirement acceptance | 79 cases |
| Regression | One case per verified-fixed defect, using the original reproduction steps | 21 cases |
| Data verification | Dashboard KPIs compared with SQL queries on source DBs | in functional |
| Configuration | 14 scenarios: mode × scope × migration settings × vessel count | [scenario matrix](02-test-environment.md#scenario-matrix) |

**Techniques:** equivalence partitioning, boundary value analysis, decision-table combinations, error guessing from defect history, risk-based prioritisation.

## 4. Priority and risk

| Risk | Impact | Mitigation |
|---|---|---|
| Wrong progress or completion values shown to client | High: client decisions based on false data | SQL cross-checks of KPIs; bug_38 test |
| Data lost or hidden across vessels | High | Multi-vessel scenarios SCN-07/08 |
| Remote upload fails silently | High | Network-loss and server-down tests; log checks |
| Installation fails on site | High: no system at all | Smoke on a clean machine for each release |
| UI layout issues at lower resolutions | Low | Resolution checks at 1920 / 1366 / 1280 |

## 5. Entry criteria
- Build delivered with release notes listing fixed defects
- Test environment ready (see [environment](02-test-environment.md)); source DBs restored
- All smoke cases pass. **If any High smoke case fails, the build is rejected.**

## 6. Exit criteria
- 100 % of smoke and regression cases executed
- ≥ 95 % of High-priority functional cases executed
- No open High-severity defect without a documented decision (fix / defer / accept)
- Every requirement WP-01 … WP-06 has passed acceptance tests or is formally deferred

## 7. Defect management
Defects are logged in the [bug tracker](../bug-reports/WebProgress_Bug_Tracker.xlsx) with mode, module, steps, expected result, priority (business impact) and severity (technical impact).

Lifecycle: **New → Open → Done**, or **Blocked** when a design decision is needed. QA closes a defect only after re-testing it on the fix build.

## 8. Deliverables
Test suite with traceability · executed results per build · defect tracker updates · test summary report per release.
