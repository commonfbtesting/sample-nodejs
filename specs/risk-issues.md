# Risk and Issues

> **Source:** [`risk-issues.json`](./risk-issues.json) &nbsp;·&nbsp; **Spec version:** 1.0.0 &nbsp;·&nbsp; **Generated:** 2026-09-23
> **Reusable across:** any app project &nbsp;·&nbsp; **Audience:** developers, maintainers, security, operations, product, agents

---

## 1. Project Reference

| Field | Value |
| :--- | :--- |
| Name | Unnamed Project |
| Slug | `unnamed-project` |
| Lifecycle stage | `greenfield` |
| Project summary | [`project.json`](./project.json) |

---

## 2. Summary

| Metric | Count |
| :--- | ---: |
| Risks | 7 |
| Issues | 4 |
| **Total items** | **11** |

**By severity** (risks + issues combined):

| Severity | Count | Distribution |
| :--- | ---: | :--- |
| `critical` | 0 | `                    ` |
| `high` | 0 | `                    ` |
| `medium` | 7 | `███████████████` |
| `low` | 4 | `████████` |
| `info` | 0 | `                    ` |

**By status:**

| Status | Count |
| :--- | ---: |
| `open` | 9 |
| `acknowledged` | 2 |

```
  Severity distribution (11 items)
  ┌────────────────────────────────────────────────┐
  │ critical  │                                     │  0
  │ high      │                                     │  0
  │ medium    │ ███████████████                     │  7
  │ low       │ ████████                            │  4
  │ info      │                                     │  0
  └────────────────────────────────────────────────┘
```

---

## 3. Scoring Model

Risk score is a product of severity and likelihood:

```
  risk_score = severity_weight × likelihood_weight
```

| Severity | Weight |  | Likelihood | Weight |
| :--- | ---: | :--- | :--- | ---: |
| `critical` | 4 |  | `almost-certain` | 5 |
| `high` | 3 |  | `likely` | 4 |
| `medium` | 2 |  | `possible` | 3 |
| `low` | 1 |  | `unlikely` | 2 |
| `info` | 0 |  | `rare` | 1 |

**Score bands:**

| Band | Range |
| :--- | :--- |
| `severe` | 16 – 20 |
| `high` | 10 – 15 |
| `moderate` | 5 – 9 |
| `low` | 0 – 4 |

```
  Score grid (severity × likelihood)

  Likelihood ─────────────────────────────────────────────────▶
  Severity   rare  unlikely  possible  likely  almost-certain
  ┌────────┬──────┬─────────┬─────────┬───────┬──────────────┐
  │critical│  4   │    8    │   12    │  16   │      20      │
  │  high  │  3   │    6    │    9    │  12   │      15      │
  │ medium │  2   │    4    │    6    │   8   │      10      │
  │  low   │  1   │    2    │    3    │   4   │       5      │
  └────────┴──────┴─────────┴─────────┴───────┴──────────────┘

  Where the 7 risks land:
    medium / almost-certain  → 10   RISK-001
    medium / likely          →  8   RISK-002, RISK-003
    medium / possible        →  6   RISK-004
    low    / likely          →  4   RISK-005
    low    / possible        →  3   RISK-006, RISK-007
```

---

## 4. Risk Matrix

```
                    LIKELIHOOD
              rare   unlikely  possible  likely  almost-certain
         ┌─────────┬─────────┬─────────┬─────────┬─────────────┐
  crit   │         │         │         │         │             │
         ├─────────┼─────────┼─────────┼─────────┼─────────────┤
  high   │         │         │         │         │             │
         ├─────────┼─────────┼─────────┼─────────┼─────────────┤
  med    │         │         │  R-004  │ R-002   │   R-001     │
         │         │         │         │ R-003   │             │
         ├─────────┼─────────┼─────────┼─────────┼─────────────┤
  low    │         │         │ R-006   │ R-005   │             │
         │         │         │ R-007   │         │             │
         └─────────┴─────────┴─────────┴─────────┴─────────────┘
```

No item reaches the `critical` or `high` severity bands; the highest score is
`RISK-001` at **10 (high band)**.

---

## 5. Risks (Potential)

| ID | Title | Category | Sev | Likelihood | Score | Band | Status | Detection |
| :--- | :--- | :--- | :--- | :--- | ---: | :--- | :--- | :--- |
| RISK-001 | No source code or project structure exists | maintainability | medium | almost-certain | 10 | high | open | detected |
| RISK-002 | No dependency manifest or lockfile | dependency | medium | likely | 8 | moderate | open | detected |
| RISK-003 | No automated tests or CI pipeline | testing | medium | likely | 8 | moderate | open | detected |
| RISK-004 | Secrets present in the runtime environment | security | medium | possible | 6 | moderate | acknowledged | detected |
| RISK-005 | No license declared | licensing | low | likely | 4 | low | open | detected |
| RISK-006 | Default branch has no protection or review policy | process | low | possible | 3 | low | open | inferred |
| RISK-007 | Application hosts are unreachable (HTTP 502) | availability | low | possible | 3 | low | open | detected |

### RISK-001 — No source code or project structure exists

| Field | Detail |
| :--- | :--- |
| **Category** | maintainability |
| **Severity / Likelihood** | medium / almost-certain → score **10** (high) |
| **Status** | open |
| **Description** | The repository at `/workspace/project` is empty: zero tracked files, zero commits, no build manifest, and no application code. Nothing can be built, run, or deployed, so every downstream activity is blocked until a codebase exists. |
| **Impact** | No deliverable can be produced from this workspace. Any delivery timeline depends entirely on the first code being written. |
| **Evidence** | `git ls-files` → no tracked files · `git log` → no commits yet · `find` → 0 files |
| **Mitigation** | Create the initial application scaffold with a dependency manifest, entry point, and README as the first change. |
| **Recommended action** | Initialize the project structure and commit an initial scaffold. |

### RISK-002 — No dependency manifest or lockfile

| Field | Detail |
| :--- | :--- |
| **Category** | dependency |
| **Severity / Likelihood** | medium / likely → score **8** (moderate) |
| **Status** | open |
| **Description** | No `package.json`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `go.mod`, `Cargo.toml`, or lockfile is present. There is therefore no pinned dependency set, no reproducible build, and no supply-chain surface to scan. Once dependencies are added without a lockfile, builds may pull unreviewed transitive versions. |
| **Impact** | Non-reproducible builds, unreviewed transitive dependencies, and exposure to dependency-confusion or typosquatting attacks later. |
| **Evidence** | filesystem scan → no manifest or lockfile of any ecosystem found |
| **Mitigation** | Add the ecosystem-appropriate manifest and lockfile, commit the lockfile, and enable automated dependency scanning (e.g. Dependabot or Renovate). |
| **Recommended action** | Introduce a manifest plus lockfile with the first code commit and wire dependency scanning into CI. |

### RISK-003 — No automated tests or CI pipeline

| Field | Detail |
| :--- | :--- |
| **Category** | testing |
| **Severity / Likelihood** | medium / likely → score **8** (moderate) |
| **Status** | open |
| **Description** | There is no test suite, test framework configuration, or CI workflow. Without automated verification, regressions cannot be caught, and quality gates cannot be enforced on future changes. |
| **Impact** | Defects reach users undetected; refactoring becomes risky; release confidence is low. |
| **Evidence** | filesystem scan → no test directories, test config, or CI workflow files |
| **Mitigation** | Adopt a test framework and add a CI workflow that runs lint, tests, and a build on every pull request. |
| **Recommended action** | Add a minimal test harness and a CI workflow before the codebase grows. |

### RISK-004 — Secrets present in the runtime environment

| Field | Detail |
| :--- | :--- |
| **Category** | security |
| **Severity / Likelihood** | medium / possible → score **6** (moderate) |
| **Status** | acknowledged |
| **Description** | The environment exposes credentials (`OPENHANDS_API_KEY`, `GITHUB_TOKEN`) as environment variables. If future code logs the environment, commits a `.env` file, or copies values into configuration, these secrets could be disclosed. |
| **Impact** | A leaked API key or repository token could allow unauthorized API access or repository modification. |
| **Evidence** | environment inspection → `OPENHANDS_API_KEY` and `GITHUB_TOKEN` are set |
| **Mitigation** | Add a `.gitignore` covering `.env` files, never log environment dumps, and use a secret manager or platform-injected secrets rather than committed values. |
| **Recommended action** | Add secret-hygiene rules and a `.gitignore` before any configuration code is written. |

### RISK-005 — No license declared

| Field | Detail |
| :--- | :--- |
| **Category** | licensing |
| **Severity / Likelihood** | low / likely → score **4** (low) |
| **Status** | open |
| **Description** | No `LICENSE` file exists, so the legal terms under which the project may be used, modified, or distributed are undefined. This blocks adoption and can create compliance ambiguity once third-party dependencies are added. |
| **Impact** | Unclear usage rights; potential license-compatibility conflicts with future dependencies. |
| **Evidence** | filesystem scan → no `LICENSE` file present |
| **Mitigation** | Choose and add an explicit license, and record a dependency-license policy. |
| **Recommended action** | Add a `LICENSE` file and note the chosen license in `project.json`. |

### RISK-006 — Default branch has no protection or review policy

| Field | Detail |
| :--- | :--- |
| **Category** | process |
| **Severity / Likelihood** | low / possible → score **3** (low) |
| **Status** | open |
| **Description** | The repository is on branch `master` with no commits and no configured remote. There is no branch protection, required review, or commit convention in place to prevent unreviewed or malformed changes once collaboration starts. |
| **Impact** | Unreviewed changes may land directly on the main branch; inconsistent history and weak accountability. |
| **Evidence** | `git branch` → only `master`, no commits · `git remote -v` → no remote configured |
| **Mitigation** | Once a remote exists, enable branch protection and require pull-request review; agree on a commit message convention. |
| **Recommended action** | Configure branch protection and review requirements when the remote repository is created. |

### RISK-007 — Application hosts are unreachable (HTTP 502)

| Field | Detail |
| :--- | :--- |
| **Category** | availability |
| **Severity / Likelihood** | low / possible → score **3** (low) |
| **Status** | open |
| **Description** | The two provisioned application hosts (work-1 and work-2) both return HTTP 502 Bad Gateway and no process is listening on the corresponding local ports. If a service is expected to run here, it is currently unavailable and its absence is not surfaced by any health check. |
| **Impact** | No application is reachable for testing or demonstration; automated checks against the host would fail with 502. |
| **Evidence** | `curl` work-1 → HTTP 502 · `curl` work-2 → HTTP 502 · no listeners on ports 12000/12001 |
| **Mitigation** | Confirm whether an application is expected on these hosts; if so, add a start command and a health-check endpoint. |
| **Recommended action** | Decide whether these hosts should serve the project, then provision a start command and health check accordingly. |

---

## 6. Issues (Known Gaps)

| ID | Title | Type | Category | Severity | Status | Detection |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ISSUE-001 | No README or project documentation | gap | documentation | medium | open | detected |
| ISSUE-002 | No .gitignore file | gap | process | medium | open | detected |
| ISSUE-003 | Security, quality, and dependency analysis could not be performed | gap | security | medium | open | not-detected |
| ISSUE-004 | No environment or configuration contract defined | gap | operational | low | open | inferred |

### ISSUE-001 — No README or project documentation

| Field | Detail |
| :--- | :--- |
| **Type / Severity** | gap / medium |
| **Status** | open |
| **Description** | The repository contains no README, no contributor guide, and no documentation of any kind. A newcomer has no entry point for understanding or running the project. |
| **Root cause** | Project has not been scaffolded yet. |
| **Evidence** | filesystem scan → no `.md` files in the repository |
| **Recommended fix** | Add a README describing purpose, setup, and usage, and keep it in sync with the project summary spec. |

### ISSUE-002 — No .gitignore file

| Field | Detail |
| :--- | :--- |
| **Type / Severity** | gap / medium |
| **Status** | open |
| **Description** | No `.gitignore` exists. Build artifacts, dependency directories, editor files, and local environment files (including `.env`) risk being committed accidentally. |
| **Root cause** | Project has not been scaffolded yet. |
| **Evidence** | filesystem scan → no `.gitignore` present |
| **Recommended fix** | Add a `.gitignore` appropriate to the chosen ecosystem, including `.env` and secret-bearing files. |

### ISSUE-003 — Security, quality, and dependency analysis could not be performed

| Field | Detail |
| :--- | :--- |
| **Type / Severity** | gap / medium |
| **Status** | open |
| **Description** | Static analysis for vulnerabilities, code-quality problems, and dependency CVEs was not possible because there is no source code, manifest, or lockfile to analyze. The security posture of the eventual project is therefore entirely unverified. |
| **Root cause** | Absence of a codebase. |
| **Evidence** | analysis attempt → no analyzable artifacts found in the workspace |
| **Recommended fix** | Once code and manifests exist, run a SAST scan, a dependency CVE scan, and a linter, and record findings in this register. |

### ISSUE-004 — No environment or configuration contract defined

| Field | Detail |
| :--- | :--- |
| **Type / Severity** | gap / low |
| **Status** | open |
| **Description** | There is no documented list of required environment variables, no example configuration file, and no validation of configuration at startup. Only runtime-injected variables currently exist, and they are platform-provided rather than project-defined. |
| **Root cause** | Project has not been scaffolded yet. |
| **Evidence** | environment inspection → only OpenHands runtime variables present; no project configuration files |
| **Recommended fix** | Add a `.env.example` and fail fast at startup when required configuration is missing. |

---

## 7. Analysis Coverage

**Checks performed**

- Filesystem inventory (tracked and untracked files)
- Git repository state (commits, branches, remotes)
- Dependency manifest and lockfile discovery
- Test suite and CI workflow discovery
- License and documentation file discovery
- Runtime environment variable inspection
- Application host reachability (HTTP) and local port listening check

**Checks not possible**

| Check | Reason |
| :--- | :--- |
| Static application security testing (SAST) | no source code present |
| Dependency vulnerability scan (SCA) | no manifest or lockfile present |
| Secret scanning of committed history | no commit history present |
| Test coverage measurement | no tests present |
| Runtime performance and error-rate analysis | no application running (hosts return HTTP 502) |

```
  Coverage map
  ┌────────────────────────────────┬────────────┐
  │ filesystem inventory           │  ✔ done    │
  │ git repository state           │  ✔ done    │
  │ manifest / lockfile discovery  │  ✔ done    │
  │ test + CI discovery            │  ✔ done    │
  │ license / docs discovery       │  ✔ done    │
  │ env variable inspection        │  ✔ done    │
  │ host reachability (HTTP)       │  ✔ done    │
  ├────────────────────────────────┼────────────┤
  │ SAST (source code)             │  ✘ blocked │
  │ SCA (dependencies)             │  ✘ blocked │
  │ secret scan (history)          │  ✘ blocked │
  │ test coverage                  │  ✘ blocked │
  │ runtime performance            │  ✘ blocked │
  └────────────────────────────────┴────────────┘
```

---

## 8. Provenance

| Field | Value |
| :--- | :--- |
| Generated at | 2026-09-23T03:48:33Z |
| Generator | OpenHands agent (codebase and environment analysis) |
| Confidence | `high` |
| Sources | filesystem inspection of `/workspace/project`; git repository state; runtime environment variables; HTTP probes of provisioned application hosts |
