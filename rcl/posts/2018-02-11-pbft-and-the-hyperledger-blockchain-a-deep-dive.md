---
comments: true
date: 2018-02-11 23:06:10
layout: post
slug: pbft-and-the-hyperledger-blockchain-a-deep-dive
title: 'A Deep Dive: PBFT and The Hyperledger Blockchain'
wordpress_id: 306
categories:
- Hyperledger
tag:
- PBFT
- Hyperledger
- Consensus Mechanism
---

Blockchain networks are designed as peer-to-peer systems that don’t have 
centralized authority points to function but for the decentralized infrastructure
to exist and work, they need an in-built decision-making feature commonly 
known as `consensus`. When implemented, consensus algorithms allow every 
member of the network to partcipate in the blockchain development by making 
decisions on the network's future. 

In my previous post, [Demystifying Consensus Algorithms](https://realchainlife.github.io/blog/2018/01/demystifying-consensus-algorithms/), we delved into the various consensus
algorithms discussing some base functionalities and mechanisms of these 
consensus algorithms. We highlighted certain benefits of the Practical 
Byzantine Fault Tolerance (PBFT) Algorithm and why it was the algorithm 
of choice for the Hyperledger Blockchain. 

In this post we will answer the question, what is practical Byzantine 
Fault Tolerance as a complete beginner's guide. We'll cover it orgins, 
how it differs from other algorithms and why its used on the Hyperledger
and other Blockchain solutions.

## Evolution of Byzantine Fault Tolerance

Practical Byzantine Fault Tolerance is a consensus algorithm introduced 
in the late 90s as a solution to a problem presented by the previous use 
of BGP (*Byzantine Generals Problem*). pBFT was designed after extensive
research and has been optimized with a diverse set of solutions in practise
to work efficiently in asynchronous systems. 

In the context of distributed systems, BFT is the ability of a blockchain 
network to function as desired and correctly reach a sufficient consensus 
despite malicious components (nodes) of the network failing or propagating 
incorrect information to other peers. The objective is to defend against 
catastrophic system failures by mitigating the influence these malicious 
nodes have on the correct function of the network and the right consensus 
that is reached by the honest nodes in the system. 

## Practical Byzantine Fault Tolerant Mechanism

PBTF is a robust, high-performance algorithm that comes with only a 3% 
increase in latency over a standard unreplicated BFT models.

Unlike PoW or PoS mechanisms, pBFT doesn’t require any hashing power to add 
new blocks to the underlying blockchain. This makes the algorithm much more 
energy efficient and eventually allows it to avoid issues with centralization 
that PoW (mining pools) and PoS (large stake holders cutting deals behind the 
scenes) suffer from.

Nodes in a pBFT blockchain system are sequentially ordered with one node being 
the `primary node` and others considered as `secondary nodes`. All of the nodes 
within the system communicate with each other and the goal is for all of the 
honest nodes to come to an agreement of the state of the system through a majority. 
Any node in the system can assume the role of primary if an old primary node 
fails or starts acting maliciously. The primary node is changed during every 
consensus round nonetheless.

<figure>
    <img src="/blog/wp-content/uploads/2018/02/practical-byzantine-fault-tolerance.png" alt="" />
    <figcaption>Illustration: pBFT</figcaption>
</figure>

The pBFT model works on the assumption that, at any point in time, the total 
amount of malicious nodes on the network doesn't exceed more than 1/3 of the 
total number of network nodes in the system in a given window of vulnerability. 
The more nodes a pBFT system has, the safer it becomes.

Block generation and confirmation in this consensus group follows more of a 
`“Commander and Lieutenant”` format. When a client sends a request to the primary
node the request is processed in three phases: 

 * **Pre-prepare phase**: Here, the primary node announces the request
   to the secondary nodes as a multicast pre-prepare message. The secondary
   nodes receive a `new block` suggestion that the group should agree on.

 * **Prepare phase**: Once received, every node executes the request by 
   `validating` the correctness and authencity of the detailed record. Another
   multicast reply is then sent to the client.

 * **Commit phase**: In this phase, the client prepares to receive a message
   from the `f + 1` majority nodes to ensure that a sufficient number of nodes 
   have agreed on the new block proposed by the primary node.

One PBFT algorithm needs to have a minimum of `3f + 1` replicas (where f is the 
maximum number of faulty nodes) to ensure that its Byzantine Fault tolerance 
is unharmed. This is the mathematical representation of 2/3rd majority.

## PBFT Implementation on Hyperledger 

"Hyperledger" is an open-source collaborative consortium for blockchain projects 
hosted by the Linux Foundation using a permissioned version of pBFT for the platform. 
Currently there are at least 4 different implementations of blockchain frameworks 
under Hyperledger:

* Fabric (IBM)
* Corda (R3)
* Iroha
* Sawtooth Lake (Intel)

**In Fabric**:

All validation peers keep open connection to each other. You can submit your transaction 
to any of them, and this transaction will be broadcasted to other peers in the network. 
One of peer is elected as "leader". At the moment when a new block is going to be generated:

 1. The leader orders the transactions candidates that should be included in a block, 
    and broadcasts this list of ordered transactions to all other validation peers in 
    the network.

 2. When each of the Validation Peers receives the ordered list of transactions, each 
    validation peer does the following:

    > It starts executing the ordered transactions one by one. As soon as all the 
      transactions are executed, it will calculate the hash code for the newly 
      created bloc (the hash code includes hashes for executed transactions and 
      final state of the world). Then it broadcasts the resulting hash code to other 
      peers in the network, and starts counting the responses from them.

If it sees that 2/3 of all validation peers have the same hash code, it will commit 
the new block to its local copy of the ledger.

**In Corda**:

PBFT is not used. This implementation uses another architecture approach. In Corda, 
consensus is provided by notaries. It is up to the notary operator which consensus 
algorithm they use. BFT is one option. You can see a Corda BFT notary sample [here](https://github.com/corda/corda/tree/master/samples/notary-demo).

 1. The transaction is validated by a cluster of one or more notaries. Notaries 
    are nodes with the sole purpose of deconflicting double-spend attempts.

 2. Using a standard BFT algorithm. Each node in the notary cluster votes on 
    whether they consider the transaction to be a double-spend attempt. The final 
    decision is based on a majority rule, and can tolerate up to 1/3rd of the 
    nodes in the cluster being malicious.

 3. In Corda, there is no central store of information that the transaction is 
    committed to. The notary cluster simply adds the spent state reference to an 
    internal database table. It will check future attempts to spend states against 
    this table, and reject the spending attempt if the state reference is already 
    stored there.

**In Hyperledger Sawtooth**:

 * PoET Proof of Elapsed Time (optional Nakamoto-style consensus algorithm used for 
   Sawtooth). PoET with SGX has BFT. PoET Simulator has CFT. Not CPU-intensive as 
   with PoW-style algorithms, although it still can fork and have stale blocks . 
   See [PoET specification](https://sawtooth.hyperledger.org/docs/core/releases/latest/architecture/poet.html)

 * RAFT Consensus algorithm that elects a leader for a term of arbitrary time. Leader 
   replaced if it times-out. Raft is faster than PoET, but is not BFT (Raft is CFT). 
   Also Raft does not fork. Hyperledger Sawtooth has the advantage of having Unpluggable 
   Consensus. An algorithm can be changed without reinitializing the blockchain or even 
   restarting the software.


Since permissioned chains use small consensus groups and don’t need the same decentralization 
as public blockchains, pBFT is effective for providing high-throughput transactions.

## Limitations of PBFT

The pBFT consensus model works efficiently only when the number of nodes in the distributed 
network is small due to the high communication overhead that increases exponentially with every 
extra node in the network.

* **Sybil attacks** : The pBFT mechanisms are susceptible to Sybil attacks, where a
  single entity controls multiple network nodes - compromising network security. This 
  threat is reduced with larger network sizes but considering the scalability issue of 
  pBFT it typically needs to be used in combination with another consensus mechanism. 

* **Scaling** : pBFT does not scale well because of its communication intensive overhead. 
  This is because each node must talk to every other node to keep the network secure, which 
  can quickly grow into a huge communication cost as the amount of nodes scales upwards. 
  When the number of nodes in the network increase so does the time taken to respond to the 
  request. pBFT is a promising consensus solution when the group of nodes is small but becomes 
  inefficient for large networks. 

## Summary

Permissioned blockchains are private and operated by invite with known identities, meaning there is 
already an element of trust between parties. This mitigates the need for a trustless environment and 
allows the network to reap the benefits of pBFT without the downsides.