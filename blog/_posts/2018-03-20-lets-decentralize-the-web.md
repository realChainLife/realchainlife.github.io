---
layout: post
title: "Let's Decentralize The Web"
date: 2018-03-20 19:57
categories: Web Decentralization
meta: "Demerits of Web Centralization, how did we get it wrong the first time 
and how do it rectify that?"
---

The internet was initially introduced as a way to build a common neutral network
which everyone can participate in equally for the betterment of humanity. During 
the first dot-com bubble much of this altruism faded as people realized it was 
easier to extract value from this neutral fabric by building <cite>centralized</cite>
services which trap and monetise information. 

So what happened to the initial dream of the web? Fortunately, there is an emerging
movement which is intending to bring the web back to its original vision. It's the 
Decentralized Web or Web 3.0 and since you managed to find this page out of all the 
possible million others on the web, congratulations! You’re passionate about 
decentralizing the web - just like me! 

Jason Griffey, a fellow at the <cite>Berkman Center for Internet and Society at 
Harvard University</cite> describes the Decentralized Web as a series of technologies 
that replace or augment current communication protocols, networks, and services and 
distribute them in a way that is robust against single-actor control or censorship. 
Simply put it's an architectural system that builds services on the internet which 
do not depend on any single “central” organisation to function.

## What’s the Problem With Centralization?

For much of their existence, centralized platforms have provided solutions and 
services to millions of internet users, across multiple continents with easy-to-use
interfaces. The centralization of the internet basically started with its 
commercialization.  

Without this commercialization we could argue the internet would not have survived 
the dot-com bubble. Users of the internet today don't just rely on it for general 
research or online shopping. We also use the Internet to pay bills, RSVP to 
invitations, work remotely with teams around the world and even internet banking. 
It has become a necessity for modern living.

Although the internet centralization has resulted in its expansion of service 
offerings its not without its shortfalls:

1. A user’s access to the Internet is at the mercy of their provider and 
   the platform;
2. CEO's of large tech companies have turned these companies into gatekeepers 
   of information and we have to trust them to use their power fairly and 
   responsibly;
3. Through the creation of Terms of Service or Data Policies, internet users 
   are required to agree with the collection of personal data which is often 
   shared with `Third Parties` for monetary gain;
4. Disruptive tech startups today suffer a slow and painful death as tech-giants 
   exploit their seemingly unlimited supply of cash to copy new features - either
   that or accept being acquired;
5. Centralized architectures, require companies to own centralized servers - which
   expose users to serious security and privacy incidents like data breaches and
   hacks which occur several times a year;
6. These architectures are also vulnerable to Denial of Service and Distributed 
   Denial of Service (DoS/DDoS) attacks;
7. Centralized servers are single points of failure, **when they fail, websites** 
   **and applications that depend on them also fail**.

A decentralized version of the internet would solve many of the problems that the 
current internet faces. Without a single point of failure, Web3.0 is resilient
against cyberattacks. Data breaches also become near impossible without central data
storage solutions. Users would once again have control and ownership of their data. 

It's not lost on me, or avid internet users that there's an urgency to decentralizing
the web. Listings the protocols and networks that will enable us to do this is
relatively easy. However understanding the underlying technology of each decentralized
protocol is usually a good deal harder. 

In this post I want to introduce some of my favorite decentralized systems, 
deconstruct how they work, provide workarounds to some of the substanial bottlenecks 
within each network (both in itself and for other resources) and finally highlight my 
evolution theory for each system. 

## Decentralized File Sharing - IPFS

IPFS, the **InterPlanetary File System**, is a hypermedia protocol created and released
in January 2015 by [Juan Benet](https://en.wikipedia.org/wiki/Juan_Benet_(computer_scientist)).
It's a synthesis of multiple peer-to-peer systems like DHTs, BitTorrent, Git, and SFS 
simplified into one cohesive system that intends to evolve into the web itself, replacing
the more commonly known HTTP protocol.

It's a network designed to create a `content-addressable`, `peer-to-peer` file 
(<cite>text or video formats</cite>) storing and sharing protocol in a distributed file 
system. By switching from the traditional location based addressing of the web, IPFS 
makes it possible to distribute high volumes of data with high efficiency and zero duplication. 

## IPFS Design & Unique Features 

The IPFS Protocol is divided into a stack of sub-protocols responsible for different 
functionalities within the network. These sub-protocols though not independent in-themselves 
are integral to the integrity of the network. They are blended and intergrated for
their unique properties. 

Without going into a lot of the details that are comprehensively covered in the IPFS
[whitepaper](https://github.com/ipfs/papers/raw/master/ipfs-cap2pfs/ipfs-p2p-file-system.pdf),
I'll highlight these subsystems with a short description of each:

* **Identities & NodeId** - Using the S/Kademlia crypto puzzle, nodes are identified
  by a NodeId, the cryptographic hash of its public-key. Although new nodes can 
  be created for every new IPFS launch, users are incentived to maintain the same node;

* **Network** - Nodes on IPFS communicate through several stack features like the use 
  of ICE NAT traversal techniques. IPFS also stores addresses as `multiaddr` formatted 
  byte strings therefore able to function without reliance on or assumption of IP 
  addresses. For example;

  ```
  an SCTP/IPv4 connection
  /ip4/10.20.30.40/sctp/1234/
  ```
* **Node Routing** - For nodes to find other peers' network addresses and serve 
  objects, IPFS uses a *Distributed Hash Table* which enables any participating 
  node to efficiently retrieve the value associated with a given key.

* **BitSwap Protocol** - In IPFS, data distribution happens through the block barter 
  exchange. This is a BitTorrent inspired protocol where nodes have to provide direct 
  value to each other in the form of blocks. In the marketplace each peer **is looking to acquire a set of blocks (`want_list`), and has another set of blocks to offer in exchange (`have_list`)**.

* **Merkle Forest** - This is a map of all network objects linked cryptographically
  through the directed acyclic graph (DAG). The DAG intergration allows IFPS to a)
  uniquely identify content by its `multihash` checksum, **including links** b) detect
  content corruption using data checksum c) deduplicating content by equating objects
  to content and storing once.

* **DNS Naming** - IPFS uses DNS TXT records to map a domain name to an IPFS address.
    Users can edit DNS records, and use them to always point to the latest version of 
    an object in IPFS. Because DNSLink uses DNS records, the names it produces are also 
    usually easy to type and read.

IPFS is designed to be used in several ways and Protocol Labs has continued to expand 
this list. If we bundle all the possible ways IPFS could be used we can summarize to 
the solving of these 3 problems: 

<figure>
  <img src="/blog/wp-content/uploads/2018/11/screenshot-css-media-all.png" alt="" />
  <figcaption>Note that all are presented as the<i>Highest</i>
  priority.</figcaption>
</figure>


By intergrating great peer-to-peer technology from other successful systems - IPFS is able 
to provide a one-in-all-solution to decentralized file sharing. We've seen great services 
already developing on top of the IPFS fabric. The best is yet to come. 

## Decentralized Money - Bitcoin

The next thing we can do to push Web Decntralization towards its natural next phase is much
much simpler. ***Investing in truly decentralized money***. 

`Bitcoin`, by virtue of how it works, is not just a digital currency - it's the foundational 
open source network needed to decentralize economic activity both on the Web and real-world
trade. This is because it has six primary features that differentiate it from the private 
networks used by governments and traditional financial institutions: 

1. It's **permissionless**;
   * Anyone in the world can connect to the network. With resources like computing
     power and software users can participate in the validation of transactions.
2. It's **decentralized**;
   * Through cryptographic breakthroughs, Bitcoin nodes are programmed to hold and 
    independently update the database in the network. 
3. It's **trustless**;
   * A central party isn't required to ensure transcations are valid. 
4. It's **transparent**;
   * The network is a record of transactions between blockchain addresses. Anyone 
     inspecting the network sees every transaction and its hash value.
5. It's **censorship resistant**;
   * A central party cannot invalidate a user's transactions or reverse changes. 
     Also as there are nodes throughout the world it is virtually impossible for 
     the entire network to be taken over by a single party.
6. It's **programmable**;
   * Bitcoin consists of individual behaviour specifications called protocols. The 
     implementation of specific protocols essentially makes it a distributed, peer-to-peer 
     and secured information database programmable to business logic and interoperable 
     financial services.

The entrepreneurial benefits of decentralized money are only just now becoming more apparent 
to millions of internet users world wide. With decentralized finance:

* anyone with an internet connection and a smartphone could access financial services. 
* costly intermediaries are scrapped. remittance fees are as low as 3%
* users have full custody of their wealth and can transact securely without validation
* with cryptograhic key management, wallets are secured using private keys for loss prevention

<small>**Source** Token Economy </small>

I could go on because of countless other ways users have continued to benefit from decentralized 
curriencies. They represent an evolving view of how information can change the world and the web.
From the way we spend money to our communication and even how we acquire services. 

## Decentralized Data Ledgers - BlockChain

<figure>
  <img src="/blog/wp-content/uploads/2018/11/screenshot-ff-import-blocked-by-js.png" alt="" />
  <figcaption>An illustration of Distributed Ledgers by CoinDesk</figcaption>
</figure>

A distributed ledger, as described (briefly) earlier, is a database that is spread across 
several nodes or computing devices. Each node replicates and saves an identical copy of 
the ledger. Each participant node of the network updates itself **independently**.

Distributed ledger technologies drastically reduces the cost of trust. The architectures 
and structures of distributed ledgers can help us mitigate our dependence on banks, 
governments, lawyers, notaries and regulatory compliance officers. 

We've already seen use cases for decentralized data ledgers applied in industries like
[banking](https://www.r3.com/) and [insurance](https://www.everledger.io/). R3CEV tests blockchain applications 
for banking and aims to create a blockchain standard. In their own words, *it was born out of a common frustration with multiple generations of disparate legacy financial technology platforms that struggle to interoperate, causing inefficiencies, risk and spiraling costs*. On the other hand **Everledger** is using
distributed public ledger technology for tracking provenance in a way that’s more 
robust and accessible than a paper trail.

### How BlockChain networks work

With decentralized ledgers, no one party like a bank controls its content, that is,
which transactions get posted (the credits and debits), which modifications are made etc 
as such, blockchain engineers write a series of functions to mediate transactions.
Member nodes in a blockchain network use a `consensus` protocol to agree on ledger 
content,`cryptographic hashes` and `digital signatures` to ensure the integrity of 
transactions.

**Consensus** ensures that the shared ledgers are exact copies, and lowers the risk 
of fraudulent transactions. **Cryptographic hashes**, such as the SHA256 computational 
algorithm, ensure that any alteration to transaction input results in a different 
hash value being computed. **Digital signatures** ensure that transactions originated 
from senders (signed with private keys) and not imposters.

The result of this programming is transactions that cannot be altered or reversed. This
is commonmly referred to network `immutability` because it requires the approval of 
all network participating nodes to agree on data alterations or transaction reversals. 

### Enterprise Blockchain Utilization

Since it is my hope that the web will transform into Web3.0 in the next few years, I've
outlined how enterprises, can create new or utilize existing blockchain networks as a 
strategy for differentiation and specialization in a free market environment.

For a blockchain network to function as highlighted above it requires four critical 
features. Each organisation implementing blockchain technology must consider these
characters:

1. **Consensus Algorithm** - This is the core of every blockchain architecture.
   It's responsible for trustless networks. Nodes might not trust each other, 
   but they can trust the algorithms that run at the core of it. 

2. **Permissionless Ledgers** - Data kept in a perpetual state of forward 
   momentum because of hashing power confirms new transactions that are 
   recorded in every participating node.

3. **Key Management** - This ensures tamper-proof address & wallet security, 
   authentication and integrity of user protection. Popular cryptographic 
   hash functions used include SHA256, Scrypt, ethash, x16 and more.

4. **Smart Contracts (Chaincode)** - These are self-executing contracts 
   converted to computer code, stored, replicated on the system and 
   supervised by the participating nodes. 
   
   This would also result in ledger feedback such as transferring money 
   and receiving the product or service.

   <figure>
      <img src="/blog/wp-content/uploads/2018/11/screenshot-async-js-blocked-by-css.png" alt="" />
      <figcaption>Example of Ethereum Smart Contract</figcaption>
   </figure>

Enterprises that meet key industry requirements such as performance, 
verified identifies, and trustless transactions will benefit the
most from Enterprise Blockchain Utilization.

## Substantial Bottlenecks & Web3.0 Evolution Theory

For Web 3.0 to commercialize and become a great investment several things 
have to happen. Decentralized systems, networks and protocols need to close 
the gap between current Web 3.0 projects status and operationally efficient.

Certain features of permissionless blockchain have backfired on some networks
in the past. Here are some of the disadvantages that us developers of permissionless 
blockchains might need to look at, it will help in overcoming the adoption bottlenecks.

  1. ***Consensus mechanism***- a permissionless blockchain like Bitcoin works on the 
     principle of Proof-of-Work where the millions worth of hashing power is 
     required for node participation. This requires the consumption of a lot 
     of resources, thus, it’s a costly affair.

  2. ***Anonymity BadRep***- Identities of the trading parties remains anonymous in
     most permissionless blockchains. Some critices of `Web Decentralization` 
     argue that this anonymity feature results in blockchain use rising in 
     illicit activities. Its on us Web 3.0 enthusiasts to bring attention to the 
     millions of transactions happening daily done by ordinary citizens around 
     the world. 

These drawbacks of the permissionless blockchain system make it a questionable 
affair for many companies. They believe that it is not suitable for them to 
make permissionless blockchain a platform for offering enterprise solutions. 

## Summary

There is a _lot_ to digest in this article. It ended up going way beyond the
post I initially intended to write. To attempt to summarise my outlook on 
Web3.0:

* `Web Centralization` comes at a huge cost to users;
* `Commercializing Web 3.0` will increase speed of adoption;
* IPFS is leading the way to the `permanent web`;
* Bitcoin is the epitome of `decentralized & distributed finance`
* `Enterprise Blockchain Utilization` will be a multiple industry
  standard.

### Conclusion

Thanks to cryptographic security, decentralized consensus and DLT, blockchain 
technologies can profoundly change the way we organize our economic, social, 
political, and scientific activities. So let's do it **Lets' Decentralize The Web**
