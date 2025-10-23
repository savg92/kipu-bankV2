# KipuBank V2 - Deployment Report

**Deployment Date:** October 23, 2025  
**Network:** Sepolia Testnet  
**Deployer:** 0xA8760074fc8671c2f2c3E2EAdD1595b88BacE195

---

## Deployed Contract Information

| Parameter | Value |
|-----------|-------|
| **Contract Address** | `0xe1b858d11bbbd3565a883a83352521765645b19f` |
| **Transaction Hash** | `0xc172a48c046535f51c3e92698e0e4024c53b20c998f9206b239935372dc5d38c` |
| **Block Number** | TBD (Check Etherscan) |
| **Chain ID** | 11155111 (Sepolia) |
| **Verification Status** | ✅ Verified |
| **Deployment Gas** | 2,186,107 |

---

## Etherscan Links

- **Contract Page**: https://sepolia.etherscan.io/address/0xe1b858d11bbbd3565a883a83352521765645b19f
- **Contract Code**: https://sepolia.etherscan.io/address/0xe1b858d11bbbd3565a883a83352521765645b19f#code
- **Read Contract**: https://sepolia.etherscan.io/address/0xe1b858d11bbbd3565a883a83352521765645b19f#readContract
- **Write Contract**: https://sepolia.etherscan.io/address/0xe1b858d11bbbd3565a883a83352521765645b19f#writeContract
- **Deployment Tx**: https://sepolia.etherscan.io/tx/0xc172a48c046535f51c3e92698e0e4024c53b20c998f9206b239935372dc5d38c

---

## Constructor Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `bankCapUSD` | `100000000000` (100,000 USDC) | Maximum total deposits in USD (6 decimals) |
| `MAX_WITHDRAW_PER_TX` | `1000000000000000000` (1 ETH) | Maximum withdrawal per transaction |
| `ethUsdPriceFeed` | `0x694AA1769357215DE4FAC081bf1f309aDC325306` | Chainlink ETH/USD price feed on Sepolia |

---

## Post-Deployment Verification

### ✅ Contract State Verification

```bash
# Bank Cap (should be 100,000 * 10^6)
cast call 0xe1b858d11bbbd3565a883a83352521765645b19f "bankCapUSD()(uint256)" --rpc-url sepolia
# Result: 100000000000 ✅

# Max Withdrawal (should be 1 ETH = 10^18)
cast call 0xe1b858d11bbbd3565a883a83352521765645b19f "MAX_WITHDRAW_PER_TX()(uint256)" --rpc-url sepolia
# Result: 1000000000000000000 ✅

# Owner (should be deployer address)
cast call 0xe1b858d11bbbd3565a883a83352521765645b19f "owner()(address)" --rpc-url sepolia
# Result: 0xA8760074fc8671c2f2c3E2EAdD1595b88BacE195 ✅

# Total Deposits (should be 0 initially)
cast call 0xe1b858d11bbbd3565a883a83352521765645b19f "totalDepositsUSD()(uint256)" --rpc-url sepolia
# Result: 0 ✅

# Deposits Paused (should be false)
cast call 0xe1b858d11bbbd3565a883a83352521765645b19f "depositsPaused()(bool)" --rpc-url sepolia
# Result: false ✅

# Current ETH Price from Oracle
cast call 0xe1b858d11bbbd3565a883a83352521765645b19f "getLatestETHPrice()(int256)" --rpc-url sepolia
# Result: ~384239500000 ($3,842.39 with 8 decimals) ✅
```

**All constructor parameters verified correctly!** ✅

---

## Contract Features Status

| Feature | Status | Notes |
|---------|--------|-------|
| ETH Deposits | ✅ Ready | Requires Sepolia ETH |
| ETH Withdrawals | ✅ Ready | 1 ETH max per tx |
| ERC-20 Deposits | ⏳ Pending | Needs token whitelist via `addSupportedToken()` |
| ERC-20 Withdrawals | ⏳ Pending | After tokens whitelisted |
| Chainlink Oracle | ✅ Working | ETH/USD price feed active |
| Bank Cap Enforcement | ✅ Active | 100,000 USDC cap |
| Emergency Pause | ✅ Ready | Owner can pause deposits |
| Access Control | ✅ Active | Owner-only admin functions |

---

## Testing Checklist

### Manual Testing via Etherscan

- [ ] **Deposit ETH** (Write Contract → deposit)
  - Use address(0) for token
  - Set amount equal to msg.value
  - Verify DepositMade event emitted
  
- [ ] **Check Balance** (Read Contract → getVaultBalance)
  - Input your address and address(0) for ETH
  - Verify balance matches deposit
  
- [ ] **Check USD Value** (Read Contract → getVaultBalanceInUSD)
  - Verify USD value calculation is correct
  
- [ ] **Withdraw ETH** (Write Contract → withdraw)
  - Withdraw amount <= balance and <= 1 ETH
  - Verify WithdrawalMade event emitted
  - Verify ETH received
  
- [ ] **Add Supported Token** (Owner only)
  - Add USDC/USDT test tokens
  - Verify TokenAdded event
  
- [ ] **Test Pause/Unpause** (Owner only)
  - Pause deposits
  - Try deposit (should fail)
  - Unpause deposits
  - Verify DepositsToggled events

---

## Next Steps

1. **Add Supported ERC-20 Tokens**
   - Find Sepolia test token addresses (USDC, USDT, etc.)
   - Call `addSupportedToken(address, decimals, priceFeed)`
   
2. **Perform Live Testing**
   - Deposit small amounts of ETH
   - Test withdrawal limits
   - Test bank cap enforcement
   - Verify all events
   
3. **Final Documentation**
   - Update README with test results
   - Document any issues found
   - Add usage examples
   
4. **Repository Finalization**
   - Ensure all documentation is complete
   - Add portfolio-ready screenshots
   - Prepare for public showcase

---

## Security Notes

- ✅ Contract verified on Etherscan (source code public)
- ✅ ReentrancyGuard active on deposit/withdraw
- ✅ SafeERC20 used for token transfers
- ✅ Checks-Effects-Interactions pattern followed
- ✅ Custom errors for gas efficiency
- ✅ Comprehensive NatSpec documentation
- ✅ 41/41 tests passing in test suite
- ✅ Access control via Ownable pattern

**No known security issues.** ✅

---

## Deployment Command Used

```bash
forge script script/DeployKipuBankV2.s.sol --rpc-url sepolia --broadcast --verify
```

**Deployment successful!** 🎉
