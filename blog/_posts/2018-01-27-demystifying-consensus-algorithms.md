---
layout: post
title: "Demystifying Consensus Algorithms"
date: 2018-01-27 21:41:11
categories: Consensus Algorithms
meta: "Go beyond the fancy titles and understand how voting mechanisms work"
---

One of my absolute all time favourite topics to write about, **Consensus Algorithms**
Before diving into the definitions, types and differences between each consensus
algorithm, we need to know more about the technology that these scripts are written 
for and function within i.e. **blockchain technology**. 

`Blockchain` is an open, distributed ledger that can record transactions between 
two parties efficiently and in a verifiable and permanent way. Generally it is a 
system for maintaining distributed ledgers by using peer-to-peer protocols. 
Blockchain enables real-time transactions and securely shares tamper-proof data 
across a trusted business network. 

<figure>
  <img src="/blog/wp-content/uploads/2017/03/commit-message-small.png" alt="" />
  <figcaption>Source: Oracle</figcaption>
</figure>

No consensus algorithm is perfect, they all have their pros and cons and for blockchain
networks, one of the major functions of a consensus algorithm is to prevent double
spend; another is to store transaction data in distributed ledgers. Depending on 
the algorithm - a network can build either a `permissioned` or `permissionless` 
distributed ledger. 

* **Permissioned** networks are closed ecosystems where validators are vetted 
  and selected by the network owner. This include *Hyperledger* and *Corda*.

* **Permissionless** networks allow anyone with the computational resources 
  to read the chain and write new blocks according to the consensus rules. 
  It's also known by its widest description as a public blockchain and its
  what we'll be covering alot of today. 

Before we can delve into each of the algorithms we need to understand some
of the base functionalities and mechanisms of these consensus algorithms.
For instance to ensure transaction validation, protocols need to follow
a simple three-step process of `endorsing`, `ordering` and `validating`
transactions. 

Because blockchain is a decentralized peer-to-peer network - participants 
(developers, miners, exchanges, users) need a decision-making model that
is not only open or logical, it needs to be fair and balanced. This
model is what is referred to as a consensus `mechanism`.

It usually covers 6 critical participant agreements on: **collaboration**,
**co-operation**, **equal-rights**, **participation** and **activity**. All
these will be covered in detail as we go through each algorithm starting
here with `Proof-Of-Work`. 

## Proof-Of-Work (PoW) Algorithm

PoW or as commonly referred, the `Bitcoin algorithm`, works on a technological
principle that requires all nodes (*miners*) to confirm all of their transactions 
and produce relevant blocks to the network chain. New blocks come with a Hash 
Function, and the hash function of the previous block. This provides the 
network an added layer of protection and prevents any type of violations. 

In proof of work, miners compete to add the next block (a set of transactions)
in the chain by racing to solve a extremely difficult cryptographic puzzle. 
Once a miner solves the puzzle, a new block gets created, and the transaction 
is confirmed.

Other cryptocurrencies such as Litecoin have adopted this model for their 
network and although a masterpiece in its own right, proof of work isn't
quite perfect.


### Where The Proof of Work Consensus Algorithm Falls Short

Far from what we can assume was Satoshi Nakamoto's vision, Bitcoin today has
evolved into a `datacenter-hosted style mining operation`. This is because of 
the high computational power required to solve cryptographic puzzles during
the creation of new blocks. As a result people and organizations that can 
afford faster and more powerful `ASICs` usually have better chances of mining 
than the others.

While environmentalists argue that this level of energy consumptions is killing 
the planet as its slowing the migration to other sources of energy - the PoW
model is getting more `energy-efficient` as a result of technological innovation. 
Therefore, the energy consumption of bitcoin will only improve with time.

Another challenge that has been noted as a result of the high computational 
resource requirement is the `centralization of miners` i.e. a small pool of
miners controling a large part of the network. Although it might seem this way,
bitcoin is used by millions across the world - and any changes to the network
will not be implementated as easily as it's often thought. It is also extremely
costly to implement changes on the network.

## Proof-Of-Stake (PoS) Algorithm

PoS is a new type of concept where every individual can mine or even validate 
new blocks only based on their coin possession. A user with a specific amount 
of coins stored previously in the wallet qualify to be a node on the network.

To qualify to be a miner users are required to deposit a certain amount of coin, 
after a vote is held to choose the network validators. At the end the miners 
stake the minimum amount required for the special wallet staking.

The tedious solving of cryptographic puzzles in PoW is replaced with a block
validation process that starts off with validators identifying blocks which 
they think will be added to the chain. They validate these block by placing
a `bet` on it. For every block staked, validators receive a reward proportionate 
to their `bets` for example a 10% stake is rewarded by validating 10% of new blocks.

The major grep with this consensus algorithm is due to its seemingly `minimal`
requirements for validator roles - What is to discourage validators from creating 
two blocks and claiming two sets of transaction fees? And what is to discourage
a signer from signing both of those blocks? This has been called the 
`'nothing-at-stake'` problem and its yet to be addressed by common users of the
algorithm including Ethereum (which recently made the switch from PoW) or PIVX.

## Proof-Of-Authority (PoA) Algorithm

PoA was proposed by a group of developers in March 2017, and was first released as
new network named Kovan a primary test network available on Ethereum. Since its
release its been optimized and used a core governance model on new networks like
`VechainThor`. 

This model leverages identity as the form of stake where validators are pre-approved 
to validate transactions and blocks within the respective network. Originally it was
thought it worked best with a small number of validators (`less ~25`) but on Vechain
they increased the number of `Authority Masternodes` to 101. 

Like other consensus algorithms designed after PoW, PoA networks run on low requirement 
of computational power, no requirement of communication between nodes to reach consensus, 
and continuity of the network is independent of the number of the available nodes since 
they are pre-approved and verifiably trustable through cross verification.

These characteristics feed into the fairly obvious advantages of the PoA algorithm. PoA
based networks enjoy increased efficiency in transaction times and overall network 
consensus. This model is also much more effective with decentralized applications
and is easily scalable compared to other decentralized networks. 

## Delegated Proof-Of-Stake (DPoS) Algorithm

Developed by [Daniel Larimer](https://bytemaster.github.io/) for use in the EOS network 
token hodlers don’t vote on the validity of the blocks themselves, but vote to elect 
delegates to do the validation on their behalf. 

The system is quite robust and adds a different form of flexibility to the whole equation.
By replacing miners or validators with delegates this system of block production ensures 
all levels of protection aganist regulatory problems. Blocks can also be produced at a
fraction of time significantly smaller that PoW networks. 

The partial centralized nature of this type of network is a major drawback for some users 
of decentralized systems.

## Practical Byzantine Fault Tolerance (PBFT) Algorithm

PBFT was made famous for it use in the `Hyperledger`, `Stellar` and `Ripple`
blockchains. It was designed as a solution to a problem presented by the
previous use of BGP (*Byzantine Generals Problem*). The algorithm is designed for 
asynchronous consensus where all the nodes inside the system get arranged 
in a specific order. One node is selected as the primary one, and others 
work as the backup plan. However, all the nodes inside the system work 
in harmony and communicate with one another.

### PBFT & The Hyperledger Blockchain

PBFT algorithms share some interesting facts with us. I will write an in-depth
article on how Hyperledger uses PBFT to run the network but for the moment I 
will highlight some of the benefits associated with PBFT and why it was the 
algorithm of choice for Hyperledger:

  * ***Block Transaction Confirmation***
    PBFT uses a system of checks and balances during the lifecycle of a 
    transaction including the usage of endorsement policies to dictate 
    the members that must endorse a certain transaction class. Once 
    nodes agree on a specific block, it gets finalized. This is due to 
    the fact that, all the authentic nodes communicate with each other 
    and come to an understanding of the specific block.

  * ***Higher Transaction Throughput***
    Hyperledger requires all participants to be authenticated, due to 
    its permissioned implementation nature, as a result, the network 
    tends to provide higher transaction throughput rates and performance.

  * ***Reduction in Energy Consumption***
    The PBFT algorithm offers a good amount of reduction in consumption 
    of power than PoW. This is because not every miner is solving the 
    typical hashing algorithmic puzzles. That’s why the system doesn’t 
    require high computational resources.

One of my major drawbacks from PBFT, despite some of it's advantages and 
promising facts is its `communication gap`. Nodes running the PBFT algorithm
are required to make sure that the information they gather is solid. This forcibly
limits how many nodes can run on the network to retain a high quality communication
between them.  

## Directed Acyclic Graphs (DAGs) Algorithm

Commonly known as the Blockchain Killers, DAGs are used in several blockchain
networks including IOTA, Hashgraph and Nano. Its also integrated in non-blockchain
networks like `IPFS`. 

<figure>
  <img src="/blog/wp-content/uploads/2017/03/commit-message.png" alt="" />
  <figcaption>Source: Hackernoon</figcaption>
</figure>

Although I've listed it as a consensus algorithm, DAG is basically a form of data 
structure that *theoretically* handles infinite transactions per second mostly 
asynchronously. **Tangle** the DAG consensus algorithm used by Iota requires each
node to validate two previous transactions before sending one on the network. This
two-for-one consensus strenghens the validity of transactions the more transactions
are added to the network.

Nodes on **Hashgraph** on the other hand, share their known transactions with other
nodes at random until eventually all the transactions are `gossiped` around to all of 
the network nodes. At 250,000+ transactions per second it is one of the fastest 
networks which makes it a great option for private networks. Despite its advantages
Hashgraph is still susceptible to [sybil attacks](https://en.wikipedia.org/wiki/Sybil_attack).

## Conclusion

Consensus algorithms make blockchain networks versatile and while there is no 
one perfect algorithm to implement the field is still wide open to innovation 
by creating variations of these implementations as well as new approaches to 
them. My brief write up covers what I've considered the most dominant in the 
market. 

The whole idea of the blockchain technology is decentralization and a fight 
against service centralization. I am eagerly waiting for the development of 
better and better consensus algorithms that will address issues like the
handling of potential attacks with ease. Join our consensus-building community 
if you're keen on developing the decentralized world further.

- - -

<small> ***Disclaimer***: The information is subject to my own opinion. Please 
do your `very own` market research before making any investment in cryptocurrencies.
Any financial loss caused as a result of this writing will be attributed to 
you alone. </small>

