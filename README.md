# Morpho Core Protocol V1

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/uLq5V14.png">
  <img alt="" src="https://i.imgur.com/ZiL1Lr2.png">
</picture>

## What is Morpho?

Morpho is a lending pool optimizer: it improves the capital efficiency of positions on existing lending pools by seamlessly matching users peer-to-peer.

- Morpho's rates stay between the supply rate and the borrow rate of the pool, reducing the interests paid by the borrowers while increasing the interests earned by the suppliers. It means that you are getting boosted peer-to-peer rates or, in the worst case scenario, the APY of the pool.
- Morpho also preserves the same experience, the same liquidity and the same parameters (collateral factors, oracles, …) as the underlying pool.

TL;DR: Instead of borrowing or lending on your favorite pool like Compound or Aave, you would be better off using Morpho-Compound or Morpho-Aave directly.

## Contracts overview

Morpho protocol is designed at its core with a set of contracts acting as a proxy and communicating with upgradeable pieces of logic via calls (to implementation contracts) and delegate calls (to delegation contracts). Here is a brief overview of the Morpho protocol's contracts interactions:

![image](https://user-images.githubusercontent.com/44097430/170581601-307fbaae-2a27-4065-a9d1-f43172e4a30e.png)

The protocol's storage, located at Morpho's main proxy contract, is defined in the [`MorphoStorage`](https://github.com/morphodao/morpho-core-v1/blob/main/contracts/compound/MorphoStorage.sol) contract and is used by every delegation contract. Having this overview in mind, Morpho contracts typically fall under the following 4 main categories:

- Core features (supply, borrow, withdraw, repay, liquidate)
- Underlying logic (peer-to-peer matching, positions management)
- Peripheral contracts (lending/borrowing incentives, underlying protocol rewards management)
- Miscellaneous (maths, solidity calls, types)

## Documentation

- [White Paper](https://whitepaper.morpho.xyz)
- [Morpho Documentation](https://docs.morpho.xyz)
- Yellow Paper (coming soon)

## Bug bounty

A bug bounty is open on Immunefi. The rewards and scope are defined [here](https://immunefi.com/bounty/morpho/).
You can also send an email to [security@morpho.xyz](mailto:security@morpho.xyz) if you find something worrying.

## Morpho-Compound on Ethereum

- Morpho Proxy: [0x8888882f8f843896699869179fb6e4f7e3b58888](https://etherscan.io/address/0x8888882f8f843896699869179fb6e4f7e3b58888)
- Morpho Implementation: [0xd5ae0dabb7fc3bdb7d11d6aa13e7b5e01db4866a](https://etherscan.io/address/0xd5ae0dabb7fc3bdb7d11d6aa13e7b5e01db4866a)
- PositionsManager: [0x082bf6702e718483c85423bd279088c215a21302](https://etherscan.io/address/0x082bf6702e718483c85423bd279088c215a21302)
- InterestRatesManager: [0xe3556899a0f9faffc20cfbc6f926e2a377a1e5f3](https://etherscan.io/address/0xe3556899a0f9faffc20cfbc6f926e2a377a1e5f3)
- RewardsManager Proxy: [0x78681e63b6f3ad81ecd64aecc404d765b529c80d](https://etherscan.io/address/0x78681e63b6f3ad81ecd64aecc404d765b529c80d)
- RewardsManager Implementation: [0x70c59877f5358d8d6f2fc90f53813eb2b2698ab7](https://etherscan.io/address/0x70c59877f5358d8d6f2fc90f53813eb2b2698ab7)
- Lens Proxy: [0x930f1b46e1d081ec1524efd95752be3ece51ef67](https://etherscan.io/address/0x930f1b46e1d081ec1524efd95752be3ece51ef67)
- Lens: [0xe8cfa2edbdc110689120724c4828232e473be1b2](https://etherscan.io/address/0xe8cfa2edbdc110689120724c4828232e473be1b2)
- CompRewardsLens: [0x9e977f745d5ae26c6d47ac5417ee112312873ba7](https://etherscan.io/address/0x9e977f745d5ae26c6d47ac5417ee112312873ba7)

## Morpho-Aave on Ethereum

- Morpho Proxy: [0x777777c9898d384f785ee44acfe945efdff5f3e0](https://etherscan.io/address/0x777777c9898d384f785ee44acfe945efdff5f3e0)
- Morpho Implementation: [0x299ff2534c6f11624d6a65463b8b40c958ab668f](https://etherscan.io/address/0x299ff2534c6f11624d6a65463b8b40c958ab668f)
- EntryPositionsManager: [0xdf93cf1ca3acf96bc26783e6fab89400d362d0b4](https://etherscan.io/address/0xdf93cf1ca3acf96bc26783e6fab89400d362d0b4)
- ExitPositionsManager: [0xf6998f72b92b81c8f683d30ed8678d348fe9754b](https://etherscan.io/address/0xf6998f72b92b81c8f683d30ed8678d348fe9754b)
- InterestRatesManager: [0x400af815ef4de9e564fbf37268351a50134e6e36](https://etherscan.io/address/0x400af815ef4de9e564fbf37268351a50134e6e36)
- Lens Proxy: [0x507fa343d0a90786d86c7cd885f5c49263a91ff4](https://etherscan.io/address/0x507fa343d0a90786d86c7cd885f5c49263a91ff4)
- Lens: [0x8706256509684e9cd93b7f19254775ce9324c226](https://etherscan.io/address/0x8706256509684e9cd93b7f19254775ce9324c226)


## Common contracts on Ethereum

- ProxyAdmin: [0x99917ca0426fbc677e84f873fb0b726bb4799cd8](https://etherscan.io/address/0x99917ca0426fbc677e84f873fb0b726bb4799cd8)

## Licensing

The code is under the GNU General Public License v3.0 license, see [`LICENSE`](https://github.com/morphodao/morpho-core-v1/blob/main/LICENSE).

## Setup & Testing

First, you must install dependencies with:

```
yarn
```

To conduct test or deploy contracts you must create an environment file named `.env.local` and fill the environment variables.

```
cp .env.example .env.local
```

For the RPC endpoint you can choose your preferred one (do not forget to update the `Makefile` or `hardhat.config.js` accordingly).
`DEPLOYER_PRIVATE_KEY` is only required to deploy contracts.

### Testing with Foundry

Tests are run against a fork of the Ethereum mainnet, which allows us to interact directly with Compound.

You must install [Foundry](https://github.com/gakonst/foundry). Run the command below to get `foundryup`, the Foundry toolchain installer:

```
curl -L https://foundry.paradigm.xyz | bash
```

If you do not want to use the redirect, feel free to manually download the foundryup installation script from [here](https://github.com/gakonst/foundry).

Then in a new terminal session or after reloading your PATH, run it to get the latest forge version:

```
foundryup
```

Finally, update git submodules:

```
git submodule init
git submodule update
```

To run tests on different platforms, navigate a Unix terminal to the root folder of the project and run the command of your choice.

To run every tests:

```
make test-compound
```

or to run only the desired test contract:

```
make c-{TestContractName}
make c-TestBorrow
make c-TestGovernance
...
```

or to run individual tests:

```
make s-{testFunctionName}
make s-testSupply1
make s-testSupply2
...
```

For the other commands, check the `Makefile`.

### Testing with hardhat

Some hardhat tests are also present on this repository (testing of the [`IncentivesVault`](https://github.com/morphodao/morpho-core-v1/blob/main/contracts/common/rewards-distribution/RewardsDistributor.sol) contract).
You just need to run:

```
yarn test
```

For the other commands, check the `package.json` file.

## Questions & Feedback

For any question or feedback you can send an email to [merlin@morpho.xyz](mailto:merlin@morpho.xyz).
