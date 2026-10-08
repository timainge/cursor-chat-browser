# Roadmap: cursor-chat-browser

- **Date**: 2026-03-07
- **Target**: Open source release (polished, resilient fork)
- **Effort**: 2–3 days core work; +1 week if pursuing Electron wrapper

## Why This Target

The fork is already working and useful, but one Cursor schema change has already broken it once. Making it a well-maintained, differentiated fork means adding resilience against future breakage and giving it a clear identity beyond "upstream + one fix".

## Steps to Ship

### Phase 1: Resilience Against Schema Changes
- [ ] Create a `fixtures/` directory with a minimal sample SQLite DB (anonymized or synthetic) covering both chat and Composer schemas
- [ ] Write integration tests (Vitest or Jest) that read the fixture DB and assert the API routes return expected shapes
- [ ] Add a GitHub Actions CI workflow (`.github/workflows/ci.yml`) that runs the tests on push

### Phase 2: Fork Differentiation
- [ ] Update `README.md` to: clarify this fork's status, list what's been added vs upstream, and document how to stay current with upstream Cursor schema changes
- [ ] Add a `CHANGELOG.md` noting the 0.43.x compatibility fix and any future divergences
- [ ] Set up a GitHub upstream remote and document the sync process in `CONTRIBUTING.md`

### Phase 3: Optional — Electron / Menu-Bar Wrapper
- [ ] Scaffold a simple Electron shell (or `menubar` package) that boots the Next.js server and opens it in a frameless window
- [ ] Add a `package.json` build script using `electron-builder` targeting macOS `.dmg` and Windows `.exe`
- [ ] Update README with download/install instructions for the packaged app

## Claude Code Tooling

### Skills
- **claude-api**: Not directly applicable, but the Anthropic Agent SDK could be used to build a "summarize this conversation" feature on top of the exported chat data — a natural future addition.

### Plugins / MCP Servers
- **filesystem MCP**: Useful for generating the fixture SQLite database programmatically during test scaffolding without leaving the agent loop.
- **github MCP**: Speeds up monitoring upstream PRs for schema-change fixes and automating the sync PR workflow.

### Reference Material
- **Cursor release notes / changelog**: Primary signal for when internal DB schema changes — subscribe or scrape to detect breakage before users do.
- **better-sqlite3 docs**: Covers synchronous query patterns and how to open read-only DBs, relevant for writing fixture-based tests safely.
- **Vitest docs (vitest.dev)**: Preferred test runner for Next.js App Router projects; covers mocking `fs` and SQLite module boundaries cleanly.

## Success Criteria

- CI passes on every push, catching any mismatch between the fixture DB schema and the app's query logic
- The README clearly distinguishes this fork from upstream and explains the maintenance strategy
- Any future Cursor schema change can be diagnosed and fixed by running `npm test` locally before users report breakage
