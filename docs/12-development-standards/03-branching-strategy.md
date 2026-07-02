# Branching Strategy

## Purpose
Define the branching strategy for EduCore to support parallel development, stable releases, and efficient collaboration.

## Branch Types
- `main` – Production-ready code.
- `develop` – Primary integration branch.
- `feature/*` – New features.
- `bugfix/*` – Non-critical fixes.
- `hotfix/*` – Urgent production fixes.
- `release/*` – Release preparation.

## Rules
- Create feature branches from `develop`.
- Merge changes through pull requests.
- Protect `main` from direct commits.
- Delete merged feature branches.

## Success Criteria
- Branch naming is consistent.
- All merges are reviewed.
- Release history remains clean and traceable.