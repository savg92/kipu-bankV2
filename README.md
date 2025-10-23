# 🏦 KipuBank V2

> Production-grade multi-token vault with Chainlink price oracles and role-based access control

## Overview

**KipuBank V2** is an advanced decentralized vault that supports ETH and ERC-20 token deposits with USD-denominated bank caps enforced via Chainlink price oracles. This project showcases professional Solidity development practices and advanced DeFi patterns.

### Key Features

- **Multi-Token Support**: Deposit and withdraw ETH and whitelisted ERC-20 tokens
- **Chainlink Oracle Integration**: Real-time ETH/USD price feeds for accurate valuation
- **USD-Denominated Accounting**: Bank cap enforced in USD across all supported assets
- **Role-Based Access Control**: Owner-managed token whitelist and emergency controls
- **Decimal Normalization**: Automatic handling of 6, 8, and 18 decimal tokens
- **Advanced Security**: ReentrancyGuard, SafeERC20, CEI pattern, comprehensive error handling
- **Gas Optimizations**: Storage caching, unchecked arithmetic, immutable variables

## Technology Stack

- **Language**: Solidity ^0.8.24
- **Framework**: Foundry
- **Dependencies**: OpenZeppelin Contracts, Chainlink Contracts
- **Network**: Sepolia Testnet

## Development Status

🚧 **In Development** - Phase 2: Contract Architecture

See [plan.md](./plan.md) for detailed development roadmap.

## Usage

### Build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

### Format

```shell
$ forge fmt
```

### Gas Snapshots

```shell
$ forge snapshot
```

### Anvil

```shell
$ anvil
```

### Deploy

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
$ cast <subcommand>
```

### Help

```shell
$ forge --help
$ anvil --help
$ cast --help
```
