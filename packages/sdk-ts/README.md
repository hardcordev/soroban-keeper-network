# @soroban-keeper-network/sdk

Typed TypeScript client for the Soroban Keeper Network `keeper-registry`
contract. This package is currently a **scaffold** (backlog 0151 / epic
E12): it ships build tooling, a `tsconfig.json`, and a placeholder export
so the ESM/CJS/`.d.ts` pipeline is proven end to end. The
`KeeperRegistryClient` and its per-entry-point methods land in the rest of
epic E12's issues.

## Workspace tooling decision

This package is a **standalone npm package**, not an npm/pnpm workspace
member — there is no root `package.json` in this repository. This matches
the existing convention for `examples/keeper-bot` and
`examples/batch-register`, which are each installed and built independently
with their own `node_modules`. Adopting workspaces would be a repo-wide
change affecting those packages too, which is out of scope for this
scaffold; it can be revisited later if the growing number of `packages/`
and `examples/` entries makes standalone installs unwieldy.

## Quick start

```bash
cd packages/sdk-ts
npm install
npm run build   # emits dist/cjs (CommonJS), dist/esm (ESM), and .d.ts declarations
npm test        # builds, then runs the require()/import smoke tests
```

## Layout

- `src/index.ts` — package entry point.
- `tsconfig.json` — shared compiler options.
- `tsconfig.cjs.json` / `tsconfig.esm.json` — per-target build configs.
- `test/` — `node --test` smoke tests, one exercising `require()` and one
  exercising `import`, against the built `dist/` output.
