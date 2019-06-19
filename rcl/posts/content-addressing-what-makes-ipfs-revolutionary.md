---
layout: post
title: "Content Addressing: What Makes IPFS Revolutionary"
date: 2018-08-12 19:07:24
categories: Permanent Web
meta: "Understanding IPFS Content Addressing"
---

IPFS is an internet protocol that makes the web faster, safer, and distributed. It
changes the addressing of information, moving from location addressing to content 
addressing. It provides cryptographic hash content addressing, file integrity and 
versioning, filesystem-level encryption and signing support by combining a series 
of old and new technologies.

Before diving into how content addressing on the IPFS works, lets briefly explore some
feature components that set IPFS apart from other internet Protocols like HTTP:

1. **Network** - The IPFS network runs by combining more protocols that make 
   the connectivity integrity more reliable and authentic. These include 
   the transport protocols, data-channels, using uTP or SCTP, using HMAC 
   with sender’s public key, etc.

2. **Objects** - IPFS builds a Merkle DAG, a directed acyclic graph which 
   providesIPFS many useful properties like content addressing, tamper 
   resistance and deduplication.

3. **Files** - On top of the Merkle DAG, IPFS defines a set of objects for 
   modeling a versioned filesystem . This object models include  block, list, 
   tree & commit.

4. **Naming** - IPNS is the DNS for IPFS. IPNS assigns every user a mutable 
   namespace at: `/ipns/<NodeId>` where a user can publish an Object to this 
   path signed by their private keys. 

All the components of the IPFS can be covered in separate articles but in this post 
we’ll explore how node `identifiers`, `routing` and `data disrtibution` works. We will 
also look into `content addressing`, to find out exactly what happens when you add a 
file to IPFS.

## Identity, Routing, and Data Distribution

**Node identification** follows the scheme from S/Kademlia where nodes are identified 
by a `NodeId`, the cryptographic hash of a public-key, created with S/Kademlia’s static 
crypto puzzle. Nodes store their public and private keys (encrypted with a passphrase). 
Basically: 

 * Nodes in this peer to peer network each hold private keys and release public keys, 
   just like in Bitcoin or Ethereum.
 * Node addresses are derived through hashing their public keys. Allowing connection 
   verification through message signing.
 * Their public keys can be used to encrypt data before it is transferred, preventing 
   interception and theft.

Users are free to instatiate a “new” node identity on every launch, though that loses 
accrued network benefits. **Nodes are incentivized to remain the same**. The crypto-
puzzle is a proof-of-work scheme that makes it hard for an attacker to quickly create 
lots of identities (`a Sybil attack`).

Solutions to the security issues of today’s web are built into this addressing system. 
There is no need for a trusted central certificate issuer to provide connection verification 
tools and all connections can easily be encrypted by default. No more SSL.

For **Routing** IPFS uses a Distributed Sloppy Hash Table (DSHT). DHT is a distributed system 
that provides access to the key-value store. The store is spread across the participating 
nodes and offers excellent performance and scalability. 

<figure>
    <img src="/blog/wp-content/uploads/2018/08/distributed-hash-table.png" alt="" />
    <figcaption>Illustration: Distributed Hash Table</figcaption>
</figure>

The DHT part of the IPFS comes from Kademlia DHT as used in BitTorrent while the “sloppy” 
in DSHT part comes from the Coral DSHT which relaxes the DHT API from `get_value(key)` to 
`get_any_values(key)` and can work with single peer. In return, Coral can distribute only 
subsets of the values to the “nearest” nodes, avoiding node hot-spots. 

**Data distribution,** on the other hand, is based on a variant of BitTorrent called `BitSwap`. 
Incentives are designed in to encourage nodes to store blocks for others, and to prevent 
freeloaders. The strategy used in BitSwap to exchange information with peers is pluggable. 
The choice of function should aim to:

 1. maximize the trade performance for the node, and the whole exchange
 2. prevent freeloaders from exploiting and degrading the exchange
 3. be effective with, and resistant to other, unknown, strategies
 4. be lenient to trusted peers

In order to have something to barter with, a node that has nothing its peers want then seeks 
the pieces that its peers want, with lower priority than it seeks its own blocks. “This 
incentivizes nodes to cache and disseminate rare pieces, even if they are not interested 
in them directly.”

The Bitswap protocol also encourages fair play by incentivizing nodes to seed even when they 
do not need anything in particular, as they might have the blocks others want. Thus, BitSwap 
nodes send blocks to their peers optimistically, expecting the debt to be repaid. It prevents
freeloading by implementing a simple credit-like system that solves the problem by making: 

1. Peers track their balance (in bytes verified) with other nodes. 
2. Peers send blocks to debtor peers probabilistically, according to a function that
   falls as debt increases. 

The credit system is backed up by the BitSwap nodes that keep ledgers accounting the transfers 
with other nodes. This allows nodes to keep track of history and avoid tampering. When activating 
a connection, BitSwap nodes exchange their ledger information. If it does not match exactly, the 
ledger is reinitialized from scratch, losing the accrued credit or debt. 

## Content Addressing and Paths

Content addressing is a technique to reference files or data by a unique `fingerprint` 
derived from the contents of the file or data itself. Content addressing is implemented 
with cryptographic hashing, so that content addresses are secure, permanent, and derived 
directly from the content itself. 

IPFS uses content addressing to ensure files, websites, and webapps can move around the 
network and be distributed by any computer securely and with perfect fidelity. All content, 
including links, is uniquely identified by its multihash checksum. Paths in IPFS are of 
the format:

    ipfs/hash-of-object/name-path-to-object

IPFS is designed to allow the files of millions of users to coexist together. The DHT, 
with content-hash addressing ensures fair and secure publication of objects. Nodes can 
pin objects to the IPFS making them available for all peers on the network. In the process
of adding and publishing objects, they run through a hash function to produce a digest. The
hash produced is guaranteed to be cryptographically uniue to the contents of the object. 

Note that Objects are essentially immutable, just like in Git. New versions hash differently, 
and thus are new objects. Basically, if the content of the file change by even one bit, the 
hash is also changed. Tracking versions is the job of additional versioning objects. This 
object hashing process is best illustrated in the image below, the object in this case, a
cat photo.

<figure>
    <img src="/blog/wp-content/uploads/2018/08/content-hashing.png" alt="" />
    <figcaption>Illustration: IPFS Content Hashing, Source: Textile</figcaption>
</figure>

Currently, on the web, if a file is moved, all links to that file need to be updated if they 
are to resolve. Because IPFS addresses are derived from the content they refer to, if the 
content still exists anywhere on the network, links will always resolve. This removes any need 
for duplication of content, except for the purposes of greater persistence security or for 
scaling up serving capabilities.

### Implications of Content Address

Now that we understand how content addressing works, what are the implication for the web as
we know it? We know that hash links permanently point to exact content and from a computer 
science perspective, any time we create data that uses content-addressed links, a persistent 
and permanent data structure is created. Some of the implications of storing and sharing data 
this way include: 

* **Data is Never Lost** - Unlike centralized servers that lose data in the event of 
  server failures or other limitations this decentralized, content-addressed ensures 
  that data will not become endangered as long as a valid copy of it exists on the IPFS 
  peer network.

* **Data Integrity is Maintained** - Content-addressing enables us to check the data's 
  fingerprints against the links because the connections are resilient and reliable even 
  on a large scale. This kind of validation is impossible with location-addressed links. 

* **Links Don't Die** - IPFS links permanently point to their content. In the unlikely
  event that entire copies of objects are destroyed, once a node re-publishes the content
  all the network peers can continue to link to cryptographic hash of the object or content.  

* **No Single Point of Failure** - As long as at least one node on the network has a copy of 
  the content, it will permanently remain available. Although content can be served from 
  different nodes, it is cryptographically verified to ensure its not tampered with and users 
  access the files as originally published. 

There are alot more ways content-addressing will change the way we use the web, however, for 
a decentralized storage system to grow to replace the current model, we need more ways to 
incentivize the storage and serving of content in this way. One such way is changing the way we
link to content - IPFS accomplishes this using a special feature called `IPNS`. 

## Mutable References and Human-readable names

IPNS, the **Interplanetary Naming System** is the DNS of IPFS. To truly appreciate the 
genius of IPNS, lets first explore the how content can be retrived from the IPFS. You'll
need the hash of the object. Using the example of the cat photo above, we'll access the 
file at `https://ipfs.io/ipfs/QmcBsE7VjTVZKYDmkzzw3A1FVXsBb5hUqJ5BqT34Xp27m` 

To do this, we use a private key to sign a reference to the IPFS hash representing the 
latest version of our file using its public key hash. But this approach has several 
challenges:

  * Firstly, it’s hard to read, let alone remember.
  * Secondly, it’s an immutable link. Which means its permanent. Any changes to the 
    content would generate a new pubkey hash which would break the link to the file. 

The IPNS addresses these problems by creating human readable mutable links and by pointing 
to the pubkey hash to the latest version of any object. 

### Human-Readable Mutable Addressing

IPNS allows you to use the existing Domain Name System (DNS) to provide human-readable 
links to IPFS/IPNS content. It does this by allowing you to insert the hash into a TXT 
record on your nameserver. The name, which follows `/ipns/` in a link is the hash of a 
public key. It is forever associated with the hash it links to that is signed by the 
corresponding private key. 

Simply put, IPNS is a global namespace based on [Public Key Infrastructure](https://en.wikipedia.org/wiki/Public_key_infrastructure) (or PKI) which allows us to build encrypted and authenticated 
trust chains. IPFS has plans to also support Namecoin, which could be used to create a 
completely decentralized, distributed web that has no requirements for a central authority 
in the entire chain. No ICANN, no central servers, no politics, no expensive certificate 
"authorities", and no choke points.

### How we'll use IPFS/IPNS in the future
Long-term, the IPFS can be used for storing all of our sites, and issue IPNS keys for each 
site. Users will continue to publish content on the IPFS and link other users independently.
This will effectively remove user dependency on centralized servers permanently changing the
way we use the web today. If you ask me, this is revolutionary technology whose transforming
I'm excitedly watching for. 

