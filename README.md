# Mini LiqPass Quote API

Small TypeScript + Node.js service that exposes two endpoints to create and fetch simple insurance-like quotes and persists them in SQLite (via sql.js WASM).

## Install

```bash
npm install
```

## Run

### Development (with auto-reload via ts-node)

```bash
npm run dev
```

The server starts at `http://localhost:3000`.

### Production (build then run)

```bash
npm run build
npm start
```

## Test

### Run all tests once

```bash
npm test
```

### Run tests in watch mode (reruns on file change)

```bash
npx vitest --watch
```

### Run a specific test file

```bash
npx vitest run test/quotes.test.ts
```

### Run tests with a custom DB path (isolate test data)

```bash
DB_PATH=./data/test-quotes.db npm test
```

## API Examples

### Create a quote

Using curl:
```bash
curl -X POST http://localhost:3000/quote \
  -H "Content-Type: application/json" \
  -d '{"userId":"alice","principal":1000,"leverage":10,"durationHours":24}'
```

Using PowerShell:
```powershell
Invoke-RestMethod -Method POST -Uri http://localhost:3000/quote `
  -ContentType 'application/json' `
  -Body '{"userId":"alice","principal":1000,"leverage":10,"durationHours":24}'
```

### Fetch quotes for a user

Using curl:
```bash
curl http://localhost:3000/quotes/alice
```

Using PowerShell:
```powershell
Invoke-RestMethod http://localhost:3000/quotes/alice
```

## Notes

- **Database**: SQLite file created at `./data/quotes.db` by default. Override with `DB_PATH` env var.
- **Validation**: Implemented with [zod](https://zod.dev).
- **Database Library**: Uses [sql.js](https://sql.js.org) (WASM-based SQLite) for Node 22+ compatibility without native builds.
- **Testing**: Vitest + fetch API for HTTP tests.
- **TypeScript**: Strict mode enabled; all source in `src/`, tests in `test/`.
