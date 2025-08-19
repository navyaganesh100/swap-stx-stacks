🔄 STX → sBTC Swap Contract (Stacks / Clarity)

Deployed Contract Address
ST87DZSKM3M2NR2EB6G25ZP13GW9Q25026D24VEJ.swap-stx

📜 Overview

This smart contract enables seamless swaps of STX → sBTC through an integrated Univ2 liquidity pool on Stacks.
It ensures safe execution, balance checks, and clear error codes on failures.
<img width="1920" height="1080" alt="Screenshot from 2025-08-20 01-10-12" src="https://github.com/user-attachments/assets/f9b0cdf5-3471-4a43-aaf6-daf23c9eeb89" />

⭐ Features

✅ Swap STX → sBTC in a single transaction

✅ Protects against insufficient STX balances

✅ Emits pool swap event on success

✅ Safe error codes for debugging

⚙️ Error Codes
Code	Meaning
u100	ERR-SWAP-FAILED → Pool swap call failed
u101	ERR-INSUFFICIENT-FUNDS → Caller balance < requested STX amount
📦 Contract Function

swap-stx-for-sbtc (stx-amount uint)

Swaps the given STX amount into sBTC using Univ2 pool.

Parameters:

stx-amount → Number of STX tokens to swap

Flow:

Verify caller balance ≥ stx-amount

Call external Univ2 pool:

Token In → wstx (wrapped STX)

Token Out → sbtc-token

Fee Contract → univ2-fees-v1_0_0-0070

Revert on pool failure with ERR-SWAP-FAILED

Return swap event data on success

Example Call:

(contract-call? .stx-sbtc-swap swap-stx-for-sbtc u1000000) ;; swap 1 STX (1,000,000 microSTX)

🛠️ Setup & Usage
Local Deployment (Clarinet)
clarinet new stx-sbtc-swap
cd stx-sbtc-swap

# Replace contracts/stx-sbtc-swap.clar with this contract

clarinet check
clarinet console

On Testnet / Mainnet

Deploy using Stacks CLI or Clarinet

Open contract in Hiro Explorer

Call swap-stx-for-sbtc with desired STX amount

📄 Security Notes

Relies on external Univ2 pool contracts:

Pool: SP20X3DC5R091J8B6YPQT638J8NR1W83KN6TN5BJY.univ2-pool-v1_0_0-0070

Fee: SP20X3DC5R091J8B6YPQT638J8NR1W83KN6TN5BJY.univ2-fees-v1_0_0-0070

Ensure addresses match your target chain (Testnet/Mainnet)

Min-amount-out = u1 (potential slippage risk)

👩‍💻 Tech Stack

Language: Clarity (Stacks Smart Contracts)

Tools: Clarinet, Stacks CLI

Network: Stacks Testnet/Mainnet
