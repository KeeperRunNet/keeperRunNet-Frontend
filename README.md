# KeeperNet Frontend

The decentralized UI for the KeeperNet automation and relayer protocol.

KeeperNet Frontend is the **Next.js** web application that gives developers and users a seamless interface for creating automated smart contract triggers, tracking job execution, managing keeper nodes, and monitoring relayer health — all powered by **Soroban smart contracts** on the **Stellar network**.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Coming%20Soon-orange)](/)
[![Documentation](https://img.shields.io/badge/Docs-Read%20Now-blue)](/docs)
[![Contributing](https://img.shields.io/badge/Contributing-Welcome-green)](/CONTRIBUTING.md)
 [![License](https://img.shields.io/badge/License-MIT-purple)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active%20Development-yellow)](/)

---

## Core Features

| Feature | Description |
|--------|-------------|
| **Wallet Integration** | One-click Stellar wallet connection via Freighter |
| **Job Dashboard** | Create, fund, and track automated Soroban contract executions |
| **Network Explorer** | Browse global relayer statistics and active keeper node health |
| **Job Creation Wizard** | Multi-step form for block-height, time-based, or state-based triggers |
| **Execution Logs** | Monitor real-time transaction fulfillment and gas fee reimbursements |
| **Dark / Light Mode** | System-aware theme toggling |
| **Toast Notifications** | Non-blocking feedback for relayer updates and transaction states |
| **Responsive Design** | Mobile-first layout for managing infrastructure on the go |

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript 5 |
| Styling | Tailwind CSS 3 + CSS Modules |
| Blockchain | Stellar + Soroban |
| Wallet | Freighter |
| State Management | React Hooks + Context API + KeeperNet TS SDK |

---

## Available Routes

| Route | Description |
|-------|-------------|
| `/` | Landing page with protocol network stats |
| `/dashboard` | User dashboard — My Automation Jobs |
| `/dashboard/logs` | Execution history and relayer receipts |
| `/dashboard/settings` | Account and gas fee preferences |
| `/nodes` | Active keeper nodes and network health |
| `/create-job` | Multi-step automation job creation wizard |

---

## Project Structure

```text
├── app/
│   ├── layout.tsx          # App shell — providers, global styles, nav
│   ├── page.tsx            # Landing page entry point
│   ├── globals.css         # Global styles and CSS variables
│   ├── dashboard/          # Dashboard routes and layouts
│   ├── nodes/              # Keeper nodes health route
│   └── create-job/         # Job registration wizard route
├── components/
│   ├── atoms/              # Primitive UI: Button, Card, Input, StatusBadge, Toast
│   ├── molecules/          # Composed UI: JobCard, FormTrigger, TxModal, WalletData
│   └── organisms/          # Page-level sections: Navbar, JobBoard, RegistrationWizard
├── hooks/
│   ├── useAccount.ts       # Stellar wallet account state
│   ├── useSubscription.ts  # Real-time backend relayer event subscriptions
│   ├── useTheme.ts         # Dark/light theme management
│   ├── useToast.ts         # Toast notification queue
│   └── useIsMounted.ts     # SSR hydration safety guard
├── shared/
│   ├── contracts.ts        # Shared registry contract address constants
│   └── utils.ts            # XDR parsing and block-time utility functions
└── public/                 # Static assets and favicon
```

---

## Getting Started

### Prerequisites

- Node.js >= 18
- [Freighter Wallet](https://freighter.app) browser extension
- A funded Stellar testnet account

### Installation

```bash
npm install
```

### Environment Setup

```bash
cp .env.example .env.local
```

Configure the following variables in `.env.local`:

```env
NEXT_PUBLIC_STELLAR_NETWORK=TESTNET
NEXT_PUBLIC_SOROBAN_RPC_URL=https://soroban-testnet.stellar.org
NEXT_PUBLIC_KEEPER_REGISTRY_ID=your-registry-contract-id
NEXT_PUBLIC_INDEXER_API_URL=http://localhost:8000/api/v0
```

### Running

```bash
# Development
npm run dev

# Lint code
npm run lint

# Type-check
npm run typecheck

# Production build
npm run build

# Start production server
npm start
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Component Guide

### Atoms

Base-level, stateless UI primitives. Use these directly or compose them into molecules.

- **Button** — primary, secondary, and loading states
- **BlockInput** — numeric input for target block heights
- **StatusBadge** — visual indicator for job states (`Pending`, `Executed`, `Failed`)
- **Toast** — auto-dismissing notification bubble
- **ThemeToggle** — dark/light mode switcher

#### Using Toast Notifications

```tsx
import { useToast } from '@/hooks/useToast'

export default function MyComponent() {
  const toast = useToast()

  return (
    <button onClick={() => toast.success('Job successfully registered!')}>
      Show Toast
    </button>
  )
}
```

Available toast types: `toast.success()` · `toast.error()` · `toast.warning()` · `toast.info()`

---

### Molecules

Stateful compositions built from atoms.

- **FormTrigger** — full trigger condition form with validation
- **TransactionModal** — step-by-step XDR signature status overlay
- **WalletData** — connected wallet summary card
- **JobCard** — visual summary of an active or historical automation job

---

### Organisms

Full page sections wired to on-chain data.

- **Navbar** — responsive top nav with wallet connect
- **JobBoard** — grid display of user's scheduled executions
- **RegistrationWizard** — job setup workflow from input to confirmation

---

## Architecture Notes

**Next.js 16 App Router** — This project uses the modern App Router (`app/` directory). Layouts, error boundaries, and loading states are handled natively at the directory level. Components in `app/` are Server Components by default; add `"use client"` at the top of files that require React hooks or browser APIs.

**Data Fetching** — Relayer status and global node metrics are fetched server-side from the KeeperNet Rust backend. User-specific job state relies on client-side fetching via the KeeperNet TypeScript SDK after wallet authentication.

---

## Security

- No private keys ever touch the browser — all signing is delegated securely to **Freighter**
- Contract IDs and Backend RPC URLs are loaded strictly from **environment variables**
- XDR simulation runs before every job registration to estimate gas and catch Soroban panics early

---

## Roadmap

### About to start

- [ ] Landing page with protocol metrics
- [ ] Dark/Light mode theming
- [ ] Toast notification system
- [ ] User dashboard with sidebar navigation
- [ ] Multi-step job creation wizard
- [ ] Responsive mobile-first design
<!-- ### In Progress -->
- [ ] Wallet Integration [#21] — Full Freighter API integration
- [ ] KeeperNet SDK [#16] — Connect frontend to `keeper-net-sdk` npm package
- [ ] Relayer WebSockets [#10] — Real-time execution log streaming

### Planned

- [ ] Node UI — Dashboard for users running their own local relayer nodes
- [ ] Advanced Triggers — UI support for cross-contract state queries
- [ ] i18n Support — Multi-language support via `next-intl`
- [ ] Testnet interactions
- [ ] Multiple chains support
---

## Contributing

We welcome contributions from the community. Whether you're fixing bugs, adding features, or improving documentation, your help is appreciated.

### Quick Start for Contributors

1. **Find an issue** — Check [`good first issues`](../../labels/good%20first%20issue) or [`help wanted`](../../labels/help%20wanted)
2. **Read the guide** — See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed instructions
3. **Set up locally** — Follow the installation steps above
4. **Make your changes** — Create a feature branch and commit your work
5. **Submit a PR** — Open a pull request with a clear description

### Development Workflow

```bash
# 1. Fork and clone the repo
git clone https://github.com/YOUR_USERNAME/keepernet-frontend.git

# 2. Create a feature branch
git checkout -b feature/your-feature-name

# 3. Make changes and test
npm run dev
npm run lint
npm run typecheck
npm run build

# 4. Commit and push
git commit -m "feat: add your feature"
git push origin feature/your-feature-name
```

We are actively seeking contributors with experience in:

- Stellar / Soroban smart contracts
- React / Next.js (App Router)
- Indexers and transaction relayers

---

## Community and Support

- **Documentation** — [Full Docs](/docs)
- **Issues** — [Report bugs or request features](../../issues)
- **Discussions** — [Stellar Community Forum](https://community.stellar.org)

---

## Project Status

This project is under **active development**. The UI foundation is complete and ready for `keeper-net-sdk` integration.

---

## License

MIT License — Copyright (c) 2026 KeeperNet Protocol.

---

*Automating the future of Soroban, one block at a time.*
