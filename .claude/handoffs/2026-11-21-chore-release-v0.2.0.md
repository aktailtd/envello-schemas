# Handoff: release v0.2.0

**Goal.** Ship the security fixes merged since the July release, and get npm/PyPI/Go metadata pointing at aktailtd.

**What changed.** Version bumped to 0.2.0 (minor: fix! dropped the internal kra* schemas (breaking under 0.x)).

**Decisions.** Repo history was rewritten on 2026-11-21 to remove personal author data; the originals are private `aktailtd/envello-schemas-archive`. Never push old history back.

**State.** PR open. After merge: tag `v0.2.0` on master. Publishing: tag push runs publish.yml (npm OIDC trusted publishing); needs the npm trusted publisher set to aktailtd/envello-schemas, publish.yml.

**Verify.** pnpm build && pnpm typecheck (no test suite). After tagging, check the Actions run and the registry page shows 0.2.0 with repository aktailtd/envello-schemas.

**Gotchas.** The July releases were published with tokens (no provenance); this is the first trusted-publishing release, so a failed publish most likely means the trusted publisher isn't configured yet. Re-run the workflow after fixing, no new tag needed.
