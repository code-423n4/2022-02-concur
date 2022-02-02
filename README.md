# Concur Finance contest details
- $71,250 USDC main award pot
- $3,750 USDC gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-02-concur-finance-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts February 3, 2022 00:00 UTC
- Ends February 9, 2022 23:59 UTC

### ConcurRewardPool

sloc : 41

This contract holds the rewards that has to go to Convex LP stakers.

80 % of all rewards will be pushed to stakers and user can claim tokens here.

### ConvexStakingWrapper

sloc : 293

Convex wrapper forked from [convex](https://github.com/convex-eth/platform/blob/main/contracts/contracts/wrappers/ConvexStakingWrapper.sol)

Modified logic is, it is no longer a ERC20, and it will hold all Convex LPs in one contract.

Convex LP holders will stake to this contract all rewards from Convex will be available in ConcurRewardPool.

When user deposits/withdraws LP, it will be notified to MasterChef.

This relies heavily on convex LP contracts and Curve pool contract.

### EasySign & VoteProxy

sloc : VoteProxy = 36, EasySign = 223

Vote proxy to enable contract signing with EIP-1271.

### MasterChef

sloc : 212

MasterChef **without** actual stake token transfers. It is used to distribute governance token without minting/depositing. Tokens will be pre-deposited before the `_startBlock`. Depositor role will be assinged to ConvexStakingWrapper and StakingRewards contract.

### Shelter

sloc : 59

Shelter for tokens when emergency happens.

### StakingRewards

sloc : 220

Single token reward contract. Will be used to give reward to governance token stakers with non-governance token (CRV/CVX).

### USDMPegRecovery

sloc : 129

- USDM deposit USDM into USDM side of the contract
- Once 40m USDM is deposited, 3Crv side of the contract starts accepting deposits
- PBM then deposits USDM with 3Crv in 50/50 ratio as 3Crv is deposited
- USDM deposits are locked based on the KPI’s from carrot.eth
- 3Crv deposits are not locked
