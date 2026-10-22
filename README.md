# Harvesta

**Plant trees. Track impact. Offset carbon.**

Harvesta connects tree sponsors with farmers, community groups, and other planters. Built around Stellar and Soroban, the platform combines tree sponsorship, planting updates, and estimated carbon-impact tracking.

> Proudly supported by [Fundable Finance](https://fundable.finance).

## What you can do

- **Sponsor trees** and support planting projects in selected regions.
- **Make donations**, including anonymous donations where supported.
- **Track planting progress** through tree records and planter-submitted updates.
- **View estimated carbon impact** based on species and growth data.
- **Use the white-label embed** to offer carbon-offset purchases on another website.

## How it works

1. A sponsor chooses a planting project, tree species, and quantity.
2. The sponsor completes payment using the method available for that flow.
3. A planter accepts or completes planting work and submits progress evidence, such as photos and location information.
4. The platform records progress and updates the sponsor's impact view. Escrow and payout behavior depends on the contract and payment flow in use.

## White-label carbon-offset embed

Organizations can embed a branded carbon-offset purchase widget on their own websites. The widget lists the company's active projects and sends customers to Stripe Checkout. A signed Stripe webhook updates the project's off-chain credit inventory after payment; this embed checkout does **not** mint a Stellar token or carbon-credit NFT.

Start with the [Carbon Offset Website Embed guide](docs/carbon-offset-embed.md) for embed-key setup, allowed domains, checkout configuration, and webhook handling.

## Technology

| Area | Technology |
|---|---|
| Web application and API | Next.js App Router, React, TypeScript |
| Styling | Tailwind CSS and shared UI components |
| Smart contracts | Rust and Soroban |
| Stellar integration | Stellar SDK |
| Data | PostgreSQL |
| Carbon estimates | Species growth data and published methodology |
| Payments and embeds | Stripe Checkout and signed webhooks |

The repository contains several contracts, including tree registry, escrow, planter registry, and carbon-credit components. See [`contracts/`](contracts/) for the full workspace.

## Getting started

### Prerequisites

- Node.js 20 or newer
- pnpm (the repository uses pnpm)
- Rust stable and Cargo for smart-contract work
- PostgreSQL and the required environment variables for database-backed features

### Run the web app

```bash
git clone https://github.com/Aonlike/stellar-app-os.git
cd stellar-app-os
pnpm install
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000). Configure the values needed for your local setup using [`.env.example`](.env.example). Do not commit secrets or expose server-side credentials through client-side environment variables.

### Build the Soroban contracts

Install the WebAssembly target once, then build the contract workspace:

```bash
rustup target add wasm32-unknown-unknown
cd contracts
cargo build --target wasm32-unknown-unknown --release
```

Configure the Stellar network, account, and contract IDs for your deployment before deploying. Do not use production credentials or mainnet for local development.

## Useful commands

| Command | Description |
|---|---|
| `pnpm dev` | Start the Next.js development server |
| `pnpm build` | Build the web application |
| `pnpm start` | Start the production server |
| `pnpm typecheck` | Run the TypeScript type checker |
| `pnpm test` | Run the Vitest test suite |
| `pnpm lint` | Run ESLint |
| `pnpm db:migrate` | Apply database migrations |

## Carbon impact estimates

Carbon figures are estimates, not guaranteed credits or measured removals. Harvesta's methodology uses published species growth data, including FAO/IPCC Tier 1 references, and should be interpreted with the uncertainty and regional limits described in the [climate impact methodology](docs/research/climate-impact-methodology.md).

## Documentation

- [System architecture](docs/ARCHITECTURE.md)
- [Planter onboarding and tree verification](docs/PLANTER_ONBOARDING_GUIDE.md)
- [Carbon-offset website embed](docs/carbon-offset-embed.md)
- [Public API reference](docs/PUBLIC_API.md)
- [Interactive API documentation](/api-docs)
- [OpenAPI specification](docs/openapi.yaml)

## Contributing

Contributions are welcome. Please open an issue to discuss significant changes, and run the relevant checks before submitting a pull request:

```bash
pnpm typecheck
pnpm test
pnpm lint
```

## License

Apache 2.0
