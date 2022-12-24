# Ghosty Contracts

# ERC721
This is a collection of solidity NFT smart contracts by [@ghooost0x2a](https://twitter.com/ghooost0x2a).

For now, only ERC721 contract is provided. ERC1155 might be added in the future.

## Why?

The motivation behind is project is to offer NFT creators/artists an alternative solution for their smart contract deployment. Instead of minting your NFTs on some markeplace contract you do not own or using other solutions like manifold that are more limited in terms of features, I am providing my **GhostyERC721Ctr.sol** contract for anyone who would like to use it. 

The tradeoff is complexity. Going this way is a bit more complicated than using manifold or lazy minting, BUT I believe it is worth it (see list of features below). The good news is, I have provided a very detailed guide below, as well as video demos. If you read it all, you will likely get a better understanding of how smart contracts work and will be able to easily deploy and interact with your own contract. Once you understand the process, you can easily deploy as many contracts/collections as you want.

## Features

The contract was built by combining mutliple contracts and features from various places. It is based on the Ultra gas optimized ERC721B contract by @squuebo_nft integrated with the LockRegistry (2FA) contracts by @OwlOfMoistness (more on this later) and heavily modified and tested. Here are some of the features:
* **Ultra Low Gas**
* **Access Control/Delegation**
* **Pausable**
* **OpenSea RegistryFilter/Royalties Compliant**
* **Set default and per token royalties**
* **Set/Update your token URI/metadata**
* **Mint to your own wallet or do airdrops to your collector wallets directly**
* **Possibility of locking up the collection (so no more minting can be done)**
* **Supports batch transfers**
* **2FA**

## Table of Contents
Note that the full deployment tutorial starts with deploying to Goerli testnet. If you want to deploy to mainnet directly (I recommend deploying to testnet at least once), please skip directly to the **[Deploying on Mainnet](#deploying-on-mainnet-1)** section.

*Note these steps were all done on desktop Metamask using Chrome. That being said, they should work on any desktop browser.*

### [Deploying on Goerli testnet](#deploying-on-goerli-testnet-1)
1. [Enable Test Networks in your metamask](#1-enable-test-networks-in-your-metamask)
2. [Get Goerli testnet ETH](#2-get-goerli-testnet-eth)
3. [Setup RemixIDE](#3-setup-remixide)
4. [Deploy to Goerli testnet](#4-deploy-to-goerli-testnet)
5. [Test contract/minting on Goerli testnet](#5-test-contractminting-on-goerli-testnet)

***This is the [link](https://goerli.etherscan.io/address/0x6f027405bb6d0088209abba85dd69c3594fab875#code) to the Goerli tesnet contract deployed in this documentation.***

### [Deploying on Mainnet](#deploying-on-mainnet-1)
1. [Setup RemixIDE](#1-setup-remixide)
2. [Deploy to Mainnet](#2-deploy-to-mainnet)
3. [Test contract/minting](#3-test-contractminting)

### [Interacting with your Contract]()
*This section is important in order to understand how the contract works and how to use the various features.*
1. [Smart Contracts General Info]()
2. [Minting info]()
3. [Access Control/Delegation]()
4. [Configure metadata]()
5. [Reduce collection size/Lock Minting]()
6. [Setting roylaties on contract]()
7. [Extra READ functions]()
8. [Extra WRITE functions]()


### Deploying on Goerli testnet
#### 1. Enable Test Networks in your metamask
In metamask Settings > Advanced, enable **Show test networks**

![enable_testnets_png](assets/enable_testnets.png)

#### 2. Get Goerli testnet ETH
1. First of all, create a FREE Alchemy account by going to **https://auth.alchemy.com/signup**.

2. Once your account is created, go to **https://goerlifaucet.com/**, connect your newly created Alchemy account.

3. Enter your wallet address (the one you will deploy the contract from) and click **Send me ETH**

![goerli_faucet](assets/goerli_faucet.png)

4. In metamask, switch your network to **Goerli test network** and confirm you received 0.5 Goerli ETH.

![goerli_network](assets/switch_network.png)
![goerli_eth](assets/goerli_eth.png)

#### 3. Setup RemixIDE 
RemixIDE is an online solidity development platform. It has all the necessary features to easily compile and deploy smart contracts, verify them, interact with them, etc.

1. Open this page in a new tab, **https://github.com/ghooost0x2a/ghosty_contracts**, click on **Code** and **Download as ZIP**

![github_download](assets/github_download.png)

2. Unzip the **ghosty_contracts-main.zip** file you just downloaded. You should end up with a folder containing all the files.

![unzip_folder](assets/unzipped_folder.png)

3. Go to **https://remix.ethereum.org/**. Delete everything in the **contracts** folder (in the left pane).

![remix_1](assets/remix_1.png)

4. Select the **contracts** folder, and click on the little **Upload** icon. Go to the unzipped folder and select the **GhostyERC721Ctr.sol**

![remix_2](assets/remix_2.png)

5. (Optional) You can delete or change the ASCII art at the top of the contract. Only delete the selected text (in the screenshot below), make sure not to delete the /\*\*\* at the top. *Note that in solidity, multi-line comments start with /\*\*\* and end with \*/. In remix, comments appear as green text.*

![remix_3](assets/remix_3.png)

6. In the **GhostyERC721Ctr.sol** file, search for the following text '**GhostyERC721Ctr_NAME_TO_REPLACE**'. Change that to the name of your collection. Then search for the text '**G0x2a**' and replace that with the token symbol you want (this is a 2-4 character code that will use to identify the token/NFT on the blockchain. For example: A15, DS, DD, etc.)

7. (Optional) Search for '**uint256 public MAX_SUPPLY = 10000**' in the contract (should be just above the ones from step #6). Change the value (10000) to the maximum size of your collection. Note that you are better off putting a bigger number now and reducing it afterwards. Once the contract is deployed, you will unable to mint more than MAX_SUPPLY tokens and that value cannot be increased AFTER the contract has been minted. 

8. Click on the editor and click **CTRL+S** to save the changes. 
#### 4. Deploy to Goerli testnet
1. On the left-hand menu in RemixIDE, click on the third icon, the **Solidity Compiler**

![remix_4](assets/remix_4.png)

2. At the top, in the **Compiler** dropdown, select the second option from the top (highest version that doesn't start with *latest local...*)

![remix_5](assets/remix_5.png)

3. Click on **Advanced Configuration** and check the **Enable optimization** checkbox. Then click on the big blue **Compile GhostyERC721...** button.

![remix_6](assets/remix_6.png)

4. If the compiler was showing any errors before, they should now have disappeared. The left-hand menu should show a green check mark.

![remix_7](assets/remix_7.png)

##### 5. Deploying
On the left-hand menu, go to the 4th icon, **Deploy & Run transactions**. On the **Environment** dropdown, select *Inject Provider - MetaMask* (make sure your metamask is on the Goerli Network). The small text under the drodown should say *Goerli (5) network*. In the **Contract** dropdown, select the contract named '**GhostyERC721Ctr - contracts/GhostyERC721Ctr.sol**' (it's important to select the rigth contract. The name should start with GhostyERC721Ctr).

![remix_8](assets/remix_8.png)

6. Click on **Deploy** and confirm the transaction in the MetaMask popup. Once the transaction finishes, you will see a message at the bottom of the RemixIDE window. Click on **view on etherscan**.

![remix_9](assets/remix_9.png)

7. On the etherscan transaction page, click on the Contract address (this might take a while to appear, just refresh the page until it does). This will bring you to the etherscan contract page. 

![remix_10](assets/remix_10.png)

8. On the Etherscan page, click on **Contract** and then **Verify and Publish**.

![remix_11](assets/remix_11.png)

9. On the following page, For **Compiler Type** put *Solidity single file*. For **Compiler version**, select the same version as used in step #2, above. For the **License Type**, select *3) MIT License (MIT)*. Click on **Continue**

![etherscan_1](assets/etherscan_1.png)

10. On the next page, on the right, set the **Optimization** to *Yes*. Go back to RemixIDE, and copy the whole contract code (CTRL+A and CTRL+C). Paste that code on the Etherscan page, in the **Enter the solidity Contract Code below** text field. Scroll at the bottom and click on **Verify and Publish**. This might take a few minutes...

![etherscan_2](assets/etherscan_2.png)

11. Once the verification is completed, Etherscan will show you a message like **Successfully generated ByteCode and ABI for Contract Address [...]**. You can click on the **Contract address** to get back to your contract code page.

![etherscan_3](assets/etherscan_3.png)

12. On your Etherscan contract page, you should now see a green check mark next to the **Contract** tab. If you click on it, you should also see 3 new buttons, **Code**, **Read Contract** and **Write Contract**. This confirms that your contract source code was successfully verified. Congrats!

![etherscan_4](assets/etherscan_4.png)

#### 5. Test contract/minting on Goerli testnet
Now that our contract is deployed and verified, let's interact with it. This is mainly done on Etherscan itself.
1. Go to your Etherscan contract page and click on **Contract**, **Write Contract**. Then click on **Connect to Web3**. Make sure to connect with the same address you used to deploy the contract. 

![etherscan_5](assets/etherscan_5.png)
2. Click on function #7 **ownerMints**, and in quantity set **1** and for recipients set **\[YOUR_OWN_ADDRESS\]** (make sure to replace the YOUR_OWN_ADDRESS with your actual address between \[square brackets\]). Click on **Write** and approve the transaction in the Metamask popup.

![etherscan_6](assets/etherscan_6.png)
3. Go to OpenSea testnet page (https://testnets.opensea.io/) and search for your contract address. Make sure to wait for OpenSea dropdown and click on the search result (not on the looking glass or ENTER). Note, this will only work AFTER you minted at least 1 token.

![os_1](assets/os_1.png)

**CONGRATULATIONS! You deployed your own contract to Goerli testnet. If you are ready to deploy to Mainnet, please read on.**

### Deploying on Mainnet

#### 1. Setup RemixIDE
1. Switch your Metamask network to ETH Mainnet.
2. Repeat step 3 of the Goerli testnet instructions **[Setup RemixIDE](#3-setup-remixide)**. **If you already did this step for the Goerli testnet deployment, you can skip it**

#### 2. Deploy to Mainnet
1. Repeat step 4 of the Goerli testnet instructions **[Deploy to Goerli testnet](#4-deploy-to-goerli-testnet)** BUT at **[step 5](#5-deploying)**, make sure that under the **Environment** it says *Main (1) network*.

![remix_12](assets/remix_12.png)

#### 3. Test contract/minting
4. Repeat step 5 of the Goerli testnet instructions **[Test contract/minting on Goerli testnet](#5-test-contractminting-on-goerli-testnet)**. Just make sure your wallet is on the **Mainnet** network. *Also, in step 3, instead of going to the OS test page, you can go to the regular **[OpenSea](https://opensea.io/)***


### Interacting with your Contract


#### 1. Smart Contracts General Info
What is a smart contract anyway? 
Simply put, a smart contract is a program (written in solidity language), stored on the blockchain. This program is stored at a given address (called the contract or collection address) created at the moment of the contract deployment on the blockchain.
The program contains variables and functions (procedures). Once a contract is deployed on the blockchain, we can interact with it, aka read and modify its variables and call its functions. 

A DAPP (Decentralized APP) is simply a web2 website with code allowing it to interact with the blockchain and call the functions on a given contract. It serves as the GUI for interacting a contract. So when an NFT project deploys a smart contract, they will typically create a DAPP that will allow its community to mint the NFTs. The DAPP simply sends calls to the mint function on the smart contract, on behalf of the user who then approves those calls/interactions in their wallet (e.g. Metamask).

This documentation does not cover DAPP creation. That subject is a more complex subject and the GhostyERC721Ctr contract only has one mint function reseved to the owner/deployer of the contract. As mentioned, DAPPs are simply user interfaces to interact with a smart contract, but there are other ways to do that. The easiest is using etherscan directly. When we deploy and verify our smart contract, etherscan gives us access to its variables and functions. We can simply call the contract functions (like mint), from etherscan itself, without any DAPPs.


#### 2. Minting info

As mentioned this contract has only one minting function called **ownerMints**. This function can only be used/called by the owner/creator of the contract, and his chosen delegates (see next section for more info on delegates).

The **ownerMints** function takes two parameters (arguments/variables). In other words, when we call this mint function, we need to give it two pieces of information, namely the **quantity** of NFTs we would like to mint, and the **recipients** of those NFTs aka the address(es) where we want to send those NFTs. 

This mint function, can be used two ways; **Minting to a SINGLE wallet** or doing an **Airdrop to MULTIPLE wallets** 


##### Minting to a SINGLE wallet
Use this method to mint one or multiple NFTs to a ***SINGLE*** wallet (that you own). In order to do this, you enter the **quantity** you want (number of NFTs) and for **recipients**, you put one of your OWN wallet \[addresses\] (DO NOT PUT THE CONTRACT ADDRESS). This could be the same address you used to deploy the contract, or another one that you own. This is basically the address where all the (**quantity**) NFTs will be sent once minted.

**Make sure that the \[address\] is between square brackets, this is IMPORTANT! (see example screenshot)**

* *Of course, this function will fail if you are not connected to etherscan with an authorized address (either the owner/creator or a delegate address).*

* *Another potential failure reason is if you are busting the MAX_SUPPLY you set in the contract during deployment. MAX_SUPPLY is the absolute maximum amount of NFTs that can ever exist in this collection. You can view its value by goign to the **Read Contract** tab, and clicking on MAX_SUPPLY* 

![etherscan_int_1](assets/etherscan_int_1.png)

##### Airdrop to MULTIPLE wallets
Use this method to mint/airdrop NFTs to ***MULTIPLE*** wallets. In order to do this, you provide the **quantity** and for **recipients**, a ***LIST*** of addresses (not just one), separated by commas (,) and between \[square brackets\].

**VERY IMPORTANT!** This method will mint ONE nft to EACH address provided in the list. This means that the number of addresses provided in the list must exactly match the **quantity** number. If you want to mint/airdrop more than one to the same address, simply put that same address multiple times in your **recipients** list. That person will get as many NFTs as times their address appears in the **recipients** list.

**Examples**

***Airdropping 3 NFTs to 3 different persons***

![etherscan_int_2](assets/etherscan_int_2.png)


***Airdropping 2 NFTs to 1 person, and 2 to 2 other persons***

As we can see in the screenshot below, the first (1) and second (2) address highlighted in yellow are one and the same. This means that it gets dropped 2 NFTs. Addresses 3 and 4 are both different, and they each get dropped 1 NFT for a total **quantity** of 4.

![etherscan_int_3](assets/etherscan_int_3.png)


#### 3. Access Control/Delegation
The **GhostyERC721Ctr** contract implements the **OWNABLE** (Common OpenZeppelin library) functionality. This is a common thing for ERC721 contracts. This functionality defines an **OWNER** address. This is used to restrict the access of some of our smart contract functions, like the mint function. The **ownerMints** is restricted, otherwise anyone could mint NFTs on your contract for free. This is also used to restrict other functionality like setting/changing the metadata, the MAX_SUPPLY (size of the collection), and so on. By default, the owner of a contract is the address/person that deploys it on the blockchain.

On top of the **Ownable** feature, this contract also implements **DELEGATES**. These are additional addresses, configured by the **OWNER** (only) that have access to restricted functions like mint, setting MAX_SUPPLY, setting metdata, etc. 

An address designated as **DELEGATE** has the ALL the permissions that the **OWNER** has **EXCEPT** for the ability to designate other delegates. Only the **OWNER** of the contract can set and remove delegates.

There are two main reasons for using delegates; If you are collaborating on a project with someone, and you want to give them access to mint and control the contract OR, if you want to give delegation to another one of your OWN addresses, for convenience (for instance, you deploy the contract from your ledger, but you delegate one of your metamask addresses to be able to mint from it).

##### Add/Remove delegate
In order to add a new delegate address, first go to Write Contract on Etherscan, and **Connect to Web3** with the **OWNER** wallet (the one you deployed from). Scroll down and click on function #18 **setDelegate**. For **addr** field, enter the address you would like to set as delegate (cannot be the contract address nor the **OWNER** address). For the **isDelegate_** field set the value to **true** and click on **Write**.

If you want to *remove* a previous delegate, simply put **false** in the **isDelegate_** field.

![etherscan_int_4](assets/etherscan_int_4.png)

##### Check if an address is a delegate
On Etherscan, switch to the **Read Contract** tab, scroll down to function #9 **isDelegate**. Enter the address you want to check and click on **Query**. This will return true or false.

![etherscan_int_5](assets/etherscan_int_5.png)


#### 4. Configure metadata
An NFT's metadata is not stored on the blockchain. The smart contract is simply text/code that dictates who owns what NFT in the collection. The contract has a function called **tokenURI** which returns the URI to the metadata of a given token number. In other words, it tells us the location of the metadata for a specific token in that collection, based on the token number. The metadata is a json file (a text file) containing information about the NFT; i.e. Description, title, image_url, attributes/traits, etc. 

Marketplates like OpenSea and Foundation (or any other NFT marketplace), interact with your smart contract by calling the **tokenURI** function for every token in your collection. It then uses the result that our smart contract returns, which will be a link to our json/text file. OS will then look into that file, find the image_url and use that to show you the NFT image/art. It will also get the attributes, title and description from that same json/text file.

What is important to understand here is that the blockchain, the smart contract, is not aware of your metadata or image. The json/text files and images are uploaded separately and independently of the smart contract itself, typically to a decentralized storage like IPFS or arweave. Once uploaded, we will update the **tokenURI** function on our smart contract to point to our freshly uploaded json/text files (which in turn will point to our images).

##### 4. Uploading your files to IPFS (free)

There are many IPFS providers out there and most of them offer a free IPFS tier with limits on the number of files/storage size. This is perfect for one of one artists, as the amount of data is small compared to a generative project. For this documentation, we will use Filebase (https://filebase.com/). Their free tier allows for 5 GB of storage and 1000 pinned files (more than enough). 

1. Start by creating a free account on https://filebase.com/. Once you confirm your email and login, yoou should see the Filebase dashboard 

![filebase_1](assets/filebase_1.png)


