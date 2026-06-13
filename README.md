# BRVBTC 

<p align="center">
  <img src="brvbtc.png" alt="BRVBTC" width="150"/>
</p>

<p align="center">
  <strong>🇻🇪 Bolivar Republica Venezuela BTC (BRVBTC)</strong><br>
  <em>A Revolutionary Stable Token Pegged to BTC with 50% On-Chain Reserve</em>
</p>

<p align="center">
  BRVBTC is not just another stablecoin. It's a hybrid between a stable asset and a Bitcoin-backed reserve token, designed to offer stability, transparency, and decentralization — all powered by real WBTC and immutable smart contracts.
</p>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Solidity](https://img.shields.io/badge/Solidity-^0.8.27-blue)](https://soliditylang.org/)
[![Foundry](https://img.shields.io/badge/Built%20with-Foundry-FFDB1C)](https://book.getfoundry.sh/)
[![Security: No vulnerabilities](https://img.shields.io/badge/Security-No%20vulnerabilities-brightgreen)](https://github.com/josat123/BRVBTC/security)
[![Contract Verified](https://img.shields.io/badge/Contract-Verified-success)](https://polygonscan.com/address/0xa5c96d77C280B9F4bA13cd4064C4864Cf69a3BCB#code)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Ethereum](https://img.shields.io/badge/Ethereum-3C3C3D?style=flat&logo=ethereum&logoColor=white)](https://ethereum.org)
[![Polygon](https://img.shields.io/badge/Polygon-8247E5?style=flat&logo=polygon&logoColor=white)](https://polygon.technology)
[![Ethereum Contract](https://img.shields.io/badge/ETH%20Contract-0x9bc0F4...-blue)](https://etherscan.io/address/0x9bc0F4d4B31AdEa0c7Fde6f40a778E4Ce7Bc652d)
[![Polygon Contract](https://img.shields.io/badge/Polygon%20Contract-0xa5c96d...-purple)](https://polygonscan.com/address/0xa5c96d77C280B9F4bA13cd4064C4864Cf69a3BCB)
[![Bridge L1](https://img.shields.io/badge/Bridge%20L1-0xe8681d...-green)](https://etherscan.io/address/0xe8681d55585FcDA6a4a39c9a59f39b63fbBa88e8)
[![Bridge L2](https://img.shields.io/badge/Bridge%20L2-0x0Ef6a6...-orange)](https://polygonscan.com/address/0x0Ef6a63a16fB21dD8398183a154596953Ce4E835)
[![Uniswap V4](https://img.shields.io/badge/Uniswap%20V4-Pool-ff69b4)](https://polygonscan.com/address/0x67366782805870060151383f4bbff9dab53e5cd6)
[![Website](https://img.shields.io/badge/Website-bolivarrepublicavenezuelabtc.com-blue?style=flat&logo=google-chrome&logoColor=white)](https://bolivarrepublicavenezuelabtc.com)

## 📌 Overview

| Feature | Value |
|--------|-------|
| **Token Name** | Bolivar Republica Venezuela BTC |
| **Symbol** | BRVBTC |
| **Blockchain** | Ethereum (L1) & Polygon (L2) |
| **Standard** | ERC20, ERC20Permit, ERC20Burnable |
| **Max Supply** | 21,000,000 BRVBTC |
| **Reserve Ratio** | 50% (backed by WBTC) |
| **Peg** | 1 BRVBTC = 1 USD (by construction) |
| **Initial Liquidity (L2)** | $100 (BRVBTC / WBTC pool on Uniswap V4) |
| **Bridge** | UniversalBridge (L1 ↔ L2, same token on both chains) |

---

## 🧠 The Idea Behind BRVBTC

BRVBTC was born from a simple but powerful idea:

> *"What if you could have a stable token, fully transparent, backed by Bitcoin, and available natively on multiple chains — without wrapped versions or centralized control?"*

We designed BRVBTC to be:

- ✅ **Stable by math** – 1 BRVBTC = 1 USD, guaranteed by the ratio `TOKEN_PER_WBTC = 100,000`
- ✅ **Backed by real BTC** – 50% of the total supply is backed by WBTC held in the contract
- ✅ **Mintable by anyone** – Send WBTC, mint BRVBTC
- ✅ **Burnable anytime** – Burn BRVBTC, get back WBTC (as long as reserve allows)
- ✅ **Cross-chain native** – Same token on Ethereum and Polygon via a custom-built bridge
- ✅ **Decentralized** – No central control, immutable rules, public verification

---

## 🔢 The Math That Makes It Work

### 1. The Peg: 1 BRVBTC = 1 USD

```solidity
uint256 public constant TOKEN_PER_WBTC = 100_000 * 10**18;
If 1 WBTC = 100,000 USD, then:

100,000 BRVBTC = 1 WBTC = 100,000 USD

1 BRVBTC = 1 USD

This is not a promise. It's mathematics encoded in the contract.

2. The 50% Reserve Ratio
solidity
uint256 public constant RESERVE_RATIO = 50; // 50%
At any time:

text
totalReserve * TOKEN_PER_WBTC * 100 / totalSupply() >= 50
This ensures that at least 50% of the token's value is backed by WBTC in the contract.

3. Minting & Burning
Mint:

solidity
mint(uint256 wbtcAmount)
User sends wbtcAmount of WBTC to the contract

Contract mints wbtcAmount * TOKEN_PER_WBTC / 10**8 BRVBTC

Reserve and supply increase, ratio is maintained

Burn:

solidity
burnToWBTC(uint256 tokenAmount)
User burns tokenAmount BRVBTC

Contract sends back equivalent WBTC (if reserve allows)

Reserve and supply decrease, ratio is maintained

# 🌉 UniversalBridge – Cross-Chain BRVBTC

BRVBTC exists natively on Ethereum (L1), Base (L2), and Polygon (L2) — not as wrapped tokens, but as the same token on each chain, thanks to our `UniversalBridge` contract adapted to each chain's native cross-chain messenger.

## 📌 Deployed Bridge Contracts

| Chain | BRVBTC Address | Bridge Address | Messenger / Adapter |
|-------|----------------|----------------|----------------------|
| **Ethereum (L1)** | `0x9bc0F4d4B31AdEa0c7Fde6f40a778E4Ce7Bc652d` | `0x95EEf9bCb0bAC8742CfBb0592cBEd367b90cB07d` | `0x25ace71c97b33cC4724cf772e9b8B8F980f9d3B5` (L1CrossDomainMessenger) |
| **Base (L2)** | `0x0Ef6a63a16fB21dD8398183a154596953Ce4E835` | `0x1fB0948080E16e55c63277c43B9B45be39a5fc5F` | `0x4200000000000000000000000000000000000007` (L2CrossDomainMessenger) |
| **Arbitrum (L2)** | `0x71585d90E726b82c3C435212995Fe49ADef98343` | `inbox : 0x4Dbd4fc535Ac27206064B68FfCf827b0A60BAB3f` | `outbox : x0B9857ae2D4A3DBe74ffE1d7DF045bb7F96E4840` (FxChild) |
| **Bsc (L2)** | `0x0Ef6a63a16fB21dD8398183a154596953Ce4E835` | `commingsoon` | `commingsoon`  |
| **Avax (L2)** | `0x0ef6a63a16fb21dd8398183a154596953ce4e835` | `commingsoon` | `commingsoon`  |
| **Polygon (L2)** | `0xa5c96d77C280B9F4bA13cd4064C4864Cf69a3BCB` | `commingsoon` | `commingsoon`  |
| **Unchain (L2)** | `0x2c8E3dd1d7Cdf1636d8C69c2af51c9653E562DAb` | `commingsoon` | `commingsoon`  |



## 🔄 Supported Flows

| Direction | Supported | Notes |
|-----------|------------|-------|
| Ethereum → Base | ✅ Yes | Bidirectional (lock & mint, burn & release). |
| Base → Ethereum | ✅ Yes | Bidirectional. |
| Polygon → Ethereum | ✅ Yes | Withdraw only (burn on Polygon, release on Ethereum). |
| Ethereum → Polygon | ❌ No | Due to the 1:1 token mapping on L1 (same L1 token cannot map to two different remote tokens). To enable this, either a separate L1 wrapper token or a contract upgrade is needed. |
Other Chain:
| Bsc is comminsoon
| Avax is commingsoon
| Unchain is commingsoon
| Or used : layerzero.network - Bridge recommended.

## 🧠 Architecture & Adaptations

`UniversalBridge` was originally designed to work with the **CrossDomainMessenger** of OP Stack chains (Optimism, Base, Mode). To integrate it with **Polygon (PoS)**, we adapted the contract to use the **FxPortal**:

- On L1, the messenger is `FxRoot` (`0xfe5e5D361b2ad62c541bAb87C45a0B9B018389a2`).
- On L2, the messenger is `FxChild` (`0x8397259c983751DAf40400790063935a11afa28a`).

Polygon support is **one-way (L2 → L1)** because the current contract uses a 1:1 mapping for remote tokens on L1. Full bidirectional support would require a separate L1 token or an upgraded contract with multi‑chain mapping.

## ⚙️ How the Bridge Works

1. **Deposit from L1 to L2 (e.g., Ethereum → Base)**  
   - User approves `grossAmount` (including any tax).  
   - Bridge **locks** tokens on L1 and sends a cross‑chain message.  
   - On L2, bridge **mints** the equivalent amount to the recipient.

2. **Withdraw from L2 to L1 (e.g., Base → Ethereum)**  
   - User calls `withdrawToL1`.  
   - Bridge **burns** tokens on L2 and sends a message to L1.  
   - On L1, bridge **releases** the previously locked tokens to the recipient.

3. **Security**  
   - `onlyMessenger` and `onlyRemoteBridge` modifiers ensure only the authenticated messenger can finalize messages.  
   - Unique nonces (`depositNonce` / `withdrawNonce`) and message hashes prevent replay attacks.  
   - `processedMessages` mapping prevents double finalization.

4. **Fees**  
   - Optional, configurable by owner (max 0.3%). Current fee: **0.05%** on all chains.  
   - Fees are paid in the deposited token and sent to `feeCollector`.

## 🧪 Testing & Verification

All contracts are verified on:

- **Ethereum**: [Etherscan](https://etherscan.io/address/0x95EEf9bCb0bAC8742CfBb0592cBEd367b90cB07d)
- **Base**: [BaseScan](https://basescan.org/address/0x1fB0948080E16e55c63277c43B9B45be39a5fc5F)
- **Polygon**: [PolygonScan](https://polygonscan.com/address/0x31C9F16e4Fee8C097a700Ea6a1010bC8807D27Fe)

## 📝 Known Limitations

- **Polygon one‑way only** – As detailed above, the bridge on Polygon only supports withdrawals to Ethereum. For deposits from Ethereum to Polygon, use an alternative bridge or wait for a contract upgrade.
- **Gas limits** – `MIN_GAS_LIMIT` = 200,000, `MAX_GAS_LIMIT` = 5,000,000. Ensure the gas provided is sufficient for finalization.
- **Fee‑on‑transfer tokens** – These are not supported if registered as `taxed = true` (the contract reverts). Use `taxed = false` for such tokens.

## 🔄 Supported Flows
Direction	Supported	Notes
Ethereum → Base	✅ Yes	Bidirectional (lock & mint, burn & release).
Base → Ethereum	✅ Yes	Bidirectional.
Polygon → Ethereum	❌ No (broken)	Withdrawals on Polygon are currently non‑operational due to a contract state lock (ReentrancyGuard stuck). Use Base for all L2 → L1 withdrawals.
Ethereum → Polygon	❌ No	Due to the 1:1 token mapping on L1 (same L1 token cannot map to two different remote tokens). To enable this, either a separate L1 wrapper token or a contract upgrade is needed.


## 🔮 Future Development

- Full bidirectional support for Polygon (via a separate L1 wrapper token or contract mapping upgrade).  
- Integration with Arbitrum (using Arbitrum's native bridge, which requires an adaptation similar to Polygon).  
- Emergency pause mechanism (already present in `setPaused`).
---
A **BRVBTC / WBTC** pool has been initialized on **Uniswap V4**:

- **Pool Address:** `0x360E68faCcca8cA495c1B759Fd9EEe466db9FB32`
- **Currency0 (WBTC):** `0x2f2a2543B76A4166549F7aaB2e75Bef0aefC5B0f`
- **Currency1 (BRVBTC):** `0x71585d90E726b82c3C435212995Fe49ADef98343`
- **Initial Liquidity:** $88.47 (enables trading and price discovery)
- **Price:** Automatically stabilized at ~1 USD thanks to the mint/burn mechanism

### On Polygon (L2)

A **BRVBTC / WBTC** pool has been initialized on **Uniswap V4**:

- **Pool Address:** `0x67366782805870060151383f4bbff9dab53e5cd6`
- **Currency0 (WBTC):** `0x1BFD67037B42Cf73acF2047067bd4F2C47D9BfD6`
- **Currency1 (BRVBTC):** `0xa5c96d77C280B9F4bA13cd4064C4864Cf69a3BCB`
- **Initial Liquidity:** $100 (enables trading and price discovery)
- **Price:** Automatically stabilized at ~1 USD thanks to the mint/burn mechanism

### On Ethereum (L1)

A **BRVBTC / WBTC** pool is also available on **Uniswap V4** on Ethereum Mainnet:

- **Pool Address:** `0x000000000004444c5dc75cB358380D2e3dE08A90`
- **Currency0 (WBTC):** `0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599`
- **Currency1 (BRVBTC):** `0x9bc0F4d4B31AdEa0c7Fde6f40a778E4Ce7Bc652d`
- **Initial Liquidity:** $105 (enables trading and price discovery)
- **Price:** Automatically stabilized at ~1 USD thanks to the mint/burn mechanism

> ⚠️ **Note:** The L1 pool uses **native WBTC** (`0x2260FAC5...`), while the L2 pool uses **posWBTC** (`0x1BFD6703...`). Both represent the same underlying Bitcoin value.

🔐 Security & Transparency
Auditable by Design
Every aspect of BRVBTC is publicly verifiable:

Aspect	How to Verify
Reserve	Call totalReserve() and totalSupply() on Etherscan
Mint/Burn	View Minted and Burned events
Bridge	Check DepositInitiated and DepositFinalized events
Pool	Inspect Uniswap V4 pool on Polygonscan
Ownership	Bridge ownership is Ownable2Step (transparent)
No Hidden Controls
No one can mint BRVBTC without WBTC

No one can change the reserve ratio (it's a constant)

No one can pause transfers or freeze funds

The bridge is configurable only by its owner (currently the deployer)

📁 Contract Structure
solidity
contract BolivarRepublicaVenezuelaBTC is 
    ERC20, 
    ERC20Burnable, 
    ERC20Permit, 
    ReentrancyGuard, 
    IERC20TokenMetadata 
{
    IERC20 public immutable WBTC;
    address public immutable uniswapPoolManager;
    
    uint256 public constant CAP = 21_000_000 * 10**18;
    uint256 public constant RESERVE_RATIO = 50;
    uint256 public constant TOKEN_PER_WBTC = 100_000 * 10**18;
    
    uint256 public totalReserve;
    string private _tokenURI;
    address public metadataOwner;

    // Events
    event Minted(address indexed user, uint256 tokenAmount, uint256 wbtcAmount);
    event Burned(address indexed user, uint256 tokenAmount, uint256 wbtcAmount);
    event ReserveUpdated(uint256 newReserve, uint256 newTotalSupply);
    
    // Core functions
    function mint(uint256 wbtcAmount) external nonReentrant;
    function burnToWBTC(uint256 tokenAmount) external nonReentrant;
    function wbtcToToken(uint256 wbtcAmount) external pure returns (uint256);
    function tokenToWBTC(uint256 tokenAmount) external pure returns (uint256);
    function getCurrentReserveRatio() external view returns (uint256);
    function canMint(uint256 wbtcAmount) external view returns (bool);
    function canBurn(uint256 tokenAmount) external view returns (bool);
}
🛠️ Technology Stack
Solidity 0.8.27

OpenZeppelin (ERC20, ERC20Permit, ERC20Burnable, ReentrancyGuard)

Foundry (for testing, deployment, and verification)

EIP-712 (for secure bridge messages)

Uniswap V4 (for liquidity pools)

UniversalBridge (custom cross-chain bridge)

🚀 Getting Started
Prerequisites
Foundry

Node.js (optional, for frontend)

A wallet with some ETH/MATIC for deployment

Clone & Install
bash
git clone https://github.com/your-org/BRVBTC.git
cd BRVBTC
forge install
Compile
bash
forge build
Test
bash
forge test
Deploy (Example on Polygon)
bash
forge create --rpc-url polygon \
  --constructor-args "ipfs://your-metadata-uri" \
  --private-key $YOUR_KEY \
  src/BolivarRepublicaVenezuelaBTC.sol:BolivarRepublicaVenezuelaBTC
⚠️ Use CREATE2 to get the same address on both chains!

📊 Tokenomics Summary
Allocation	%	Amount	Vesting
Initial Liquidity (L1)	~76%	16,000,000	Unlocked (for bridge & trading)
Team & Development	~24%	5,000,000	Controlled by deployer (transparent)
Max Supply	100%	21,000,000	Hard cap, enforced by contract
🔮 Roadmap (Community-Driven)
✅ Token deployed on Ethereum & Polygon

✅ Bridge operational L1 ↔ L2

✅ Uniswap V4 pool initialized on Polygon

⬜ Community-led liquidity campaigns

⬜ Integration with major DeFi protocols

⬜ Partnerships and real-world use cases

⬜ Governance (if community desires)

🧪 Testnet (Coming Soon)
We will deploy testnet versions on:

Sepolia (Ethereum testnet)

Amoy (Polygon testnet)

For now, everything is live on mainnet — ready to be used.

🤝 Contributing
We welcome contributions from the community!

Found a bug? Open an issue

Want to improve the docs? Submit a PR

Built something cool with BRVBTC? Let us know!

📄 License
MIT © 2026 BRVBTC Team

💬 Community & Support
GitHub Issues: For technical discussions

Twitter/X: [@BRVBTC] (coming soon)

Discord/Telegram: (to be announced)

🙏 Final Words (From the Builder)
*"After 4 years of work, two tokens, a cross-chain bridge, and a vision — BRVBTC is finally live. It's not about promises. It's about math, transparency, and real value. 1 BRVBTC = 1 USD, backed by 50% WBTC, available natively on Ethereum and Polygon. We are at 0 today, but the fundamentals are already 100. The rest is up to the community."*

— The BRVBTC Team
