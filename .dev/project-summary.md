# Research Summary: cursor-chat-browser

- **Date**: 2026-03-06
- **Tech Stack**: Next.js 14 (App Router), TypeScript, Tailwind CSS, shadcn/ui, better-sqlite3, Puppeteer
- **Origin**: Fork of [thomas-pedersen/cursor-chat-browser](https://github.com/thomas-pedersen/cursor-chat-browser)
- **State**: Working
- **Completion**: ~90% — fully functional, actively maintained upstream
- **Branch**: main @ 126d1a5

## What It Is

A Next.js web app that reads Cursor editor's local SQLite databases to let you browse, search, and export your AI chat and Composer conversation histories. It auto-detects the workspace storage path across macOS, Windows, WSL2, and Linux, and supports exporting conversations to Markdown, HTML, and PDF.

## Current State

The app is fully functional. The most recent commit (Dec 2024) added compatibility for Cursor 0.43.x, suggesting active maintenance tracking upstream Cursor changes. All core features are implemented: workspace browsing, chat/composer log viewing, full-text search with type filters, multi-format export, dark/light mode, and syntax-highlighted code blocks. No TODOs or FIXMEs in the source. No test suite exists. Tim's fork is 1 commit ahead of upstream (the 0.43.x compatibility fix, merged via PR from a third-party contributor).

## Potential

This is a genuinely useful developer tool — Cursor doesn't offer any native way to browse or export chat histories, so this fills a real gap. The upstream project has attracted external contributors (PRs for copy-all, workspace path fixes, compatibility fixes), indicating real user demand. The fork's only notable divergence from upstream is pulling in that compatibility hotfix. There's no novel architecture here, but the utility is solid and well-scoped.

## Recommendation

**Action**: Maintain

Tim's fork appears to exist primarily to track upstream with the 0.43.x fix merged before the upstream author did. The project is working well as-is. The main risk is bit-rot as Cursor evolves its internal database schema — this has already happened once (0.43.x). Concrete next steps:

1. Keep an eye on upstream PRs for Cursor schema changes and pull them in promptly.
2. Consider adding a test fixture (a sample SQLite DB) and basic integration tests to catch schema-breakage early.
3. If you want to differentiate the fork, a packaged Electron or menu-bar app wrapper would be a natural next step — eliminating the need to run a dev server manually.
