---
title: "Choosing the right blockchain for your next NFT project"
layout: post
permalink: /blog/right-blockchain-for-nft-platform/ 
date: '2022-06-08T10:00:00.000-03:00' 
category: development
tags:
  - Blockchain development
  - NFT Marketplace
  - DApp Development
  - Smart Contract Developmen
author_id: mtnBarreto
author: Martin Barreto
show: true
featured_image: /images/choosing-the-right-blockchain/CHOOSING_THE_RIGHT_BLOCKCHAIN.png
---


Choosing the right blockchain is vital during the early development stage of an NFT platform. There are plenty of options that provide different capabilities, each having advantages and disadvantages. NFT DApps are getting more sophisticated as well as their requirements in terms of blockchain technology (mainly security, scalability, and low transaction gas fee).

This blog post introduces three NFT platform caegories according to their functional and technology requirements. We also evaluate the most  suitable blockchains for each one and give examples of popular NFT DApps built on top of them. I hope thse cateories help you find the most suitable blockchains for the NFT idea you have in mind. 

## What to consider when choosing the right blockchain:

- It should support functionality for the time to come. You should make sure it can develop every use case and that your team will never get stuck with technical limitations.
- Make sure the ecosystem and community around the blockchain are thriving. It's not all about good tech and solid fundamentals; the ecosystem and what it builds around it matter too.
- A marketplace of their own is not a requirement for some NFT solutions. There are third-party marketplaces where NFTs can be bought and traded, such as [Open Sea](https://opensea.io/), which supports a few blockchains.

## What Blockchain platforms to consider

The following section will list different blockchain platforms according to market capitalization. Later we’ll dive into some of them in further detail. 

Although there’s an abundance of blockchains, only a small percentage of them have smart contract capabilities, a must-have for developing dApps (NFTs and their marketplaces).

### By market capitalization

The most popular blockchains according to market capitalization are changing constantly, and the ranking is greatly affected by industry innovations. Just as an example of this, many of the [top 10 cryptocurrencies in 2017](https://coinmarketcap.com/historical/20171217/) have disappeared or are no longer in the top 10.
Here is [Coinmarketcap’s](https://coinmarketcap.com/) list of blockchains by market capitalization; Ethereum, Cardano, Solana, Polkadot, Avalanche, and Polygon are the most popular blockchains with smart contracts support within the top 20 (at the moment of writing this blogpost).

![Coinmarketcap top 20 blockchains with smart contract support](/images/choosing-the-right-blockchain/coinmarketcap.png)
*Coinmarketcap top 20 blockchains with smart contract support.*

Beyond the top 20, the market cap and volume are pretty low, and so is the community. It can be risky to use anything that’s not in the top 20. 

## Popular blockchain platforms

### **Ethereum**
It's the mother of dApps and the first blockchain with smart contract capabilities. There is a massive community that includes many apps, but it suffers from two big issues: an expensive gas fee plus a lack of scalability. To address these issues but still benefit from the security and decentralization level provided by Ethereum, [L2 blockchain](https://ethereum.org/en/layer-2/) solutions were created, but more on that later.

![Ethereum NFT volumen](/images/choosing-the-right-blockchain/ethereum_volumen.png)

Looking at the most popular Ethereum NFT collections at [dappradar](https://dappradar.com/nft/collections/protocol/ethereum),  we observe a huge volume. This volume means a strong community, a lot of users in the ecosystem, and many successful projects. Ethereum network and its consensus mechanism are super reliable, which makes them ideal for expensive NFTs, making trading volume even higher.

### **Cardano**
Smart contract capability was added recently (mid-2021 approx.), and the dApp ecosystem and NFT community are not fully developed yet. As of today, I wouldn't recommend it for an NFT project. Cardano has a great team but was late to the smart contracts game.

### **Solana**
Solid [L1 blockchain](https://academy.binance.com/en/articles/what-is-layer-1-in-blockchain) with proprietary standards, smart contracts are written in C, C++, or Rust. It's super-fast, in theory, it supports up to 65k transactions per second and has a low-cost gas fee. Besides, it has an incredibly vibrant community and growing ecosystem.

![Solana NFT Volumen](/images/choosing-the-right-blockchain/solana_volumen.png)
*Solana volume is smaller than Ethereum.*

### **Avalanche**
I really like the fundamentals of Avalanche. It's an eco-friendly, relatively fast, EVM-compatible blockchain, which means you can easily migrate an Ethereum dApp and run it on an Avalanche network.

It's a great alternative to solve Ethereum’s scalability and high gas fees issues. Ethereum and Avalanche share most of their developer's tools, such as the Truffle and Solidity languages. Avalanche has its own crypto, **Avax**, whereas Ethereum's crypto is **Ether**.

Its ecosystem is growing fast but it’s not as big as Solana's or Polygon's ecosystems yet. 

![Avalanche NFT Volumen](/images/choosing-the-right-blockchain/avalanche_volumen.png)

### **Polygon**
Polygon is a popular Ethereum Layer 2 blockchain solution. It handles transactions off Ethereum while taking advantage of the robust decentralized security provided by Ethereum (layer 1). Polygon is EVM compatible and runs dApps on its own network, communicating regularly with Ethereum to save a bunch of transactions simultaneously, minimizing transaction time and gas fees.

![Polygon Volumen](/images/choosing-the-right-blockchain/polygon_volumen.png)

### **Other ecosystems**
There are also many other thrilling ecosystems I haven’t listed here but deserve attention nonetheless (such as [Tron](https://tron.network/),  [Algorand](https://www.algorand.com/), [flow](https://www.onflow.org/)). I’d advise you to take a look at them as some might be a good fit for your needs.

## **Types of NFT marketplaces**

NFT platforms have quickly evolved from nice digital art marketplaces to sophisticated play-to-earn (P2E) games. In this next section, I’ll cover three different NFT platform categories and the most suitable blockchain technology for each one.

Creativity around NFT platforms will continue to expand, leaving many use cases yet to be uncovered. For instance, Soulbound Tokens, which are essentially non-transferable NFTs, will open plenty of innovation opportunities in the ecosystem. 

### Just Collectible Art - Very low transactions count

Typically these NFT projects are high-priced NFTs of collectible art. Buyers speculate about the NFT’s future value, expecting to sell at a higher price. The artist and the art itself are crucial for the success of the project as well as a good marketing and launch strategy.

These NFT projects are relatively simple to develop. Mostly they just require a few smart contracts, if not only one. Minting and trading the NFTs are the only transactions. Mining is performed one time per NFT (to create it), while trading transactions are occasionally performed since the buyer is basically getting digital art.

L1 solutions like Ethereum could be a good choice. For these NFT platforms, Ethereum's gas fee is not a blocker, considering how sporadically users trade expensive NFT pieces. Also, Ethereum is super reliable due to its decentralization and proof of work consensus mechanism, making it ideal for "storing" valuable assets.

[Border Ape](https://boredapeyachtclub.com/), for instance, uses the Ethereum blockchain. With the current Ether price, a simple transaction of buying a Border Ape NFT costs approximately 160 USD. Considering the floor price of these NFTs is 91 ETH (~182,000 USD when writing this blog post), the purchase fee doesn't look so bad.

![Border Ape](/images/choosing-the-right-blockchain/border_ape.png)

[Crypto Punks](https://www.larvalabs.com/cryptopunks) and [Lazy Lions](https://www.lazylionsnft.com/) are other popular NFT marketplaces in this category deployed on Ethereum. 

### Staking + Brreeding mechanisms - Few transactions count

These marketplaces are pretty much the same as the former (in terms of mining and NFT trading) but with staking and breeding mechanisms. Here, the NFTs have some use besides their artistic aspects.

**NFT staking** is a way to earn passive income in the crypto ecosystem. It lets NFT holders lock their assets in DeFi platforms to receive rewards, all without the need to sell their NFT collections. Often this kind of platform also launches its own ERC 20 token (or analog for non-EVM compatible blockchains) and uses them to reward NFT holders. 

A common use case is buying an NFT, then staking it to earn custom tokens (ERC 20), to either buy more NFTs, do something in the ecosystem, or trade these earned tokens.

**NFT breeding**, as the name indicates, is the process of getting a new NFT from an existing NFT or a combination of two of them. Sometimes the process takes time, and the user must burn custom tokens (ERC 20) in order to produce a new NFT.

I won't get into the tokenomics of an NFT project, but this type of platform needs to carefully control the demand/supply balance to make sure the demand and the asset value rise over time. So creating new NFT from breeding should be controlled and performed according to the community's overall interest and growth to have a sustainable project.

One of the first projects to apply this mechanism was [CryptoKitties](https://www.cryptokitties.co/). An owner can combine two kitties' attributes to get a new one that mixes the parents' characteristics and visual style.

![cryptokitties](/images/choosing-the-right-blockchain/cryptokitties.png)

[Wizard & Dragons](https://wnd.game/) is another game that uses this kind of economic mechanism. It's a 100% on-chain, community-driven strategy game combining collectible utility-focused NFTs with DeFi mechanics. They initially used the Ethereum network but migrated to Polygon after some scalability issues and the expensive gas fee.

### Active gameplay - Huge transaction volume

Everything that the previous category provides, plus active gameplay (meaning the game requires player interaction as opposed to idle gameplay). These games have a blockchain connection, and players can buy, stake, and breed NFTs to use within the game. They can also spend coins (in the game) to gain some prizes or recognition.

These platforms need a super scalable solution and the cheapest gas fee to support thousands of users playing the game simultaneously (which strongly depends on the blockchain, NFTs, and other tokens).

Besides sending transactions to the blockchain, it needs to store (off or on-chain) all the user-generated data created during the game.

[Axeinfinity](https://axieinfinity.com/), for instance, has developed "his own blockchain," [Ronin Ethereum Sidechain](https://whitepaper.axieinfinity.com/technology/ronin-ethereum-sidechain), which is a proprietary blockchain, making it permissioned (developers cannot deploy dApps).

![axie infinity](/images/choosing-the-right-blockchain/axie_infinity.png)

 Trung, its CEO, said this about the future of Ronin:

> *“We are very excited about the possibilities Ronin brings. Though it’s still in an early state, Ronin will continuously evolve over the years to serve the spirit and ethos of blockchain gaming. On the technical side, we are also looking into various solutions to further strengthen and scale Ronin. zKSyncs, for example, is looking promising, but it could take time until it’s production-ready — particularly for NFTs and games.”*
> 

Another play-to-earn game, [God Unchained](https://godsunchained.com/), uses [Immutable X](https://www.immutable.com/), an L2 EVM-compatible blockchain created with P2E game requirements in mind. If you want to be part of their ecosystem, you need to get approved, so it's not totally permissionless either.

Besides these two, other interesting blockchains for play-to-earn games are [Solana](https://cryptodaily.io/best-solana-games/) and [Polygon](https://gamingnews.cyou/best-play-to-earn-games-at-polygon/). Here you can check what was built on Solana and Polygon regarding P2E games.

## Reviewing each blockchain's ecosystem

### Volume
We have already shown the volume for each blockchain we covered, with Ethereum having the most significant volume. But Ethereum's dominance in the NFT space is slowly crumbling. 

Solana and Polygon have similar trade volumes between each other, and although Avalanche has a lower volume, its ecosystem is growing fast.

![Avalanche’s NFT ecosystem keeps growing according to [https://avaxnftstats.com/](https://avaxnftstats.com/).](/images/choosing-the-right-blockchain/avalanche_nft_stats.png)
*According to [AvaxNftStats](https://avaxnftstats.com/), Avalanche’s NFT ecosystem keeps growing.*

Is having more volume important? It depends. Higher volume indicates an interesting ecosystem and many users, something everyone is looking at when launching a DApp. At the same time, maybe some blockchains whose ecosystem is growing fast but still don't have your NFT innovation may be willing to promote your NFT platform and help in the marketing strategy. In the end, both are pushing forward a blockchain ecosystem.


![Avalanche’s NFT ecosystem keeps growing according to [https://avaxnftstats.com/](https://avaxnftstats.com/).](/images/choosing-the-right-blockchain/avalanche_nft_stats.png)

### Transactions per second
Is TPS important? It depends on the NFT platform you want to build. If your NFT platform does not fall into the first category we covered previously (Very low transactions count), I would say yes.


![Transactions per Second).](/images/choosing-the-right-blockchain/transations-per-second.png)

Ethereum is not an option if you need high throughput, as the table above indicates. Notice that Ethereum is being [upgraded](https://ethereum.org/en/upgrades/) to improve scalability.

### Transaction finality
Finality guarantees that no one can alter, reverse or cancel crypto transactions once completed. Avalanche is the king with a transaction finality of fewer than two seconds in this subject.


![Transactions Finality).](/images/choosing-the-right-blockchain/transations-finality.png)


It's impressive how Avalanche can process up to 4500 transactions per second, with 2 sec. finality time and scale, even more, using subnets. It could be a great alternative if you need scalability, reliability, and a low gas fee. 

Transaction finality is vital to provide a great user experience in some apps. Imagine a DeFi app that needs to notify the user the transaction was confirmed and irreversible in the network. Avax can accomplish that in less than 2 seconds, thanks to its [consensus mechanism](https://docs.avax.network/overview/getting-started/avalanche-consensus/) and Snowball algorithm.

### By availability of DApp Engineers
Most blockchain developers are experts in EVM because Ethereum was the first blockchain with smart contract functionality. At the same time, EVM-compatible blockchains share most developer tools and developers can easily build dApps in any of them. So if your concern is getting the right team, EVM compatible blockchains such as Avalanche, Polygon, and Ethereum are better.

![EVM-compatible).](/images/choosing-the-right-blockchain/evm-compatible.png)

Also, EVM-compatible blockchains typically have better interoperability with Ethereum. For example, $MATIC, the Polygon native cryptocurrency, is an [ERC-20](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/) token in the Ethereum network. The [Avalanche Bridge (AB)](https://bridge.avax.network/) can be used to transfer ERC20 tokens from Ethereum to Avalanche's C-Chain and vice versa and so on.

### By NFT Marketplaces
You can either list an NFT collection in your own developed marketplace, use a third-party marketplace such as OpenSea, or even list NFTs on your own and in multiple third-party marketplaces.

OpenSea is the biggest NFTs marketplace but it only supports Polygon, Ethereum, and Solana NFTs for now.  Also, almost every blockchain has its marketplace supporting its own ecosystem projects. 

Why would you list your NFT on a third party? Simple, more people will find your NFT. And some crazy people still trust more on a third-party marketplace than on a real dApp. It’s important to do some research and explore potential marketplaces for listing your NFT. 

![[Open Sea](https://opensea.io/) is the largest marketplace according to trading volume.](/images/choosing-the-right-blockchain/open-sea.png)

[Open Sea](https://opensea.io/) is the largest marketplace according to trading volume.

## Final thoughts

The image below recapitulates each blockchain's characteristic and its advantages compared to each other (green means "best at", yellow means "good but not the best at")

![Smart contract blockchain comparison](/images/choosing-the-right-blockchain/blockchain-comparison.png)


If you have read so far, you would have a more deep understanding of the different NFT platforms as well as the characteristics of the most interesting blockchains to build them on, which one serves your needs better, and what to look at when selecting the best platform to work with.

In the end, the blockchain you choose will mostly depend on your NFT platform requirements. If you lack an experienced team or still feel lost or hesitating in which one fit best your requirements, please contact us and we gladly help you!

We’re always on beta! Let us know if you already have experience and have some blockchain you think is worth adding to the post. 
