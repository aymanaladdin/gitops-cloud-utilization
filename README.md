# 🚀 GitOps & Cloud Utilisation — 3-Month Roadmap (README)

This repository tracks a focused 12-week journey to master **GitOps**, **Cloud Utilisation**, **FinOps**, **Reliability**, and **Infrastructure as Code (IaC)**. Designed for a senior engineer, it emphasizes production-grade practices and measurable outcomes.

---

## 🎯 Learning Goals

- Operate Kubernetes with **GitOps** as the single source of truth.
- Master **IaC** (Terraform or Pulumi) for end-to-end, reproducible infrastructure.
- Apply **FinOps** to control and optimize cloud spend.
- Build **Reliability** guardrails: observability, autoscaling, progressive delivery, chaos testing, SLOs, DR.
- Produce a **portfolio-ready capstone** that demonstrates all of the above.

---

## 🧭 How to Use This Repo

- Track progress by ticking checkboxes `[ ] → [x]`.
- Each month has **Detailed Outcomes** with **Evidence Artifacts** you must produce.
- Each week has **tasks, deliverables, and resource links**.
- Keep docs in `/docs`, IaC in `/iac`, app manifests in `/manifests`, dashboards/policies under `/ops`.

```text
repo/
  docs/            ← architecture notes, runbooks, DR plan, SLOs
  iac/             ← Terraform/Pulumi code (VPC, cluster, DB, monitoring, budgets)
  manifests/       ← Kubernetes app/env manifests (dev/stage/prod) for GitOps
  ops/             ← Grafana dashboards, Alertmanager configs, OPA/Kyverno policies
  .github/workflows/ or ci/  ← CI for app + IaC pipelines
```

---

## 📅 Roadmap Overview

- **Month 1:** GitOps & Cloud-Native Foundations
- **Month 2:** IaC, Observability & Reliability
- **Month 3:** FinOps, Security & Advanced Reliability

---

## ✅ Month 1 — GitOps & Cloud-Native Foundations

**Goal:** Boot a managed K8s cluster, wire **GitOps** from day one, and begin IaC.

### Learning Activities

- Install and configure **Argo CD** (or Flux CD).
- Deploy a demo app; drive changes via **PRs**; test rollback from Git.
- Create **multi-environment** structure (dev/stage/prod) with app + config separation.
- Provision a **managed K8s** cluster (EKS/GKE/AKS).
- Begin **Terraform**: VPC/network + cluster provisioning.

### Detailed Outcomes (Measurable)

- [ ] **Git-driven deployments**: Any manifest change merged to `main` reconciles automatically within ≤5 minutes; rollback performed by reverting a commit.
- [ ] **Multi-env strategy**: Clear separation of envs (folders or branches) + per-env overlays (Kustomize or Helm) with sealed/external secrets.
- [ ] **Managed cluster online**: Public endpoint reachable; baseline namespaces `{platform, dev, stage, prod}` created by GitOps.
- [ ] **Terraform baseline**: Idempotent `apply` creates VPC + K8s + node groups; `destroy` fully tears down (no orphans).

### Evidence Artifacts (to commit under `docs/` & `manifests/`)

- Architecture note: **gitops-topology.md** (repos, app of apps, env structure).
- **runbook-deploy-rollback.md** with exact commands/screens.
- **terraform-baseline.md** with state backend, workspaces, and module layout.

---

## ✅ Month 2 — IaC, Observability & Reliability

**Goal:** Expand IaC to full infra; add observability; implement autoscaling and progressive delivery; validate resilience.

### Learning Activities

- Extend **Terraform** modules (VPC, DB/cache, cluster, monitoring, budgets).
- Integrate **CI/CD**: GitHub Actions (or Terraform Cloud) for IaC pipelines; Argo CD for app delivery.
- Install **Prometheus + Grafana** (metrics) and **Loki/EFK** (logs).
- Configure **HPA** and **Cluster Autoscaler**.
- Use **Argo Rollouts** for **canary/blue-green** strategies.
- Run **chaos experiments** (LitmusChaos/Gremlin): pod kill, network latency.

### Detailed Outcomes (Measurable)

- [ ] **IaC owns infra**: No manual clicks; changes only via PRs. A fresh account/ project can be bootstrapped end-to-end in ≤60 minutes.
- [ ] **Observability SLIs**: Grafana shows **latency (p50/p95)**, **error rate**, **saturation**; logs are searchable by app, env, and trace ID.
- [ ] **Autoscaling**: HPA responds to CPU/RAM or custom metrics; cluster scales nodes under load; capacity graphs recorded.
- [ ] **Progressive delivery**: Canary deploy routes ≤10/30/100% with auto/Manual promotion; rollback under 2 minutes.
- [ ] **Resilience**: At least **3 chaos experiments** executed with documented hypotheses and outcomes.

### Evidence Artifacts

- **observability-dashboards.md** with screenshots + panel JSON exports (commit to `/ops/dashboards`).
- **rollouts-canary-plan.md** with traffic steps, abort criteria, rollback steps.
- **chaos-experiments.md** (hypothesis → method → expected vs. actual → follow-ups).

---

## ✅ Month 3 — FinOps, Security & Advanced Reliability

**Goal:** Optimize cost, enforce guardrails, define SLOs, and prove full DR from Git.

### Learning Activities

- **FinOps**: Install **Kubecost**, set **budgets** and **anomaly alerts**; rightsizing; spot/preemptible strategies.
- **Security/Policy**: **OPA Gatekeeper** or **Kyverno** (mandatory limits, disallow privileged, enforce namespaces/labels); IAM/RBAC mapping.
- **Reliability**: Define **SLIs/SLOs/SLAs**; DR: restore entire stack from Git + IaC; incident playbooks.

### Detailed Outcomes (Measurable)

- [ ] **Cost visibility**: Kubecost shows per-namespace/team spend; weekly cost report auto-generated; budget alerts fire on breach.
- [ ] **Rightsizing**: Requests/limits tuned to <20% headroom on average with controlled p95 throttling; spot usage quantified.
- [ ] **Policy as code**: At least **5 enforced policies**; PRs failing when violations occur; exemption workflow documented.
- [ ] **SLOs live**: SLI queries defined; Grafana SLO dashboard with burn-rate alerts (e.g., 1h and 6h windows).
- [ ] **DR proof**: New environment bootstrapped **100% from Git** (IaC + GitOps) in ≤90 minutes; recovery steps documented and rehearsed.

### Evidence Artifacts

- **finops-report-YYYY-MM.md** with snapshots and key findings.
- **policy-catalog.md** with links to rego/kyverno rules and rationale.
- **slos-and-burn-rates.md** including alert rules.
- **dr-playbook.md** with stopwatch timings and pitfalls.

---

## 🗂 Weekly Sprint Breakdown (with Resources)

| Week         | Focus Area           | Learning Tasks                            | Hands-On Deliverables                                            | Resources                                           | Checkpoint |
| ------------ | -------------------- | ----------------------------------------- | ---------------------------------------------------------------- | --------------------------------------------------- | ---------- |
| **1**  | GitOps basics        | Argo CD/Flux concepts; reconcile/rollback | Install Argo CD locally; deploy demo app; rollback by Git revert | Argo CD GitOps Bootcamp (Udemy); Argo CD Docs       | [ ]        |
| **2**  | Managed K8s          | Create EKS/GKE/AKS cluster                | Cloud cluster online; Argo CD targets it; demo app deployed      | GKE Quickstart / EKS Workshop                       | [ ]        |
| **3**  | IaC intro            | Terraform basics; remote state            | `iac/` provisions VPC+cluster; idempotent `apply/destroy`    | Terraform Associate prep; Terraform on AWS with EKS | [ ]        |
| **4**  | Multi-env GitOps     | Dev/stage/prod overlays; secrets mgmt     | Deploy across ≥2 envs; sealed/external secrets wired            | Argo CD Multi-cluster guide; Kustomize/Helm docs    | [ ]        |
| **5**  | IaC expansion        | Modules for DB, networking, monitoring    | VPC/DB/Cluster modules; pipelines for plan/apply                 | TF Modules best practices; Pulumi vs TF (optional)  | [ ]        |
| **6**  | Observability        | Prometheus/Grafana fundamentals           | Metrics + 3 dashboards (latency, errors, saturation)             | Prometheus course (Pluralsight); Grafana tutorials  | [ ]        |
| **7**  | Logging & HPA        | EFK/Loki + HPA                            | Central logs; HPA scaling demo under load                        | Elastic EFK on K8s; K8s HPA docs                    | [ ]        |
| **8**  | Progressive delivery | Argo Rollouts                             | Canary/blue-green in staging with promotion/abort                | Argo Rollouts docs; Progressive Delivery guide      | [ ]        |
| **9**  | Chaos engineering    | Principles + 3 experiments                | Pod kill, network delay, node drain; results logged              | LitmusChaos docs; Principles of Chaos               | [ ]        |
| **10** | FinOps basics        | Kubecost; budgets; anomalies              | Cost report; budget alert; rightsizing PRs merged                | Kubecost install; LF Intro to FinOps                | [ ]        |
| **11** | Security guardrails  | OPA/Kyverno; RBAC/IAM                     | ≥5 enforced policies; failing PRs for violations                | Gatekeeper docs; Kyverno policies                   | [ ]        |
| **12** | Reliability wrap-up  | SLOs; DR rehearsal                        | Full rebuild from Git+IaC; DR/playbooks committed                | SRE Book; SRE Specialization (Coursera)             | [ ]        |

> **Tip:** Keep weekly demos in `/docs/demos/week-XX.md` with screenshots, commands, and links to PRs.

---

## 🎓 Core Courses & Reading (Suggested Track)

- **GitOps**: Argo CD GitOps Bootcamp (Udemy); Argo CD Docs.
- **Kubernetes**: GKE Quickstart or EKS Workshop (choose your cloud).
- **IaC**: Terraform Associate prep; *Terraform on AWS with EKS* (Stephane Maarek). Optional: Pulumi docs if TypeScript/Go preferred.
- **Observability**: *Cloud-Native Monitoring with Prometheus* (Pluralsight); Grafana Tutorials.
- **Progressive Delivery**: Argo Rollouts Docs.
- **Chaos**: LitmusChaos Docs; principlesofchaos.org.
- **FinOps**: Linux Foundation *Introduction to FinOps*; Kubecost docs.
- **Reliability**: *Site Reliability Engineering* & *The SRE Workbook* (Google SRE Books); Coursera SRE Specialization.
- **Security/Policy**: OPA Gatekeeper; Kyverno policy library.

---

## 🧪 Capstone — Acceptance Criteria

To complete the program, the repository must demonstrate:

1) **Reproducible Infra (IaC)**

   - `terraform apply` (or Pulumi) bootstraps VPC, K8s, node pools, budgets, DB/cache, and monitoring.
   - CI pipeline runs `plan` on PR and `apply` on main with approvals.
2) **GitOps Delivery**

   - Argo CD watches `manifests/`; App-of-Apps or per-service apps; health/status green; rollback is a Git revert.
3) **Observability**

   - Grafana dashboards for latency/error/saturation; logs joined via trace IDs; alert rules for critical services.
4) **Reliability**

   - HPA + cluster autoscaler proven under load; canary rollout with abort criteria; 3 chaos experiments documented.
5) **FinOps**

   - Kubecost shows namespace/team cost; monthly report; budget alerts; rightsizing PRs with before/after graphs.
6) **Security & Policy**

   - ≥5 enforced policies; failing checks block PRs; exception process documented.
7) **DR & SLOs**

   - End-to-end rebuild in ≤90 minutes from a clean project; SLOs with burn-rate alerts; DR playbook with timings.

---

## 🔎 Glossary (Quick Reference)

- **GitOps**: Ops via Git PRs; controllers reconcile desired vs. actual state.
- **IaC**: Infra described in code; idempotent; reviewable; versioned.
- **SLI/SLO/SLA**: Indicator, Objective, Agreement; use burn-rate alerts.
- **FinOps**: Cloud cost accountability; allocate, budget, optimize.
- **Progressive Delivery**: Safer releases via canaries/blue-green + policy.

---

## ✅ Progress Log

Use this checklist to mark overall completion:

- [ ] Month 1 outcomes achieved + artifacts committed
- [ ] Month 2 outcomes achieved + artifacts committed
- [ ] Month 3 outcomes achieved + artifacts committed
- [ ] Capstone acceptance criteria met

> Keep iterating. Treat this README as a living spec; update it as your architecture evolves.

---

## 📚 Detailed Resources per Month

### Month 1 — GitOps & Cloud‑Native Foundations

- **Argo CD (GitOps)**
  - Argo CD Documentation — concepts, Install, App-of-Apps: https://argo-cd.readthedocs.io/en/stable/
  - Argo CD Project Page (quick overview, UI tour): https://argoproj.github.io/cd/
  - Multiple Sources in one Application (monorepos / Helm + Kustomize): https://argo-cd.readthedocs.io/en/latest/user-guide/multiple_sources/
- **Managed Kubernetes (pick your cloud)**
  - GKE Quickstart — Create a cluster & deploy a workload: https://cloud.google.com/kubernetes-engine/docs/quickstarts/create-cluster
  - Deploy an app to a GKE cluster (Autopilot/Standard): https://cloud.google.com/kubernetes-engine/docs/deploy-app-cluster
  - AWS EKS Workshop — Introduction & Getting Started: https://www.eksworkshop.com/docs/introduction/  •  https://www.eksworkshop.com/docs/introduction/getting-started/
- **Infrastructure as Code (Terraform)**
  - Terraform Associate Learning Path (HashiCorp Learn): https://developer.hashicorp.com/terraform/tutorials/certification-003/associate-study-003
  - Provision a GKE Cluster with Terraform (end-to-end tutorial): https://developer.hashicorp.com/terraform/tutorials/kubernetes/gke

### Month 2 — IaC, Observability & Reliability

- **Terraform Modules & Pipelines**
  - Terraform Associate Prep (curated study & tutorials): https://developer.hashicorp.com/terraform/tutorials/certification-003
- **Metrics & Dashboards**
  - Prometheus Operator / kube‑prometheus‑stack (Helm chart): https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack
  - Prometheus Operator — Installing with Helm: https://prometheus-operator.dev/docs/getting-started/installation/
  - Grafana Tutorials & Fundamentals: https://grafana.com/tutorials/  •  https://grafana.com/tutorials/grafana-fundamentals/
- **Autoscaling**
  - Kubernetes Horizontal Pod Autoscaler (HPA): https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/
  - HPA Walkthrough: https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/
- **Progressive Delivery**
  - Argo Rollouts (Docs): https://argoproj.github.io/rollouts/  •  https://argo-rollouts.readthedocs.io/

### Month 3 — FinOps, Security & Advanced Reliability

- **FinOps / Cost Visibility**
  - Install Kubecost on EKS (AWS guide): https://docs.aws.amazon.com/eks/latest/userguide/cost-monitoring-kubecost.html
  - Kubecost Install (vendor docs): https://www.apptio.com/products/kubecost/install/
  - Introduction to FinOps (FinOps Foundation / Linux Foundation): https://learn.finops.org/introduction-to-finops
- **Policy as Code (Security)**
  - OPA Gatekeeper — Docs & Policy Library: https://open-policy-agent.github.io/gatekeeper/website/docs/  •  https://github.com/open-policy-agent/gatekeeper
  - Kyverno — Policies Library & Docs: https://kyverno.io/policies/  •  https://kyverno.io/
- **Reliability / SRE**
  - Google SRE Book (free online): https://sre.google/books/  •  TOC: https://sre.google/sre-book/table-of-contents/
  - The SRE Workbook (free online): https://sre.google/workbook/table-of-contents/
