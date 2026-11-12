# clone-lin-aave-cumulate

Experimental **LIN** clone of Aave V3 `ReserveLogic.cumulateToLiquidityIndex`
(flashloan premium folded into the aToken liquidity index).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [aave/aave-v3-core](https://github.com/aave/aave-v3-core) `782f51917056a53a2c228701058a6c3fb233684a`
  - `ReserveLogic.sol` sha256 `6b827ea494fa5bb1b38fa9e7db973bd0aed0ee3d53677cac950f6614cb8fd0c9` blob `bc48163dbbfcac7c832d2e9dfef71a9ddadfe836`
  - `WadRayMath.sol` sha256 `fae5b995ec613cc213050c99ea6352c9c18ceebba106d03b1726cfa8f1f0124e` blob `f61fe87f2f2748144cd4d113c848e649c41a4e5d`
- **License of the algorithm:** MIT after BUSL Change Date 2023-01-27. This clone is original LIN/C11.
- **Class:** EXPERIMENTAL uint64-scale, `RAY' = 1e9` (mainnet `RAY = 1e27` does not fit i64).

## Files

- `src/lin_aave_cumulate.lin` — LIN kernel (`acl_cumulate(total_liq, amount, index)`)
- `test/oracles/aave_cumulate_c11.c` — independent C11 `__int128` XOR limb oracle (not TCB)

## Reproduce proofs (in lin-open)

```bash
make aave-cumulate-proof
# or: python3 test/prove_aave_cumulate_external.py
```

Named goldens: identity `amount=0` leaves index `1e9`; 0.1% premium **1001000000**;
0.09% flashloan premium **1000900000**; `rayMul(1, 5e8)` half-up **1** vs floor **0**.

## Not claimed

Uint256 / RAY=1e27 / aToken mainnet parity. LIN replacing Aave or the EVM.
TVL or dollar savings. zk soundness.
