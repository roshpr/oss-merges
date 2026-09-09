# OSS merges log — Rosh Ramadass (`roshpr`)

Living record of **merged** upstream contributions. Newest first.

**How to update:** when any PR merges, run the Document OSS merge skill and append an entry here. Do not list open/draft PRs.

---

## Index

| Merged (PT) | Repo | PR | Title | Merged by |
|-------------|------|-----|-------|-----------|
| 2026-09-09 | falcosecurity/charts | [#1055](https://github.com/falcosecurity/charts/pull/1055) | fix(falco-talon): restart on rulesOverride change | poiana |
| 2026-09-04 | argoproj/argo-helm | [#4051](https://github.com/argoproj/argo-helm/pull/4051) | fix(argo-cd): add application-controller livenessProbe | mbevc1 |

---

## Entries

### falcosecurity/charts#1055 — falco-talon rulesOverride restart

| Field | Value |
|-------|--------|
| **PR** | https://github.com/falcosecurity/charts/pull/1055 |
| **Issue** | https://github.com/falcosecurity/charts/issues/955 |
| **Repo** | [falcosecurity/charts](https://github.com/falcosecurity/charts) |
| **Author** | [roshpr](https://github.com/roshpr) |
| **Merged** | 2026-09-09 15:04:24 UTC (~8:04am PT) by [poiana](https://github.com/poiana) |
| **Base / head** | `master` ← `cursor/fix-955-talon-rules-checksum-27e0` (`1eaf890a`); merge commit `8580f131` |
| **Diff** | 1 commit · +6 / −1 · 3 files |
| **Status at merge** | DCO yes; labels `kind/bug`, `area/falco-talon-chart`, `size/XS`, `lgtm`, `approved`; tide merged after leogr LGTM/approve |

**Summary** Added a `rules-checksum` pod-template annotation hashed from the rendered falco-talon rules ConfigMap (next to the existing `secret-checksum`), and bumped the chart 0.4.1 → 0.4.2 with a CHANGELOG entry. Rules are mounted with `subPath`, so Kubernetes does not refresh the file in a running pod; without a checksum-driven rollout, `helm upgrade` that only changes `rules.yaml` or `config.rulesOverride` left Falco Talon on stale rules until a manual restart.

**Review arc**
- Opened 2026-09-02; reviews requested from bencer and alacuku; DCO green from the start.
- Author follow-up (Sep 3): posted `/kind bug` and `/area falco-talon-chart` (template slash commands had been left quoted so labels never fired) and rewrote the PR body.
- No change requests. leogr approved with LGTM on 2026-09-09 (~8:03am PT), noting it matches the falco chart checksum pattern and that a rollout is required for `subPath` mounts. poiana applied `lgtm` + `approved` and merged minutes later.

**Owned by**
Falco Contrib. Cloud agent `bc-fb2f5786-7d40-4717-9932-9ebcc64a27e0` authored the branch; Chief of Staff transferred ownership after open.

**Notes / lessons**
- Uncomment `/kind` and `/area` in the Falco charts PR template (or post them as a comment) so Prow labels fire — quoted template lines do nothing.
- GitHub PAT cannot comment or edit upstream falcosecurity PRs (403); use the signed-in browser as `roshpr` for those.
- Keep falco-talon changes scoped to `charts/falco-talon` only; leave `secret-checksum` alone unless a reviewer asks.
- On merge: document in https://github.com/roshpr/oss-merges and tell Chief of Staff.

---

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

**Summary**  Added an **optional** `livenessProbe` for the Argo CD application-controller Deployment (dynamic cluster distribution) and StatefulSet. Probe is **off by default** so existing installs are unchanged — matching upstream’s decision to remove a hard-coded controller liveness probe because restarting an overloaded controller can be worse than leaving it up ([argoproj/argo-cd#9557](https://github.com/argoproj/argo-cd/pull/9557)). Operators opt in via:

```yaml
controller:
  livenessProbe:
    enabled: true
```

**Review arc**  
- mkilchhofer: required a values/README warning explaining why the probe is default-off.  
- jmeridth: agreed; also wanted looser `timeoutSeconds` and a rebase onto chart `10.8.0`.  
- Follow-up from roshpr addressed warning + rebase + timeout; marked ready; merged by mbevc1.

**Owned by**  
Argo Contrib (Chief of Staff coordinated). Cloud-agent assisted implementation on fork.

**Notes / lessons**  
- Keep AI-assisted PRs **draft** until human review.  
- Document upstream rationale in values when a default looks “surprising.”  
- Use the OSS contribution checklist for labels, docs, DCO, draft, CI.

---

<!-- Newest entries go above this line (after ## Entries) and also in the Index table -->
