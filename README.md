<p align="center"><a href="README.md">English</a> · <a href="README.pt-BR.md">Português</a> · <a href="README.es.md">Español</a></p>

<p align="center">
  <img src="assets/hatchpad-logo-512.png" width="120" alt="Hatchpad" />
</p>

<h1 align="center">Hatchpad — hatchpad.fun</h1>

<p align="center">Permissionless memecoin launchpad on Robinhood Chain.<br/>Tokens hatch on a bonding curve and graduate to Uniswap V3 with liquidity locked forever.</p>

---

## How it works

1. **Create** — anyone can launch a token in seconds for a 0.002 ETH fee. Every
   token has a fixed supply of 1,000,000,000 and the same transparent
   allocation: **80%** sold on the bonding curve, **10%** reserved for Uniswap
   liquidity, **5%** to the creator, **5%** to a community airdrop.
2. **Trade** — buys and sells happen on a constant-product bonding curve. Price
   moves deterministically with supply; there are no order books and no
   presales. Every trade pays a **1% fee**, split 50/50 between the token
   creator and the protocol.
3. **Graduate** — when the curve collects **2.5 ETH**, trading moves to a
   canonical **Uniswap V3** pool created at the exact final curve price. The
   LP position is minted to a vault that can **never withdraw the principal or
   transfer the NFT** — liquidity is locked forever. LP trading fees keep
   flowing: 50% to the creator, 50% to the protocol.
4. **Airdrop** — any creator can distribute their token with a built-in Merkle
   airdrop: paste a list of addresses, deploy a distributor, fund it, and
   recipients claim on-chain. Unclaimed tokens can be swept back by the
   creator after the claim window ends.

## Fees at a glance

| Fee | Amount | Where it goes |
| --- | --- | --- |
| Token creation | 0.002 ETH | protocol |
| Curve trading fee | 1% per trade | 50% creator / 50% protocol |
| Post-graduation LP fees | Uniswap V3 1% tier | 50% creator / 50% protocol |

Each launch snapshots its economics at creation — the protocol cannot change
fees or targets for an existing token, ever.

## The HATCH token

Fixed supply of **1,000,000,000 HATCH**. No minting after deployment.

| Allocation | Share |
| --- | --- |
| Community & airdrops | 50% |
| Protocol treasury | 20% |
| Ecosystem incentives | 15% |
| Team (cliff + linear vesting) | 10% |
| Liquidity reserve | 5% |

### Buyback & burn

**40% of protocol fees** are automatically routed by an on-chain splitter to a
burner contract. Executing a burn requires approval from the protocol multisig
(at least 2 of 3 signers); the contract then buys HATCH on Uniswap V3 and
calls `burn()`, permanently reducing total supply. Every burn emits a public
on-chain event with the exact amounts.

Governance may adjust the burn share within contract-enforced bounds; it can
never be set below 10%. Burns are discretionary supply management. Nothing in
these docs is financial advice or a promise of token value.

## What the protocol can and cannot do

**Cannot** (enforced by contracts):

- withdraw curve reserves or locked LP principal
- change the economics of an already-launched token
- mint more supply of any token, including HATCH
- block sells, graduation, or valid claims — even during an emergency pause

**Can** (governance, multisig + 48h timelock, all publicly logged):

- adjust bounded defaults for *future* launches (creation fee ≤ 0.01 ETH,
  trade fee ≤ 2%, graduation target 0.5–10 ETH)
- pause *new* launches during an incident (auto-expires in 72h)
- hide malicious token metadata from discovery (the contract stays usable)
- approve buyback burns and community takeovers of abandoned tokens

## Security

- Full test suite: unit, fuzz, invariant, and mainnet-fork tests against
  canonical Uniswap V3 on Robinhood Chain
- Stateful fuzzing (Echidna), symbolic execution (Halmos), and mutation
  testing (100% mutants caught on the pricing math)
- Static analysis (Slither) with public triage
- Liquidity locked by contract, not by promise

⚠️ Hatchpad is in **beta** and the contracts have not yet completed an
independent third-party audit. Memecoins are highly speculative — never spend
what you cannot afford to lose.

## Links

- App: [hatchpad.fun](https://hatchpad.fun)
- X / Twitter: [@hatchpadfun](https://x.com/hatchpadfun)
- Telegram: [t.me/hatchpadfun](https://t.me/hatchpadfun)
- Chain: Robinhood Chain (id 4663) · explorer via Blockscout

Contract addresses will be published here after mainnet deployment and
verification.
