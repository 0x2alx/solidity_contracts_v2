# Ghosty Contracts

## ERC721
This is a collection of solidity NFT smart contracts by [@ghooost0x2a](https://twitter.com/ghooost0x2a).

For now, only ERC721 contract is provided. ERC1155 might be added in the future.

### Why?

Many people seem to be using manifold nowadays, and although they are doing a great job, their contracts are not perfect. For one, they have not yet implement the OpenSea RegistryFilter required for Royalties to be respected on OS sales.
My contract is also full of features, customizable and easy to use.

### Features

The contract was built by combining mutliple contracts and features from various places. It is based on the Ultra gas optimized ERC721B contract by @squuebo_nft integrated with the LockRegistry (2FA) contracts by @OwlOfMoistness (more on this later) and heavily modified and tested. Here are some of the features:
* **Ultra Low Gas**
* **2FA**
* **Access Control/Delegation**
* **Pausable**
* **OpenSea RegistryFilter/Royalties Compliant**
* **Set default and per token royalties**
* **Set/Update your token URI/metadata**
* **Mint to your own wallet or do airdrops to your collector wallets directly**
* **Possibility of locking up the collection (so no more minting can be done)**
* **Supports batch transfers**

### Deployment Steps
Note that the full deployment tutorial starts with deploying to Goerli testnet. If you want to deploy to mainnet directly (I recommend deploying to testnet at least once), please skip directly to the **Deploying on Mainnet** section.

#### Deploying on Goerli testnet
1. Enable Test Networks in your metamask
2. Get Goerli testnet ETH
3. Setup RemixIDE
4. Deploy to Goerli testnet
5. Test contract/minting on Goerli testnet

#### Deploying on Mainnet
1. Setup RemixIDE
2. Deploy to Goerli testnet
3. Test contract/minting on Goerli testnet

#### Deploying on Goerli testnet
##### 1. Enable Test Networks in your metamask
![enable_testnets_png](assets/enable_testnets.png)