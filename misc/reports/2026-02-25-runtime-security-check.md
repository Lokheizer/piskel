# Runtime & Security Check Report (2026-02-25)

## Scope
- Repository: `piskel`
- Goal: run the project, capture startup/runtime timings, and run dependency vulnerability checks.

## Runtime checks

### Development mode (`npm run dev`)
Command used:
```bash
npm run dev
```

Measured with scripted readiness probing against `http://localhost:9901/`:
- Startup to `connect:dev` ready: **2592 ms**
- Request 1 total: **0.061848 s**
- Request 2 total: **0.003519 s**
- Request 3 total: **0.004933 s**

### Production mode (`npm run prod`)
Command used:
```bash
npm run prod
```

Measured with scripted readiness probing against `http://localhost:9001/`:
- Startup to `connect:prod` ready: **10749 ms**
- Request 1 total: **0.011708 s**
- Request 2 total: **0.005298 s**
- Request 3 total: **0.003693 s**

## Security checks

### npm audit (online)
Command used:
```bash
npm audit --audit-level=low
```
Result:
- Failed due to environment/registry policy issue (`403 Forbidden` on npm advisory endpoint).

### npm audit (offline lockfile check)
Command used:
```bash
npm audit --package-lock-only --offline
```
Result:
- `found 0 vulnerabilities`

## Notes & risk interpretation
- The online advisory feed could not be queried from this environment, so the strongest vulnerability signal is unavailable.
- The offline lockfile-based audit reports no known issues in the local metadata.
- Recommendation: re-run `npm audit` in CI or a network context with full registry advisory access.
