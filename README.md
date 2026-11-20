# wallet-ai-bitcoin
Self-hosted Bitcoin wallet infrastructure for developers and AI agents. Built with Go, featuring SegWit, Taproot, JSON APIs, and cURL integration.


# WALLET AI BITCOIN

### Your Bitcoin Wallet. Your Keys. Your Engine.

**Self-hosted Bitcoin infrastructure for developers, applications, and AI agents.**

WALLET AI BITCOIN (WAB) is a Bitcoin software ecosystem focused on wallet sovereignty, programmable infrastructure, and straightforward integration through HTTP, JSON, and cURL.

**Bitcoin Mainnet & Testnet · Go · SegWit · Taproot · REST API · cURL**

## Official links

| Resource | Link |
| --- | --- |
| Personal website | [THAMER.ORG](https://thamer.org/) |
| Bitcoin Engine | [Engine and installation](https://thamer.org/engine) |
| API documentation | [API and cURL reference](https://thamer.org/api) |
| Software releases | [Repository and downloads](https://thamer.org/repo/) |
| GitHub | [@thamerorg](https://github.com/thamerorg) |
| X | [@thamer_org](https://x.com/thamer_org) |

## Overview

WAB separates **wallet creation** from **wallet execution**:

- **Factory:** Independently creates wallet identity and recovery credentials and issues the signed fee law at wallet birth.
- **Bitcoin Engine:** Restores existing wallets and provides authorized wallet operations through a local HTTP API.
- **Developer tools and AI agents:** External clients that integrate with the Engine. Agent-specific spending permissions and limits belong in the client/tool layer, not in the Bitcoin Engine's fee-law implementation.

The architecture is designed for self-hosted operation. It is not a hosted custody service.

## Capabilities

- Bitcoin Mainnet and Testnet support
- Native SegWit (BIP84) and Taproot (BIP86) wallet addresses
- JSON-based HTTP API with cURL examples
- Wallet receive, balance, UTXO, send, and transaction-status operations
- Wallet recovery and restoration workflows
- Per-wallet signed fee law issued at creation and verified by the Engine
- Integration points for CLI tools, payment applications, and AI agents

## Installation

See the [official Engine documentation](https://thamer.org/engine) for supported platforms, dependencies, installation steps, and release status.

> **Release status:** Do not run an unverified remote installation script. Use the installation command published with a verified release on the official Engine page.

The Engine requires access to Bitcoin Core and the Bitcoin network for normal operation.

## API and cURL

The Engine is designed around HTTP requests and JSON responses. The following examples show the intended local API interface; check the [current API reference](https://thamer.org/api) for the exact request schema and authentication requirements of your installed version.

### Local endpoint

```bash
export BASE_URL="http://127.0.0.1:7070"
```

### Health

```bash
curl -sS "$BASE_URL/api/v5/btc/health" | jq .
```

### Receive — Testnet SegWit

```bash
export BTC_KEY="YOUR_BTC_KEY"

curl -sS -X POST "$BASE_URL/api/v5/btc/wallet/receive" \
  -H "X-BTC-KEY: $BTC_KEY" \
  -H "Content-Type: application/json" \
  -d '{"net":"test","type":"segwit"}' | jq .
```

### Balance — Testnet SegWit

```bash
curl -sS -X POST "$BASE_URL/api/v5/btc/wallet/balance" \
  -H "X-BTC-KEY: $BTC_KEY" \
  -H "Content-Type: application/json" \
  -d '{"net":"test","type":"segwit"}' | jq .
```

For UTXOs, SEND, transaction status, Taproot, and recovery operations, consult the [API documentation](https://thamer.org/api). Never execute a real-money SEND request without reviewing the destination, amount, network, and fee policy.

## Security and wallet sovereignty

- Keep **BTC KEY** and **BTC SECRET** private. Never commit real credentials to a public repository.
- Restrict access to authenticated Engine endpoints; do not expose a local wallet API directly to the public Internet.
- Wallet removal from the Engine's local database does **not** destroy the sovereign wallet or erase on-chain history.
- Each wallet's signed fee law is fixed at creation. The Engine verifies and executes that wallet's law rather than issuing a replacement.
- Wallet sends are subject to the signed **10% inclusive software usage fee** policy, including the Bitcoin miner fee within that budget. Read the [fee terms](https://thamer.org/tos#fee) before using the software.

## For developers and AI agents

WAB's API-first approach supports integration from scripts, Go services, automation systems, and AI clients. Keep wallet credentials and transaction authorization under the wallet owner's control. Treat external agents as clients with explicitly granted permissions, not as independent custodians.

Potential integrations include Bitcoin CLI tools, payment interfaces, donation applications, and transaction monitoring services. Availability varies by product and release; consult the official links above.

## Documentation and releases

- **Website and articles:** https://thamer.org/
- **Engine and installation:** https://thamer.org/engine
- **API and cURL examples:** https://thamer.org/api
- **Software repository:** https://thamer.org/repo/

---

**WALLET AI BITCOIN — Your Bitcoin Wallet. Your Keys. Your Engine.**

Developed by [THAMER](https://thamer.org/).
