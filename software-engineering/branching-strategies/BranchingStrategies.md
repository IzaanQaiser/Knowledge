# Branching Strategies

- Defines how teams use Git to manage features, bugs fixes, releases, and deployements in a manageable way

### It tells us:
- Where code goes at each stage of development
- What gets deployed into production
- How do teams avoid merge conflicrs
- How code is reviewed and released

### Branching Strategies Matter because...
- They encourage parallel development
- They reduce merge conflicts
- The improve code quality through review
- They enable faster bug fixes
- They support CI/CD pipelines
- They provide clean histories for releases and rollbacks


## 1. Git Flow
### Main Branches:
- `main` - Production-ready code
- `develop` - Integration branch for ongoing work

### Supporting Branches
- `feature/<name>` - For building features, branched from develop
- `release/<x.y.z>` - To prep stable code for release
- `hotfix/<name>` - For critical production bug fixes
- `bugfix/<name>` - For smaller, non-urgent bugs

### Good for:
- Larger teams, staged release processes
### Avoid if:
- You deploy continuously (too much overhead)


## GitHub Flow (Ideal for CI/CD and Web Apps)
### Main Branches:
- `main` - Always deployable

### Supporting Branches:
- `feature/<name>` - short-lived branches from `main`

### Flow:
1. Create a branch from `main` 
2. Code, commit, push
3. Open a pull request
4. Review, test, and merge into `main`
5. CI/CD automatically deploys main

### Good For:
- Startups, small teams, web apps, frequent deploys
### Avoid if:
- You need to maintain multiple versions


## Trunk-Based Development
### Main Branches:
- `main` or `trunk` - Single shared branch

### Supporting Branches:
- Temporary branches for small features (merged quickly or commited directly)

### Good For:
- High-velocity teams, real-time apps
### Avoid if:
- You work on long-lived features or large modules without feature flags


## Best Practices:
1. Keep branches short-lived to avoid stale code conflicts
2. Use pull requests with reviews before merging
3. **Automate tests on every PR**
4. Keep `main` always deployable
5. Use **clear branch names** for clarity
6. Delete branches after merging
7. Use feature flags for incomplete features on `main`