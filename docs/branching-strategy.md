# Branching Strategy

## 1. Release model

*State how you release, then pick the strategy that follows from it. Choose by your release model, not by what is popular.*

The release model for this project is based on a cadence, with one version in production at a time. The cadence is determined by iterations, typically aligning with the project's development sprints.

It follows this Main, Dev, Feature branching strategy model: 

```text
Main <-- Production
  |
  +-- Dev <-- Pre-Production testing
       |
       +-- Feature/*
       +-- Doc/*
       +-- Refactor/*
       +-- Test/*
       +-- Hotfix/*
```
---

## 2. Branches

| Branch | Purpose | Lifetime | Who may push | Protected |
|---|---|---|---|---|
| `main` | Always releasable | Permanent | Nobody directly | Yes |
| `dev` | Testing global project before release | Permanent | The author | No | 
| `feature/*` | One change to improve the project | 1 Iteration | The author | No |
| `doc/*` | Modification to the documentation | 1 Iteration | The author | No |
| `refactor/*` | Performance optimisation | 1 Iteration | The author | No |
| `test/*` | Production fix that cannot wait | 1 Iteration| Whoever is on call | No |
| `hotfix/*` | Urgent production fix | Hours | The project owner | No |

---

## 3. Branch lifetime

Permanent branches are those that exist for the lifetime of the project, such as `main` and `dev`. 

Short-lived branches, like `feature/*`, `doc/*`, `refactor/*`, and `test/*`, are created for specific tasks and should be deleted once their purpose is fulfilled. This ensures a clean and manageable repository, reducing the risk of stale branches cluttering the project.

Hotfix branches are also short-lived and should be deleted after the fix has been merged into both `main` and `dev`.

---

## 4. Merging and protection

- **Merge method.** The merge method to use is squash merging.
- **Required checks.** Passing all CI checks are required before merging into `main`. For other branches, the required checks are the security and test checks.
- **Required reviews.** As this is a personal project, no formal code review is required. If the project grows or involves multiple collaborators each pull request must be reviewed by the project owner.
- **Push access to protected branches.** `main` and `dev` are protected, and nobody may push directly to them. The code owner is allowed to push urgent fixes when necessary. 

---

## 5. Hotfix path

A hotfix branch should branch from `main` and be named `hotfix/*`. The minimum review is one approval from the project owner. CI checks may be skipped only with the project owner's authorization. Once the fix is complete, it must be merged back into `main` immediately to ensure the next release includes the fix. 

Additionally, the hotfix should be merged into `dev` to keep it up to date with the latest changes.
