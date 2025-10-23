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

## Deployment

✅ **Deployed to Sepolia Testnet**

- **Contract Address**: [`0xe1b858d11bbbd3565a883a83352521765645b19f`](https://sepolia.etherscan.io/address/0xe1b858d11bbbd3565a883a83352521765645b19f)
- **Network**: Sepolia (Chain ID: 11155111)
- **Deployment Transaction**: [`0xc172a48c046535f51c3e92698e0e4024c53b20c998f9206b239935372dc5d38c`](https://sepolia.etherscan.io/tx/0xc172a48c046535f51c3e92698e0e4024c53b20c998f9206b239935372dc5d38c)
- **Verification**: ✅ Verified on Etherscan
- **Bank Cap**: 100,000 USDC (USD-denominated)
- **Max Withdrawal**: 1 ETH per transaction
- **Chainlink Price Feed**: ETH/USD on Sepolia

### Interact with Contract

Visit the [Etherscan page](https://sepolia.etherscan.io/address/0xe1b858d11bbbd3565a883a83352521765645b19f#writeContract) to interact with the contract:

1. **Read Contract**: View bank cap, total deposits, your balance, and more
2. **Write Contract**: Deposit ETH, withdraw funds, check balances (requires Sepolia ETH)

## Development Status

✅ **Phase 4 Complete** - Deployed and Verified on Sepolia

See [STATUS.md](./STATUS.md) for current project state and [plan.md](./plan.md) for detailed roadmap.

## Quick Start - Using the Deployed Contract

### Deposit ETH

```bash
# Deposit 0.1 ETH (via cast)
cast send 0xe1b858d11bbbd3565a883a83352521765645b19f \
  "deposit(address,uint256)" \
  "0x0000000000000000000000000000000000000000" \
  "100000000000000000" \
  --value 0.1ether \
  --rpc-url sepolia \
  --private-key $PRIVATE_KEY
```

Or use **Etherscan's Write Contract** interface (easier):

1. Visit the [Write Contract tab](https://sepolia.etherscan.io/address/0xe1b858d11bbbd3565a883a83352521765645b19f#writeContract)
2. Connect your wallet
3. Call `deposit` with:
   - `token`: `0x0000000000000000000000000000000000000000` (ETH)
   - `amount`: Same as ETH sent (in wei)
   - `payableAmount`: Amount to deposit (e.g., 0.1 ETH)

### Check Your Balance

```bash
# Check balance (replace YOUR_ADDRESS)
cast call 0xe1b858d11bbbd3565a883a83352521765645b19f \
  "getVaultBalance(address,address)(uint256)" \
  "YOUR_ADDRESS" \
  "0x0000000000000000000000000000000000000000" \
  --rpc-url sepolia
```

### Withdraw ETH

```bash
# Withdraw 0.05 ETH
cast send 0xe1b858d11bbbd3565a883a83352521765645b19f \
  "withdraw(address,uint256)" \
  "0x0000000000000000000000000000000000000000" \
  "50000000000000000" \
  --rpc-url sepolia \
  --private-key $PRIVATE_KEY
```

## Development

### Build

```shell
forge build
```

### Test

```shell
forge test -vv
```

### Test with Gas Report

```shell
forge test --gas-report
```

### Deploy to Sepolia

```shell
forge script script/DeployKipuBankV2.s.sol --rpc-url sepolia --broadcast --verify
```

### Format

```shell
forge fmt
```

### Gas Snapshots

```shell
forge snapshot
```

### Local Testing with Anvil

```shell
anvil
```

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
