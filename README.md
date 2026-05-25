# Lockstep

**Milestone escrow for freelancers & clients**

Lock ETH on Sepolia; release payment to a freelancer only when the client approves each milestone. Full-stack demo: Foundry smart contract + React/wagmi frontend.

## Problem & solution

| | |
|---|---|
| **Problem** | Clients and freelancers struggle with trust: pay upfront vs. deliver first. |
| **Solution** | On-chain escrow locks funds; the client calls `approveMilestone` to release proportional ETH per milestone. |

## Architecture

```
React (wagmi)  →  Escrow.sol  →  Sepolia testnet
```

## Project structure

```
├── contracts/          # Foundry: Escrow.sol, tests, deploy script
├── frontend/           # Vite + React + wagmi UI
└── README.md
```

## Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [Foundry](https://book.getfoundry.sh/getting-started/installation) (`forge`, `cast`)
- MetaMask (or similar) on **Sepolia**
- [Alchemy](https://www.alchemy.com/) API key
- [WalletConnect Cloud](https://cloud.walletconnect.com/) project ID (for WalletConnect)

## Smart contracts

### Install Foundry (if needed)

```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

On Windows, use [Foundry releases](https://github.com/foundry-rs/foundry/releases) or WSL.

### Run tests

```bash
cd contracts
forge test -vv
```

### Deploy to Sepolia

1. Copy `contracts/.env.example` → `contracts/.env`
2. Add `PRIVATE_KEY`, `SEPOLIA_RPC_URL`, `ETHERSCAN_API_KEY`
3. Fund deployer with Sepolia ETH ([faucet](https://sepoliafaucet.com/))

```bash
cd contracts
forge script script/Deploy.s.sol:DeployScript --rpc-url sepolia --broadcast --verify -vvvv
```

4. Copy deployed address into `frontend/.env` as `VITE_ESCROW_ADDRESS`

## Frontend

```bash
cd frontend
cp .env.example .env
# Edit: VITE_ALCHEMY_API_KEY, VITE_ESCROW_ADDRESS, VITE_WALLETCONNECT_PROJECT_ID
npm install
npm run dev
```

Open http://localhost:5173, connect wallet on Sepolia, create an escrow.

### Demo flow (certification video)

1. **Elevator pitch** — “Lockstep: milestone escrow on Sepolia”
2. **Problem** — trust in freelance payments
3. **Solution** — locked ETH + milestone releases
4. **Demo** — connect → create & fund → approve milestone → Etherscan
5. **Tech** — Foundry tests, Solidity, wagmi

## Deployed contract

| Network | Address |
|---------|---------|
| Sepolia | _Set after deploy — update this table and `frontend/.env`_ |

## Certification submission

- [ ] Record ≤5 min video (pitch, problem, solution, live demo)
- [ ] Submit form on [AU EVM certification](https://university.alchemy.com/certifications/evm-chain) → Project Submission tab
- [ ] Optional: deploy frontend to Vercel and link in submission

See [SUBMISSION.md](./SUBMISSION.md) for video script and checklist.

## Resources

- [AU EVM resources](https://university.alchemy.com/certifications/evm-chain?tab=resources)
- [Alchemy Builders Discord](https://discord.com/invite/alchemy-builders)

## License

MIT
