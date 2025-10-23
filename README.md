## Foundry

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

https://book.getfoundry.sh/

## Usage

### Build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

### Setup (dependencies)

If you prefer to keep the repository lean, `forge-std` is managed by Foundry and can be installed on each developer machine or CI instead of vendoring the library. Run once to install into `lib/`:

```shell
forge install foundry-rs/forge-std
```

If you've previously committed `lib/forge-std` and want to stop tracking it in git (keep the local copy but remove it from the repo), run:

```shell
git rm -r --cached lib/forge-std
echo "lib/forge-std/" >> .gitignore
git add .gitignore
git commit -m "Stop vendoring forge-std; use forge install instead"
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
