# Technical Summary

> **Source:** [`tech.json`](./tech.json) &nbsp;·&nbsp; **Spec version:** 1.0.0 &nbsp;·&nbsp; **Generated:** 2026-09-23
> **Reusable across:** any app project &nbsp;·&nbsp; **Audience:** developers, architects, operations, security, agents

---

## 1. Project Reference

| Field | Value |
| :--- | :--- |
| Name | Unnamed Project |
| Slug | `unnamed-project` |
| Lifecycle stage | `greenfield` |
| Project summary | [`project.json`](./project.json) |

---

## 2. Stack Layers

The schema models a technology stack as ordered layers, from the code a
developer writes down to where it runs. Every layer uses the same reusable
**component** shape.

```
  ┌──────────────────────────────────────────────────────────────────────┐
  │  APPLICATION TYPES   web · mobile · desktop · service · cli · api    │
  ├──────────────────────────────────────────────────────────────────────┤
  │  LANGUAGES           (none declared)                                 │
  ├──────────────────────────────────────────────────────────────────────┤
  │  FRAMEWORKS          (none declared)                                 │
  ├──────────────────────────────────────────────────────────────────────┤
  │  RUNTIMES            (none declared)                                 │
  ├──────────────────────────────────────────────────────────────────────┤
  │  PACKAGE MANAGERS    (none declared)                                 │
  ├──────────────────────────────────────────────────────────────────────┤
  │  BUILD TOOLS         (none declared)                                 │
  ├──────────────────────────────────────────────────────────────────────┤
  │  DATA LAYER          databases · caches · message brokers            │
  │                      (none declared)                                 │
  ├──────────────────────────────────────────────────────────────────────┤
  │  INFRASTRUCTURE      containers · orchestration · cloud · ci/cd      │
  │                      (none declared)                                 │
  └──────────────────────────────────────────────────────────────────────┘
```

### Component shape (reused everywhere)

| Property | Type | Allowed values |
| :--- | :--- | :--- |
| `name` | string | — |
| `version` | string \| null | semver or range |
| `category` | string | layer/category label |
| `purpose` | string \| null | why it is used |
| `scope` | enum | `runtime` · `dev` · `build` · `test` · `optional` |
| `criticality` | enum | `critical` · `high` · `medium` · `low` |
| `license` | string \| null | — |
| `source` | string \| null | registry / URL |
| `notes` | string \| null | free text |

---

## 3. Declared Stack

| Layer | Components |
| :--- | :--- |
| Application types | — |
| Languages | — |
| Frameworks | — |
| Runtimes | — |
| Package managers | — |
| Build tools | — |
| Databases | — |
| Caches | — |
| Message brokers | — |
| Infrastructure | — |
| Containers | — |
| Orchestration | — |
| Cloud providers | — |
| CI/CD | — |

All layers are empty because no manifest, source file, or build configuration
exists in the workspace.

---

## 4. Architecture

| Field | Value |
| :--- | :--- |
| Style | — |
| Overview | — |
| Components | — |
| External integrations | — |

---

## 5. Dependencies

```
  ┌──────────────────────────┬──────────────────────────┐
  │      RUNTIME DEPS        │     DEVELOPMENT DEPS     │
  │                          │                          │
  │        (none)            │        (none)            │
  └──────────────────────────┴──────────────────────────┘
              │                          │
              └────────────┬─────────────┘
                           ▼
              Lockfile:        — (none)
              Manifest files:  — (none)
```

| Field | Value |
| :--- | :--- |
| Runtime dependencies | — |
| Development dependencies | — |
| Lockfile | — |
| Manifest files | — |

---

## 6. Tooling

| Tooling category | Components |
| :--- | :--- |
| Linters | — |
| Formatters | — |
| Type checkers | — |
| Test frameworks | — |
| Security scanners | — |
| Quality gates | — |

---

## 7. Configuration

**Config files:** none.

**Environment variables** (all are platform-provided by the OpenHands runtime,
not project configuration):

| Name | Required | Secret | Default | Description |
| :--- | :---: | :---: | :--- | :--- |
| `OH_VSCODE_PORT` | no | no | `60001` | Runtime-provided port for the embedded VS Code server. Supplied by the runtime, not the project. |
| `VSCODE_PORT` | no | no | `60001` | Runtime-provided VS Code port. Supplied by the runtime. |
| `OH_CONVERSATIONS_PATH` | no | no | `/workspace/conversations` | Runtime-provided path where conversation state is stored. Not a project configuration value. |
| `OPENHANDS_API_KEY` | no | **yes** | — | Runtime-injected credential for OpenHands Cloud API access. Managed by the platform; never commit a value. |
| `GITHUB_TOKEN` | no | **yes** | — | Runtime-injected GitHub authentication token. Managed by the platform; never commit a value. |

```
  ⚠  SECRETS PRESENT IN ENVIRONMENT
  ┌───────────────────────────────────────────────┐
  │  OPENHANDS_API_KEY   ████████████  (redacted) │
  │  GITHUB_TOKEN        ████████████  (redacted) │
  └───────────────────────────────────────────────┘
  Never log the environment, never commit .env files.
```

---

## 8. Deployment & Observability

| Aspect | Value |
| :--- | :--- |
| Deployment targets | — |
| Strategy | — |
| Artifacts | — |
| Ports | 12000, 12001 |
| Logging | — |
| Metrics | — |
| Tracing | — |
| Health checks | — |

```
  Deployment pipeline
  ┌────────┐   ┌────────┐   ┌─────────┐   ┌──────────┐
  │ build  │──▶│  test  │──▶│ package │──▶│  deploy  │
  └────────┘   └────────┘   └─────────┘   └──────────┘
       ▲                                        
       └── no pipeline defined (no CI/CD in workspace)
```

---

## 9. Provenance

| Field | Value |
| :--- | :--- |
| Generated at | 2026-09-23T03:48:33Z |
| Generator | OpenHands agent (codebase inspection) |
| Confidence | `high` |
| Sources | filesystem inspection of `/workspace/project` (no manifests found); runtime environment variable inspection; git repository state |
