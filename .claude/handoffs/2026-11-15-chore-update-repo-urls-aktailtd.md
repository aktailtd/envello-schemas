# Update repo URLs to aktailtd

**Goal:** the repo moved from Bergblumestudio to the `aktailtd` org; point metadata at the new home.

**What changed:** package.json : replaced `github.com/Bergblumestudio/` with `github.com/aktailtd/`.

**Decisions:** URL-only change, no version bump; publishing a release is left to the owner.

**State:** done. Same change opened on all six envello SDK repos.

**Verify:** `grep -ri bergblume .` returns nothing.

**Gotchas:**
- GitHub redirects old URLs only until a repo is created at the old path.
- README still links the monorepo at aktailtd/envello on purpose: that repo has not moved.
