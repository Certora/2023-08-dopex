# Dopex audit details

# Overview

rDPX V2 introduces a new synthetic coin dpxETH which is pegged to ETH. dpxETH will be used to earn boosted yields on ETH and will be a staple collateral token for future Dopex Options Products.

The rDPX bonding process represents the method in which new dpxETH tokens can be minted. When a user bonds with the rDPX V2 contract they receive a receipt token. A receipt token represents ETH and dpxETH LP on curve.

Via the bonding process new dpxETH is minted and its backing is maintained via a rDPX and ETH reserve (the Backing Reserves). These backing reserves are controlled via AMOs. To ensure a safe and controllable way to scale rDPX V2 and dpxETH together we have decided incorporate the AMO ideology from Frax Finance.

Full product spec: https://dopex.notion.site/rDPX-V2-RI-b45b5b402af54bcab758d62fb7c69cb4

# Scope

*See scope.txt*

| Contract                                                                          | SLOCs | Purpose                                                        | Libraries used                                                                 |
| --------------------------------------------------------------------------------- | ---- | -------------------------------------------------------------- | ------------------------------------------------------------------------------ |
|  UniV2LiquidityAmo.sol                      | 271  | This contract encompasses all functions for the Uniswap V2 AMO | [`@openzeppelin/*`](https://openzeppelin.com/contracts/), Uniswap V2 libraries |
|  UniV3LiquidityAmo.sol                      | 269  | This contract encompasses all functions for the Uniswap V3 AMO | [`@openzeppelin/*`](https://openzeppelin.com/contracts/), Uniswap V3 libraries |
|  RdpxV2Core.sol                                   | 708 | This is the core contract of rDPX V2                           | [`@openzeppelin/*`](https://openzeppelin.com/contracts/)                       |
|  RdpxV2Bond.sol                                   | 54   | ERC721 contract for minting NFT bonds via the core contract    | [`@openzeppelin/*`](https://openzeppelin.com/contracts/)                       |
|  RdpxDecayingBonds.sol           | 119  | Contract responsible to mint rDPX decaying bonds               | [`@openzeppelin/*`](https://openzeppelin.com/contracts/)                       |
|  DpxEthToken.sol                               | 51   | ERC20 dpxETH token contract                                    | [`@openzeppelin/*`](https://openzeppelin.com/contracts/)                       |
|  PerpetualAtlanticVault.sol     | 420  | Contract for the Perpetual Atlantic Vault (ERC721)             | [`@openzeppelin/*`](https://openzeppelin.com/contracts/)                       |
|  PerpetualAtlanticVaultLP.sol | 182  | Contract for the Perpetual Atlantic Vault LP (ERC4626)         | [`@openzeppelin/*`](https://openzeppelin.com/contracts/), solmate              |
|  ReLPContract.sol                     | 190  | Contract to perform the reLP process on the Uniswap V2 AMO     | [`@openzeppelin/*`](https://openzeppelin.com/contracts/)                       |

## Out of scope

RdpxV2ReceiptToken contracts, staking contracts, reserve contracts, dpxETH/ETH oracle.

 

## Setup

```bash
# Cloning
git clone --recurse  2023-08-dopex.git
# Updating with submodule if the repo was cloned without `--recurse-submodules`
git submodule update --init --recursive
```

Having foundry installed: https://book.getfoundry.sh/getting-started/installation

> (Optional) Setup the `.env` file with the vars mentioned in the `.env.sample` file.

### Compiling

```bash
forge build
```

### Running tests

Run all tests like this:

```bash
forge test
```

### Running coverage

First, comment the following to avoid a stack too deep error due to https://github.com/foundry-rs/foundry/issues/3357:

-  Periphery.t.sol#L131-L221
-  UniV3LiquidityAmo.sol#L213-L270

Then, to run solidity code coverage and generate the coverage reports, please use one of the following commands:

```bash
sh coverage.sh
```

or 

```bash
chmod +x coverage.sh
./coverage.sh
```

### Slither

Slither's output can be found at slither.txt. 
You can run it on your own with `slither .`
