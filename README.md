# GenDuel

GenDuel is a GenLayer staked-debate court: two parties enter a motion, commit matching GEN stakes, submit opposing cases, and let an intelligent contract adjudicate the record with live web evidence, LLM reasoning, validator-comparative consensus, challenges, appeals, settlement, and reputation.

This repository contains the static product UI, the deployed Studionet contract source, deployment metadata, smoke transaction evidence, and tests.

## Live System
| Surface | Link |
| --- | --- |
| **App** | [https://genduel.vercel.app](https://genduel.vercel.app) |
| **GitHub** | [https://github.com/Dark-Brain07/genduel](https://github.com/Dark-Brain07/genduel) |
| **Contract** | [View on GenLayer Studio Explorer](https://explorer-studio.genlayer.com/address/0xeC412B00bc5E5999cb3D7EDD6cE1BB354B59C598) |
| **Vercel Project** | [View Vercel Dashboard](https://vercel.com/md-raju-ahmeds-projects-a8ce4550/genduel) |

## What GenDuel Proves
GenDuel turns a debate into a verifiable dispute lifecycle:

1. A creator opens a duel and stakes GEN.
2. A challenger accepts with an opposing case and matching stake.
3. Evidence and arguments are attached to the record.
4. GenLayer reads and reasons over the dispute.
5. The contract opens challenge and appeal windows.
6. The final settlement pays or archives the duel.
7. Reputation updates are kept alongside the audit trail.

The frontend preserves a clean face-off arena UX (inspired by Doodles NFT aesthetics), while the contract handles the lifecycle state, challenge/appeal logic, reputation, indexed reads, and legacy compatibility wrappers.

## Contract Architecture
| Area | Detail |
| --- | --- |
| **Contract** | `contracts/genduel.py` |
| **Network** | GenLayer Studionet |
| **Write methods** | 20 |
| **Read methods** | 20 |
| **GenLayer features** | `gl.nondet.web.render`, `gl.nondet.exec_prompt`, `gl.eq_principle.prompt_comparative` |
| **Storage model** | duel records, case records, evidence, challenge records, appeal records, reputation, audit events |
| **Legacy UI support**| `open_duel`, `accept_duel`, `rule`, `get_duel`, `get_duel_count`, `get_argument` |

### Core lifecycle:
```text
draft_duel
  -> add_case_for / add_case_against
  -> add_evidence
  -> open_deliberation
  -> judge_with_genlayer
  -> open_challenge_window
  -> submit_challenge
  -> resolve_challenge_with_genlayer
  -> submit_appeal
  -> resolve_appeal_with_genlayer
  -> settle
  -> archive_duel
```

### Useful reads:
- `get_duel_count`
- `get_duel`
- `get_duel_record`
- `get_argument_count`
- `get_recent_duels`
- `get_duels_by_status`

## Verification Trail
The deployed contract was successfully deployed and smoke-tested on the GenLayer Studionet.
- **Contract Address:** `0xeC412B00bc5E5999cb3D7EDD6cE1BB354B59C598`
- **Frontend Integrated:** Yes, via `genlayer-lite.js`.
- **Test Result:** All smoke writes and read assertions passed.

## Frontend
GenDuel ships as a static WebGL-styled face-off interface:
- Split FOR / AGAINST composition
- Three.js clash arena
- Doodles NFT-inspired aesthetic (pastel colors, rounded corners, thick outlines)
- Live wallet connection through the bundled browser client
- On-chain read flow through GenLayer JS
- Standalone Vercel bundle with local `shared/` client files

## Run Locally
From this repository folder:

```bash
python -m http.server 3000
```
Open: `http://localhost:3000/`

## Deploy
```bash
vercel --prod --yes
```

## Repository Safety
This public repository intentionally excludes local secrets:
- no private keys
- no vault files
- no `.env` files
- no `.vercel` project state
- no local dashboard data

Public files include only frontend code, contract source, deployment metadata, tests, and non-sensitive proof links.
