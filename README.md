# Mobazha

**Independent commerce, connected on your terms.**

Most online marketplaces bundle the storefront, discovery, checkout, data, and customer
relationship inside one operator. Mobazha separates them. A seller can own the store and its
commercial history while choosing which markets, services, and interfaces to connect.

The open-source Mobazha Node can publish products, receive and fulfill orders, verify supported
payments, communicate with buyers, and preserve transaction history on a backend chosen by the
operator. Other stores, marketplaces, apps, and Agents can connect through shared interfaces while
each seller's backend remains authoritative for its own business state.

[Try Mobazha](https://app.mobazha.org/) ·
[Explore the product](https://docs.mobazha.org/project/product-map) ·
[Run your own store](https://docs.mobazha.org/self-host/install) ·
[Read the whitepaper](https://docs.mobazha.org/project/whitepaper) ·
[Documentation](https://docs.mobazha.org/)

> **Current status:** `v0.3.0-rc.1` is the public release target. Use testnet while evaluating the
> current source; stable signed binaries have not yet been published.

[![Direct peer-to-peer and hybrid Mobazha store networks](https://docs.mobazha.org/images/docs/project/store-network-topologies.svg)](https://docs.mobazha.org/project/architecture)

_Stores can operate independently, use selected hosted services, or participate in a hybrid network
without moving every order into one central database._

## Why Mobazha

- **Own the commercial relationship.** Keep control of your store identity, catalog, policies,
  orders, customer interactions, and operational data.
- **Use one commerce core across many channels.** Present the same store through its own storefront,
  shared markets, direct links, embedded experiences, or Agent-assisted workflows.
- **Choose what to operate yourself.** Run the complete open-source Node, use a compatible hosted
  service, or combine your own backend with selected external services.
- **Make important actions accountable.** Orders, payment observations, fulfillment, recovery, and
  disputes are recorded by the backend that owns the transaction—not inferred from a page or
  notification.

## One product, two core repositories

This repository contains **Mobazha Node**, the commerce engine and source of truth for store and
transaction state. It provides the data, policies, APIs, messaging, payment verification, and
operator controls needed to run a store.

[Mobazha Unified](https://github.com/mobazha/mobazha-unified) is the shared buyer and seller
experience. It turns the capabilities of a connected Node or hosted backend into storefront,
checkout, order, marketplace, and administration journeys.

Together they support three operating paths:

- **Hosted:** start quickly while a service operator runs the backend under published terms.
- **Self-hosted:** run the Node on infrastructure you control and own its security, backup, and
  availability.
- **Hybrid:** keep the store backend independent while opting into selected discovery, payment,
  delivery, messaging, AI, or other services.

[Compare the operating paths](https://docs.mobazha.org/start/choose-deployment).

## Try Mobazha

The fastest way to see the buyer and seller experience is
[app.mobazha.org](https://app.mobazha.org/).

To evaluate an independent Node from source:

```bash
git clone https://github.com/mobazha/mobazha.git
cd mobazha
go build -tags goolm -o mobazha .
./mobazha init --testnet
./mobazha start --testnet --open
```

The embedded Web UI and API listen on `http://127.0.0.1:5102` by default. The current Community
release enables BTC, BCH, and LTC by default, subject to store configuration and runtime readiness.
See the [release scope](https://docs.mobazha.org/project/release-scope) before relying on any specific
capability.

## Supported payment networks

The Node's multi-chain payment layer covers UTXO chains (Bitcoin, Bitcoin Cash, Litecoin, Zcash) and
EVM networks, including **BNB Smart Chain** (BNB Chain, chain ID 56). On BNB Smart Chain the Node
handles native **BNB** together with BEP-20 stablecoins — USDT
(`0x55d398326f99059fF775485246999027B3197955`), USDC
(`0x8AC76a51cc950d9822D68b83fE1Ad97B32Cd580d`), and BUSD
(`0xe9e7CEA3DedcA5984780Bafc599bD69ADd087D56`).

Chain definitions live in [`pkg/wallet-interface/cointype.go`](./pkg/wallet-interface/cointype.go),
asset metadata in [`pkg/assetid/registry.go`](./pkg/assetid/registry.go), and per-chain RPC defaults
in [`internal/chains/config.go`](./internal/chains/config.go) — where BSC is configured against
`bsc-dataseed.binance.org` for mainnet and `data-seed-prebsc-2-s2.binance.org` for testnet.

Escrow on BNB Smart Chain and other EVM networks uses canonical
[Safe](https://github.com/safe-global/safe-deployments) v1.4.1 multisig contracts: each order gets a
dedicated 2-of-3 Safe (buyer, seller, moderator) deployed deterministically through the official
`SafeProxyFactory`. Mobazha deploys no bespoke escrow contract of its own.

Which networks a given store actually accepts depends on its configuration and on the capabilities
advertised by the backend serving it.

## Go deeper

- [How Mobazha fits together](https://docs.mobazha.org/project/product-map)
- [System and store-network architecture](https://docs.mobazha.org/project/architecture)
- [Buy from an independent store](https://docs.mobazha.org/buy)
- [Start and operate a store](https://docs.mobazha.org/sell)
- [Build with the API, webhooks, and MCP](https://docs.mobazha.org/build)
- [Fees](https://docs.mobazha.org/project/fees),
  [compatibility](https://docs.mobazha.org/project/compatibility), and
  [packaging](https://docs.mobazha.org/project/distribution)
- [Roadmap and current release scope](https://docs.mobazha.org/project/roadmap)

## Contributing and security

Contributions are welcome. Start with [CONTRIBUTING.md](./CONTRIBUTING.md); implementation and
release evidence lives in the repository's [`docs`](./docs/) directory. Run `make test`
before submitting Go changes.

Report security issues privately as described in [SECURITY.md](./SECURITY.md).

## License and attribution

Mobazha-authored source is licensed under the [Mozilla Public License 2.0](./LICENSE). Portions
derived from OpenBazaar remain available under the
[OpenBazaar MIT License](./LICENSES/MIT-OpenBazaar.txt). See [NOTICE](./NOTICE) and
[Attribution and source identity](./docs/project/ATTRIBUTION.md) for details.

Originally developed by [fengzie](https://github.com/fengzie) and maintained by the Mobazha
contributors. The canonical source repository is
[mobazha/mobazha](https://github.com/mobazha/mobazha).
