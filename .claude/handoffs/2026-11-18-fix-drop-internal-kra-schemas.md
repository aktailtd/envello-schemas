# Drop internal KRA schemas from @envello/schemas

**Goal:** stop the published package exporting the internal CEO dashboard (KRA) schemas. The monorepo's own `packages/schemas` copy is untouched; the API and dashboard keep using it.

**What changed:**
- `src/kra.ts`: deleted. Internal ops schemas, never public API.
- `src/index.ts`: removed `export * from "./kra.js"`.
- `package.json`: `build` now runs `rm -rf dist` before `tsc`, so a stale local `dist/kra.*` can't ride along in a tarball. `files` and `exports` already only expose `dist` and `.`, so no other change there.

**Decisions:**
- No CHANGELOG entry: the repo has no changelog file and adding one wasn't in scope. Note the breaking removal in the release notes instead.
- No sync script exists in this repo, so nothing to make skip `kra.ts`. If files get copied over by hand from the monorepo, leave `kra.ts` out.
- No version bump, tag or publish. Publishing is the owner's call.

**State:** merged but not published: 0.1.2 on npm still contains kra until a new version is published, and consider `npm deprecate @envello/schemas@0.1.2`. Both are the owner's decision. The next release should be a breaking bump (0.2.0) since exports were removed.

**Verify:**
- `pnpm build && pnpm typecheck` passes.
- `npm pack --dry-run 2>&1 | grep -ci kra` prints `0`.
- `grep -rni kra src` returns nothing.

**Gotchas:**
- There is no test script in this repo, so there are no tests to run.
- README says the package is published from the monorepo, but releases actually go from this repo (`scripts/release.sh` pushes a tag, `.github/workflows/publish.yml` publishes). The monorepo copy is at 0.1.0 and still has `kra.ts`; publishing from there would bring it back.
