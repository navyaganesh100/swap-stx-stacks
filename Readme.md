Deployed Contract Address = ST87DZSKM3M2NR2EB6G25ZP13GW9Q25026D24VEJ.swap-stx
🔄 STX → sBTC Swap Contract (Stacks / Clarity)
📜 Overview

This smart contract provides a simple interface to swap STX for sBTC using an existing Univ2 liquidity pool deployed on Stacks.

It wraps the swap function of the pool contract and ensures:

The caller has enough STX to cover the swap.

The pool call executes successfully.

Any swap failure reverts with a clear error.
<img width="1920" height="1080" alt="Screenshot from 2025-08-20 01-10-12" src="https://github.com/user-attachments/assets/f9b0cdf5-3471-4a43-aaf6-daf23c9eeb89" />

⭐ Features

✅ Swap STX → sBTC in a single call.

✅ Protects against insufficient balances.

✅ Emits the underlying swap event on success.

✅ Safe error codes for debugging.

⚙️ Error Codes
Code Meaning
u100 → ERR-SWAP-FAILED Pool swap call failed
u101 → ERR-INSUFFICIENT-FUNDS Caller balance < requested STX amount
📦 Contract Function
swap-stx-for-sbtc (stx-amount uint)

Swaps the given amount of STX into sBTC using the external pool.

Parameters:

stx-amount → The number of STX tokens to swap.

Flow:

Checks that caller (tx-sender) has enough STX.

Calls the external Univ2 pool contract’s swap function:

Token In: wstx (wrapped STX)

Token Out: sbtc-token

Fee contract: univ2-fees-v1_0_0-0070

If the pool swap fails, aborts with ERR-SWAP-FAILED.

Returns the raw swap event data on success.

Example Call:

(contract-call? .stx-sbtc-swap swap-stx-for-sbtc u1000000) ;; swap 1 STX (1_000_000 microSTX)

🛠️ Usage
Local Deployment (Clarinet)
clarinet new stx-sbtc-swap
cd stx-sbtc-swap

# replace contracts/stx-sbtc-swap.clar with this contract

clarinet check
clarinet console

On Testnet

Deploy via Stacks CLI
or Clarinet.

Open in Hiro Explorer
.

Call swap-stx-for-sbtc with the desired stx-amount.

📄 Security Notes

This contract depends on external Univ2 pool contracts:

Pool: SP20X3DC5R091J8B6YPQT638J8NR1W83KN6TN5BJY.univ2-pool-v1_0_0-0070

Fee: SP20X3DC5R091J8B6YPQT638J8NR1W83KN6TN5BJY.univ2-fees-v1_0_0-0070

Make sure these addresses match the ones on your target chain (testnet/mainnet).

The min-amount-out is hardcoded to u1 (may expose slippage risk).

📄 License

MIT — free to use, fork, and adapt.
