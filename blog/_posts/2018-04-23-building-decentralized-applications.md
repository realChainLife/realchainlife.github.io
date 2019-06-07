---
comments: true
date: 2018-04-23 19:41:12
layout: post
slug: building-decentralized-applications
title: Building Decentralized Applications
categories:
- Decentralized Web
tag:
meta: "An introduction to building Dapps"
---

Decentralized applications (or Dapps) are server-less applications that run 
on a P2P network of computers rather than a single computer. They can be run 
jointly on the client side and within a blockchain based distributed network - 
although they don’t necessarily need to run on top of a blockchain network.

BitTorrent, Popcorn Time, BitMessage, Tor, are all traditional dApps that run 
on a P2P network, but not on a Blockchain (*which is a specific kind of P2P* 
*network*).

<figure>
  <img src="/blog/wp-content/uploads/2018/04/building-dapps-01.png" alt="">
    <figcaption>Blockchain & Decentralized Apps</figcaption>
</figure>

This post aims to cover:

* Features of a blockchain dApp;
* Ways of developing decentralized apps;
* Why decentralized apps are the future;
* Overview dApp development Platforms

Technically most of the Decentralised applications run on the principle of 
`smart contracts` with no centralized authority controlling the application. 
The apps contain real-world assets which can be used within the network.

## Features of a Decentralized Application

If you're going to build a dApp, there are some prominent features that I suggest 
be included by default. These features prove that programmable trust could power 
a `decentralized system` without the need for a central institution. These are the 
technological features that will power modern applications of all kinds:

1. **Censorship Resistance Apps** - As the number of countries engaged in 
  some form of censorship continues to increase YOY it will be important 
  that you create applications on a decentralized infrastructure with a 
  natural resistance to all forms of censorship.

2. **Resilience & Reliability** - The dApp logic and data should be replicated 
  across all the participating nodes on the networks using smart contracts.
  These replicated and distributed smart contracts will ensure fulltime
  availability and reliability for the dApp.

3. **Auditability & transparency** - With the integrated smart contracts,
   users can verify the code implementing the business logic. This provides
   additional transparency and verifiable trust model to dApps.

4. **Better Business Model** - For Web decentralization to work, we need to 
  develop commercialization models that are not only user friendly but also
  provided better mechanism designs and digital assets - these will cultivate
  a better internet.

5. **Cryptographic Key Management** - Because the production of digital assets
   go hand-in-hand with protection, dApps need to incorporate asymmetric 
   encryption systems for the user credential management policy. This creates a 
   very sparse and challenging attack surface. A hacker now has to breach each 
   user individually.

Using Dapps, we can design platforms that are fully decentralized and give more control 
to users. There are very few mobile app developers out there who understand the nitty 
gritty of developing a decentralized app. Though blockchain enthusiasts have definitely 
increased over the past few years, there is still a deficiency of expert decentralized 
app developers.

Regardless of where you fall on the developer skill level, anyone can try out a few 
methods to developing dApps that can be compiled into an easy-to-follow guide.

## Developing Decentralized Apps

Before we get started with key steps involved in the developing, building and 
deploying of decentralized applications its important to remind ourselves that 
this field is constantly evolving and that it is always a good idea to keep 
refreshing your knowledge on the subject.

### Development Step I: Defining Your Environment

Deciding which blockchain environment would best fit a business creates a headache 
formany companies and developers. Due to the fragmented nature of the industry, 
technology implemented by some companies faces many risks including `obsoletion`, 
`insecurity`, `cost-inefficieny` and so on. 

To avoid the pains associated with poor matching of a solution to technology, 
developers need to determine the type of technology required for each area of 
development i.e.

  * Database Management
  * APIs
  * Development Servers
  * Hosting
  * Frameworks
  * Programming Language
  * & Frontend

Each technology choice contributes to the final efficiency, usability and 
commercialibilty of the dApp and thus its can be called a critical factor of 
dApp development.

### Development Step II: Set Up Development Framework

Dependent on the technology you've chosen to work with, we will proceed to 
installing the development framework, dependancies and evironment needed to 
start working on the codebase and business logic for the smart contracts.

There are two development frameworks that are most common and available for 
developers to select from:

  * ***Platform Apps*** - These are suitable for developers new to 
  decentralized app building. Platforms like Hyperledger, Ethereum 
  or Azure provide easy to follow steps to deploying application most 
  of them requiring developers to only write a smart contract that is 
  deployed on the network through a series of automatic functions.

  * ***Software Apps*** - With this approach, developers can leverage 
  pre-exiting softwares to build new sofwares or dApps that provide a 
  specific suitable solution to existing network problems. AN example 
  is the Lightning Network build on Bitcoin to solve the problem of 
  high-cost transactions.

Based on the framework of choice, you'll need to set up all the tools you will 
need for the end-to-end development and deployment of the app. Every framework 
provides an easy to work with development platform including Truffle on Ethereum. 

### Development Step III: Code The Application

The core of any decentralized application is the business logic written into
its smart contract. Though it might feel a little counterproductive for a new
learning curve to be indroduced to something as basic as a programming language,
that's excatly what happens with some blockchain networks. 

As a developer of a dApp, you'll need to learn & adopt to each development platform's
`standard` for writing smart contracts. On **Ethereum** for example, smart contracts 
are written in specific new language, [solidity](https://solidity.readthedocs.io/en/v0.5.9/) 
and deployed through a special editor **Remix**. On **Hyperledger** smart contracts
are referred to as [Chaincode](https://hyperledger-fabric.readthedocs.io/en/release-1.4/chaincode4ade.html) 
and work with [Chaincoder](https://www.chaincoder.org) an interactive tool for rapid 
development, creation and deployment of applications on Hyperledger Fabric. 

In this example, we have two solutions that have addressed the issue of programming
language differently. Chaincode is implementable in `Go`, `node.js` or `java` - 
already common languages but Ethereum requires you to learn the the language
from scratch. This should be considered in while choosing the preferred development
environment. 

Here, you should also consider your `Frontend UI` options and include the design and
development process in the entire coding phase. This will be important for the dApp
tests that will be done in the next step. 

### Development Step IV: Deploy & Test Application

Before we can launch and start using our application in the last step we need to 
deploy and test what you've developed. For majority of platform applications this
step is as simple as:

1. Uploading the configuration files and smart contracts
2. Adding network participants
3. Running test transactions

It is worth noting that any deployed smart contract code will be unalterable and 
forever stored on the blockchain. For this reason, you should know before beginning
all the `variables` that will be testnet for various function performance tracking. 

### Development Step V: Launch The App

This can be the most exciting and daunting phase of the entire development process.
Exciting because the fruit of your hardwork is seemingly ready to be shared with 
the world - daunting because any mistakes in the development of the application
can lead to un-usability of the dApp. 

Once your app has been tested you will be ready to launch it. Choose a custom domain 
for the application and let everyone know it is up and ready. Keep in mind that this 
will be the most intensive part of your marketing strategy and you should keep up the 
same level of hard work and diligence that lead to you creating a great app in the 
first place.

## Decentralized Apps of The Future

Time and time again I have mentioned the importance of the `Decentralized Web`
and the role decentralized applications will play in the mainstream adoption
of decentralized and distributed systems. 

<figure>
  <img src="/blog/wp-content/uploads/2018/04/building-dapps-02.png" alt="">
    <figcaption>Illustration: Decentralized Application</figcaption>
</figure>

A major challenge we face with the current client/server models we use on our
applications gives hackers a single point at which to orchestrate attacks. This 
failure has resulted in massive data breaches which have not only cost huge sums 
of money, but have also dented customer trust as well. Decentralization prevents 
these kinds of attacks because there is no one point of failure.

The decentralized application will be held to the same criteria of decentralized
applications in development today:

  * **Distributed Ledger** - Application’s data and records of operation 
    must be cryptographically stored in a public, decentralized blockchain 
    in order to avoid any central points of failure.

  * **Generate Tokens** - Application must generate tokens according to a 
    standard cryptographic algorithm acting as a proof of the value, for
    example Bitcoin uses the Proof of Work Algorithm to generate more BTC.

  * **Open Source** - Application must operate autonomously, and with no 
    entity controlling the majority of its tokens - the consensus of its 
    users must decide all changes.

dAapps act as an enabler for new kinds of applications providing decentralized 
scalability, strong security, resilience, and availability. By building on the 
current technical solutions we will offer significant control to end-users on 
their credentials, data, and communications and hence will create a major shift, 
particularly in consumer applications.

## Overview: Decentralized Application Platforms

As I've mentioned sparsely in the steps to developing, deploying and launching
a decentralized applications, `platform apps` offer various easy solutions to 
dApp development. 

In this last segment I want to hightlight, briefly, some of my favorite platforms
to work with for smart contract deployment: 

1. **[Liquid Network](https://blockstream.com/liquid/)** - This Bitcoin 
   sidechain was announced by Blockstream in 2016 and is set for release
   later this year, will provide participants various benefits including 
   *rapid transfers*, *issued assets* & *streamlined development*.

2. **[Ethereum](https:ethereum.org)** - Perhaps the most popular dApp
   platform, Ethereum provides users with multiple tools like Truffle,
   Web3, Remix and more to facilitate the creation and deployment of 
   smart contracts. Learning **Solidity** is easy as well which is a 
   very welcome addition to the ease-of-use of Ethereum.

***Platforms To Watch***:

This list although not exhaustive covers the platform that are currently
developing solutions that I think will contribute greatly to how we 
write and deploy decentralized applications:

  * IPFS,
  * Vechain Thor,
  * Waves Platform &
  * Steem

This is my personal list, if yours is different from mine leave a comment
with the list and why that's your selection. Also, what's would the most 
vital feature of your decentralized application?
