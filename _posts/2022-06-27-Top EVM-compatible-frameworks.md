---
title: "Top EVM-compatible frameworks to build dApps - Truffle vs Hardhat"
layout: post
permalink: /blog/best-blockchain-development-framework/ 
date: '2022-06-28T10:00:00.000-03:00' 
category: development
tags:
  - DApp Frameworks
  - Truffle
  - Hardhat
author_id: mtnBarreto
author: Martin Barreto
show: true
featured_image: /images/evm-compatible-frameworks/TopEVM-compatible-frameworks-to-build-dApps-Truffle-vs-Hardhat.png
---

Web3.0 space is exploding right now. There's an unprecedented demand for blockchain developers to build the next revolutionary dApp. But for those giving their first steps in the field, choosing a framework from all those available can be overwhelming.

In addition, building a well-developed dApp requires solid computer science skills, dealing with different technologies, handling several environments, setting up a testing library, deploying smart contracts, forking the chain, and integrating plug-ins (among other things).

**The question is... which framework should I use?** There are too many smart contract development frameworks, and it's hard to have real development experience with all of them.

In this blog post, I'll list two popular frameworks for building EVM-compatible dApps. I'll also share some valuable tools to speed up your dApp building time even more. Let's get into it!

# What’s a dApp Framework?

Smart contract frameworks are software development platforms to develop, compile, test, and deploy decentralized applications (dApps). Using a framework, you can build a simple dApp in a matter of minutes while ensuring the usage of best practices and tools, and mitigating significant risks around dApp development.

## What dApp Frameworks have to offer

- The ability to run a local blockchain node for testing and development purposes.
- Tools to compile your solidity code to bytecode.
- A testing framework.
- Multiple environments. Connection to local development, Testnet, and Mainnet networks to deploy, test, and debug smart contracts.
- DApp end-to-end development tools to develop both the blockchain and client-side functionality (frontend framework, web3.js helpers, and base code).
- Easy integration with IPFS (decentralized storage) to store large files off-chain.
- Tooling for verifying and publishing smart contracts source code.

## What happens if you don't want to use a framework?

Well, you could still develop dApps from scratch (without the set of tools that a framework provides). Still, you'll have to handle a bunch of complexity, create a lot of boilerplate code, integrate tools, add-ons, configuration files, set up testing frameworks, and so on.

If you want to save time and have fun, you should use a framework.

## Main challenges when developing dApps

- It’s challenging to manage and fix problems in decentralized systems once they're deployed.
- The lack of proper development and testing tools increases programming errors significantly.
- Security risks: There's real money involved, smart contracts code mints, trades and burns tokens, and your app is exposed to hacks and attacks.
- Manage multiple environments, upgrade dApp and blockchain forks.

# Frameworks to build EVM dApps

## Truffle

Probably the most popular framework. Initially created for Ethereum, you can develop any EVM-compatible dApp using it. Almost every EVM-compatible blockchain (Avalanche, Ethereum, Polygon, etc.) tutorial uses [Truffle](https://trufflesuite.com/) to guide you through each step of building a dApp.

Truffle provides a suite of tools and solves every major dApp development challenge. It’s internally written in javascript, and you can easily install it using npm (node package manager) by executing `npm install -g truffle`*.*

**Project structure**

Once you install Truffle, you can create a new Ethereum project by running `truffle init`. It will make the project structure and base project files within the current folder, but it won't contain any smart contracts.

> Alternatively, you can use `truffle unbox <box-name>`  to initialize the base template that contains actual dApp functionality (more on that later). As you can see, Truffle offers many command-line commands to perform tasks. For instance, `truffle compile` compiles your smart contracts into their bytecode.
> 

![Truffle project’s folder structure](/images/evm-compatible-frameworks/poject-structure.png)
*Truffle project’s folder structure*

- **contracts:** directory for smart contract files.
- **migrations:** directory for deployment scripts.
- **test:** directory for testing files.
- **truffle-config.js:** framework and project configuration file.

**Testing**

Testing dApps is super important since once you deploy the smart contracts, it’s impossible to change the code.

In Truffle, you can write test code in solidity or javascript (Mocha.js testing framework). `truffle test` runs tests using the chosen framework. Every time you run the tests using Truffle, a local development blockchain (Ganache) gets started to run on this fresh local development node.

**Local development blockchain**

Truffle provides a local development blockchain for testing and debugging proposes.

`truffle develop` lets you work with smart contracts interactively. It runs a [ganache](https://trufflesuite.com/ganache/) instance and attaches the console to the environment.

![`truffle develop` terminal output](/images/evm-compatible-frameworks/truffle-develop.png)
*`truffle develop` terminal output*

As seen in the image above, it automatically provides ten blockchain accounts and their corresponding private keys so you can play interactively with the blockchain network.

Once you execute the command, you'll immediately see the following prompt:

```jsx
truffle(development)>
```

`truffle console -network <name>` it’s pretty much the same as the last command but with some significant differences. It won't run the local development node nor provide specific accounts and private keys. But it allows connecting to any other network such as testnet and mainnet. 

You can execute `migrate —reset` to deploy de contracts on the connected network. 

![migrate -reset.png](/images/evm-compatible-frameworks/migrate_-reset.png)

Using an interactive console is super helpful to debug the app accordingly in different environments. For instance, you can quickly get the transaction hash and receipt to look up the transaction log in the real distributed blockchain (you can see the log for Avalanche and Binance Smart Chain at [https://testnet.snowtrace.io/](https://testnet.snowtrace.io/) and [https://testnet.bscscan.com/](https://testnet.bscscan.com/) respectively).

This section aims to give you a sense of how simple it is to create and interact with smart contracts using a framework like Truffle. You can visit the [official Truffle documentation](https://trufflesuite.com/docs/truffle/getting-started/using-truffle-develop-and-the-console/) for more information on how to interact with contracts.

> Suppose your dApp needs third-party services (other dApps). In that case, you can set up the configuration to fork the necessary blockchain chain and have those services available on the local development node.

### Most **essential** tools in truffle

[Ganache:](https://trufflesuite.com/ganache/) An open-source personal blockchain to develop, test, and debug your dApp without spending actual gas fees. Ganache UI is super helpful to test dApp for confidence before deployment. 

![Gatache UI](/images/evm-compatible-frameworks/ganache-window.png)
*Gatache UI*

Using Ganache, you can track blockchain account status such as transactions, addresses, keys, balance, etc. Ganache provides many other helpers, simulating mining, blockchain activity log output, and a rich UI to explore blockchain blocks.

**[Truffle Boxes:](https://trufflesuite.com/boxes/)**

Boxes are just helpful boilerplates. Some of them are project scaffolds (templates), so you can quickly start your project using the best tooling and practices and focus on your dApp functionality. All boxes created by the community are listed [on their website](https://trufflesuite.com/boxes/). 

`truffle unbox <box_name>` download a box to the current directory.

**[Truffle drizzle:](https://trufflesuite.com/drizzle/)**

A collection of libraries to quickly develop dApp user interfaces. It will feel familiar if you have developed frontends with react and redux. Drizzle provides a redux state for contracts, addresses, transactions, and events, so it’s easy to interact and sync the UI components according to the dApp state.

If you don't know where to start when it comes to developing the dApp user interface and interacting with the smart contract from a frontend, I strongly recommend you take a look at [drizzle](https://trufflesuite.com/drizzle/). Many boxes already provide the frontend code, many of which use drizzle as the main library.

## Hardhat

**[Hardhat](https://hardhat.org/)** is another popular smart contract development framework for Ethereum and EVM-compatible blockchains which shares many similarities with Truffle, although with a fair share of differences.

Regarding what you can do with Hardhat, it’s pretty much the same as Truffle, so I won't go deeper on that as we did with Truffle, but I will focus on the main implementation differences and reasons to use one over the other.

Hardhat, like Truffle, is written in javascript, so you only need to have a node.js environment to install it.

### Popularity

Truffle was the first framework for smart contracts development, but Hardhat has gained broad popularity (check out npm weekly installation chart in the images below).

<table>
 <tr>
    <td>
      <figure>
        <img src="/images/evm-compatible-frameworks/truffle-adoption.png" /> 
        <figcaption>Weekly download for truffle is pretty stable and in a downtrend.</figcaption>
      </figure>
    </td>
    <td>
      <figure>
        <img src="/images/evm-compatible-frameworks/hardhat-adoption.png" /> 
        <figcaption>Weekly download for hardhat is growing since its release.</figcaption>
      </figure>
    </td>
  </tr>
</table>

**Does this mean something?** Well, it shows some developer preference for HardHat over Truffle. Something important to consider because once you develop a dApp using one framework it’s hard to migrate to another. Also, the Hardhat downloads uptrend looks like it will continue.

### The biggest difference between Hardhat and Truffle.

**Testing capabilities and local development blockchain**

Like Truffle, Hardhat also provides a local development blockchain for testing, which is its default network called [Hardhat Network](https://hardhat.org/getting-started#connecting-a-wallet-or-dapp-to-hardhat-network). Unlike Truffle, Hardhat does not provide a UI for the local development network that comes out of the box. We just have a CLI (command-line interface) version of a [local development blockchain](https://hardhat.org/getting-started#connecting-a-wallet-or-dapp-to-hardhat-network) to develop, test, and debug the dAdd before deploying it to the mainnet.

**Is it better to have the UI?** Again, it depends on the developer's preferences. Some developers feel more comfortable having a UI that shows blockchain information like accounts, transactions, and so on in real-time; instead of having to execute CLI commands to get this information.

> BTW, Hardhat developers can also use Ganache and its UI, but it’s not the default configuration.

**Debugging capabilities**

The main difference with Truffle is the solidity `console.log` which allows printing log information at any point of the smart contract when running on Hardhat Network. Whether you are running tests or interacting with the development network doesn't matter. This is super important (especially for complex dApps) since most developers are familiar with using these debugging capabilities in traditional applications. Still, smart contract development works differently, in a more atomic way, when developers can execute transactions and get results. Still, getting information within the smart contract execution process is complex.

```jsx
pragma solidity ^0.6.0;

import "hardhat/console.sol";

contract Token  {

	function transfer(address to, uint256 amount) external {
	    console.log("Sender balance is %s tokens", balances[msg.sender]);
	    console.log("Trying to send %s tokens to %s", amount, to);
	
	    require(balances[msg.sender] >= amount, "Not enough tokens");
	
	    balances[msg.sender] -= amount;
	    balances[to] += amount;
	}

}
```


The login information is shown when tests are executed. Nice right?

```jsx
$ npx hardhat test

  Token contract
    Deployment
      ✓ Should set the right owner
      ✓ Should assign the total supply of tokens to the owner
    Transactions
**Sender balance is 1000 tokens
Trying to send 50 tokens to 0xead9c93b79ae7c1591b1fb5323bd777e86e150d4
Sender balance is 50 tokens
Trying to send 50 tokens to 0xe5904695748fe4a84b40b3fc79de2277660bd1d3**
      ✓ Should transfer tokens between accounts (373ms)
      ✓ Should fail if sender doesn’t have enough tokens
**Sender balance is 1000 tokens
Trying to send 100 tokens to 0xead9c93b79ae7c1591b1fb5323bd777e86e150d4
Sender balance is 900 tokens
Trying to send 100 tokens to 0xe5904695748fe4a84b40b3fc79de2277660bd1d3**
      ✓ Should update balances after transfers (187ms)

  5 passing (2s)
```

Truffle has been improving its [debugging capabilities](https://trufflesuite.com/docs/truffle/getting-started/using-the-truffle-debugger/) to provide similar features.

**Documentation**

In my opinion, Truffle's documentation looks clearer, more organized, and more detailed. I guess this advantage exists because Truffle has had more time in the market. Still, I have to say Truffle doc is some steps ahead of Hardhat, and most EVM-compatible platforms use Truffle as the default framework in tutorials.

**Opinioned vs. unopinionated framework**

Regardless of the tools you end up using in your project; Hardhat is more flexible (unopinionated) than Truffle. Of course, both come with build-in default tooling, but with Hardhat, you can easily override the out-of-the-box configuration to your favorite plug-ins and tooling set.

For instance, in Hardhat, you can use our favorite libraries for testing, such as Waffle, ether.js, chai, and mocha, or any other combination. Hardhat is super flexible when it comes to compound and select plug-ins, libraries, and tools; much more flexible than Truffle.

Let’s get into some examples to clarify that.

**Using web3.js vs. ether.js:** Truffle uses web3.js by default; Hardhat is more plug-in oriented by default and it’s easy to switch from web3.js to ether.js, whereas in Truffle, this could be more tricky.

**Migrations folder in Truffle vs. Scripting folder to interact with blockchain in Hardhat.**

To deploy a smart contract in Truffle, we must add a migration file to the migrations folder. In contrast, in Hardhat, there is a script js file where we can add any needed script to interact and deploy to networks (deployment scripts work like any other script).

Is this flexibility good or bad? It depends on the developer's preference. Personally, I leave the configuration as it comes out of the box, but at the same time, I like some level of flexibility to tweak things (when the requirements force me to do so).

 

## **Additional tools typically used along with dApp frameworks**

### **[OpenZepplin](https://openzeppelin.com/)**

OpenZeppelin provides a set of tools and smart contracts to security build, automate, and operate decentralized applications.

As I have already mentioned, it’s super hard to fix security and functional issues after deployment. Using audited, well-written base code minimizes those risks and speeds up development time. OpenZepplin provides modular, reusable, and secure smart contract implementations for ERC standards. It also includes helper libraries such as [Math](https://docs.openzeppelin.com/contracts/2.x/api/math) to wrap Solidity arithmetic operations which makes your code more secure (avoiding overflows and so on).

> Just in case, there are some tricks to upgrade a dApp by using a smart contract proxy and delegating implementation to another smart contract. This way, we can change the contract code while preserving the state, balance, and address of the dApp.
> 

OpenZeppelin Defender (another product) is an automated tool to ship and manage smart contracts after deployment. Read more on their [site](https://www.openzeppelin.com/defender).

Most popular NFT and Defi EVM-compatible platforms trust OpenZeppelin, and I strongly recommend it if you are building something that matters.

### [Figment.io](https://www.figment.io/) Datahubs

Figment’s development platform, DataHub, allows developers to use the most powerful and unique blockchain features without becoming protocol experts.

With DataHub, developers now have access to Web 3 protocols through the **[enterprise-grade infrastructure](https://learn.datahub.figment.io/guides/datahub-infrastructure)**.  They provide reliable access to the RPC and REST APIs of supported protocols for both the latest mainnets and testnets so developers can test and implement their products safely.

![datahub.png](/images/evm-compatible-frameworks/datahub.png)
 *Datahubs hi-level architecture wrapping popular EVM-compatible protocols.*

### [Alchemy](https://www.alchemy.com/)

Alchemy platform has some similarities with Figment in regards with infrastructure provided and services to develop complex dApps like analytics, performance monitoring and webhooks to get notified about on-chain events. 

### [Remix](https://remix-project.org/)

A "no-setup" browser and desktop app to develop and learn Ethereum smart contracts. They provide an online IDE super interesting to learn and play with EVM-compatible smart contracts. 

## Final Thoughts

We have seen two of the most popular frameworks for building dApps. Are there more frameworks?

[For sure](https://ethereum.org/en/developers/docs/frameworks/). But I don't recommend anything other than Truffle or Hardhat, especially if you take EVM-compatible dApp development seriously. You would have to learn Javascript, Solidity, and several other tools, but it's well worth it. As I said, framework selection is critical, and you must evaluate both.

**So the question is Truffle or Hardhat? Which one is definitely the best framework?** 

That's hard to answer. It depends on your personal preferences, what you value the most, and how you like to do things.

Do you prefer opinionated or unopinionated frameworks? Does Hardhat's growth trend mean something to you? Do you want to have more flexibility with the plug-ins and tools? Do you value having a local development blockchain with a UI where you can see balances, addresses, and transaction information without using the CLI? How much do you need to fork features to the local development node?

I feel comfortable with Truffle; it was the first framework I learned. Still, I have been progressively switching over to Hardhat to get comfortable, feel its developer experience and be able to compare both. I think I will continue using Hardhat for the dApps to come. Although I use the out-of-the-box configuration, I like to have the ability to tweak things according to app requirements and my personal developer preferences. Also, the market trend of Hardhat means something to me; somehow, Hardhat adoption is growing faster than Truffle, at least according to npm installation metrics.

I would say you'll do well with any of them. Both do their job, both are solid frameworks and provide almost the same capabilities to develop dApps, and both are getting a lot better over time. Just some things are more easily on Truffle while others are on HardHat. So, if you have time, play with both and decide for yourself.

That being said, sometimes the project you jump into is already using Truffle or Hardhat (because you are a freelancer or you are running an agency), and choosing one is not an option. If this is the case, invest time learning both.