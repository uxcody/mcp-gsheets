# mcp-gsheets

TypeScript MCP server for Google Sheets API integration. Read, write, format, and manage Google Sheets via Claude or any MCP client.

## Stack
- TypeScript 5+, Node 20+, MCP SDK 1.x, googleapis v4
- Transport: stdio only (`src/index.ts` → `StdioServerTransport`)
- Auth: Google service account (3 methods — see below)
- Build tool: tsup, test runner: vitest

## Structure
- `src/tools/` — MCP tool implementations
- `src/utils/` — Google auth, error handling, range helpers
- `src/config/` — constants (scopes, retry config, batch limits)
- `src/types/` — shared TypeScript types
- `tests/` — vitest test suite (485 tests)
- `dist/` — compiled output (entry: `dist/index.js`)

## Commands
- Build: `npm run build`
- Typecheck: `npm run typecheck`
- Test: `npm run test:run`
- Lint: `npm run lint`
- Dev: `npm run dev` (tsx watch)

## Auth environment variables (one method required)
1. `GOOGLE_APPLICATION_CREDENTIALS=/path/to/key.json` + `GOOGLE_PROJECT_ID`
2. `GOOGLE_SERVICE_ACCOUNT_KEY='{"type":"service_account",...}'` (JSON string)
3. `GOOGLE_PRIVATE_KEY` + `GOOGLE_CLIENT_EMAIL`

## Notes
- Spreadsheets must be shared with the service account email before Claude can access them
- Scope: `https://www.googleapis.com/auth/spreadsheets` (read + write)
- MCP server runs stdio-only; the HTTP/OAuth transport stack in the SDK is not used
- `dist/` is built and gitignored — run `npm run build` before running
