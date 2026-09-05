# OSS merges log — Rosh Ramadass (`roshpr`)

Living record of **merged** upstream contributions. Newest first.

**How to update:** when any PR merges, run the Document OSS merge skill and append an entry here. Do not list open/draft PRs.

---

## Index

| Merged (PT) | Repo | PR | Title | Merged by |
|-------------|------|-----|-------|-----------|
| 2026-09-04 | argoproj/argo-helm | [#4051](https://github.com/argoproj/argo-helm/pull/4051) | fix(argo-cd): add application-controller livenessProbe | mbevc1 |

---

**Summary**  
Added an **optional** `livenessProbe` for the Argo CD application-controller Deployment (dynamic cluster distribution) and StatefulSet. Probe is **off by default** so existing installs are unchanged — matching upstream’s decision to remove a hard-coded controller liveness probe because restarting an overloaded controller can be worse than leaving it up ([argoproj/argo-cd#9557](https://github.com/argoproj/argo-cd/pull/9557)). Operators opt in via:

```yaml
controller:
  livenessProbe:
    enabled: true
```

**Review arc**  
- mkilchhofer: required a values/README warning explaining why the probe is default-off.
- - jmeridth: agreed; also wanted looser `timeoutSeconds` and a rebase onto chart `10.8.0`.
  - - Follow-up from roshpr addressed warning + rebase + timeout; marked ready; merged by mbevc1.
   
    - **Owned by**
    - Argo Contrib (Chief of Staff coordinated). Cloud-agent assisted implementation on fork.
   
    - **Notes / lessons**
    - - Keep AI-assisted PRs **draft** until human review (Fabrizio / checklist).
      - - Document upstream rationale in values when a default looks “surprising.”
        - - Use the OSS contribution checklist for labels, docs, DCO, draft, CI.
         
          - ---

          <!-- Newest entries go above this line (after ## Entries) and also in the Index table -->

## Entries

### argoproj/argo-helm#4051 — application-controller livenessProbe

| Field | Value |
|-------|--------|
| **PR** | https://github.com/argoproj/argo-helm/pull/4051 |
| **Issue** | https://github.com/argoproj/argo-helm/issues/4042 |
| **Repo** | [argoproj/argo-helm](https://github.com/argoproj/argo-helm) |
| **Author** | [roshpr](https://github.com/roshpr) |
| **Merged** | 2026-09-04 21:37:31 UTC (~2:37pm PT) by [mbevc1](https://github.com/mbevc1) |
| **Base / head** | `main` ← `cursor/application-controller-liveness-probe-e424` (`17d94d69`) |
| **Diff** | 1 commit · +54 / −3 · 5 files |
| **Status at merge** | CI green; re-approvals after rebase from mkilchhofer + mbevc1 |
