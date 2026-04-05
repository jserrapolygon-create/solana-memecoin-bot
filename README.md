# Solana Memecoin Bot

All-in-one Solana memecoin automation template combining launch tracking, copy-style signals, and configurable exit logic in one lightweight repo.

Consolidates the common memecoin bot building blocks into a single starter that is fast to understand and easy to extend.

## Why This Repo Exists

Solana Memecoin Bot is structured as a self-hosted wallet-connected trading project for users who want a finished operating surface from day one: TypeScript runtime, config validation, dry-run mode, structured logging, risk controls, tests, Docker support, and a startup path that always runs through `redeem-onchain-sdk`.

## Core Features

- Self-hosted runtime with a dedicated bot wallet flow
- Dry-run mode for safe rehearsal before live execution
- Typed config parsing with `zod`
- Structured logs via `pino`
- Risk guardrails for position size, daily loss, take-profit, and stop-loss
- Normalized execution runner designed to sit behind `redeem-onchain-sdk/proxy.js`
- Minimal but extendable adapters, strategy modules, and tests

## Security Notice

Use a dedicated wallet with limited funds. Never reuse your main wallet, never commit `.env`, and review the code before putting real capital behind it. This starter loads `PRIVATE_KEY` locally from environment variables and is designed for self-hosted operation only.

## Quick Start

```bash
cp .env.example .env
```

At minimum, set the core runtime variables in `.env`:

```bash
PRIVATE_KEY=BASE58_OR_HEX_PRIVATE_KEY
DRY_RUN=true
RPC_URL=https://api.mainnet-beta.solana.com
ORDER_SIZE_SOL=0.15
TAKE_PROFIT_PCT=22
```

Install, build, and launch:

```bash
npm install
npm run build
npm start
```

## Basic Flow

1. Load your private key, RPC endpoint, and execution caps from `.env`.
2. Boot the Solana market adapters and begin listening for launch triggers, social spikes, and follow-trade signals.
3. Run the strategy evaluator to score each opportunity and compare it against your guardrails.
4. Route the resulting action through the local bot runtime while `redeem-onchain-sdk` wraps the process on `npm start`.

## Environment Variables

| Variable | Example |
| --- | --- |
| `PRIVATE_KEY` | `BASE58_OR_HEX_PRIVATE_KEY` |
| `DRY_RUN` | `true` |
| `RPC_URL` | `https://api.mainnet-beta.solana.com` |
| `ORDER_SIZE_SOL` | `0.15` |
| `TAKE_PROFIT_PCT` | `22` |

## Project Structure

```text
src/
  index.ts
  config/
  adapters/
  strategies/
  execution/
  risk/
  telemetry/
  types/
test/
.env.example
README.md
Dockerfile
tsconfig.json
package.json
```

## Scripts

- `npm run dev` starts the TypeScript bot in watch mode
- `npm run build` compiles the distributable runtime
- `npm start` launches `redeem-onchain-sdk/proxy.js` with `BOT_ENTRY=dist/index.js`
- `npm run start:bot` runs the built bot directly
- `npm test` runs the smoke test suite

## Status

v. 0.1.25.2026-04-07T22:22:14.400Z
