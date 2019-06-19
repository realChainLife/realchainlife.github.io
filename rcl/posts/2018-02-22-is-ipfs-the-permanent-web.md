---
layout: post
title: "Is IPFS The Permanent Web"
date: 2018-02-22 09:51:11
categories: Decentralized Web
meta: "Is Claiming The IPFS is the Permanent Web a Fallacies of Distributed Computing?"
---

[IPFS](https://ipfs.io) the **InterPlanetey File System** is a global, versioned, 
peer-to-peer file system. It combines good ideas from Git, BitTorrent, Kademlia, 
and SFS. You can think of it like a single BitTorrent swarm, exchanging Git objects, 
making up the web. IPFS provides an interface much simpler than HTTP, but has 
permanence built in.

Is claiming the IPFS is the permanent web a **fallacy of distributed computing** then?
Before diving into the detailed workings of IPFS we need to discuss the HTTP protocol - 
the is the most commonly known Internet Protocol. Although, I strongly believe IPFS
will replace HTTP, this position is met with alot of speculation. Replacing HTTP 
sounds like a ball-out-of-the-park idea yet alot of us concur the current internet
model is broken and needs us to apply state of the art technology to the distribution 
problem, and design a better protocol for the web.

In this post, I want to focus on three thing in relation to the web design: how HTTP 
works, the problems with HTTP design models and how IPFS solves this problems. Whether
we realise it or not, we’re in the business of distributed computing: you probably want 
that internet service you're building to make its way from one computer (a server) to 
another computer (a user’s phone) over some kind of network (the internet) with minimal
intermediaries.

## How HTTP Protocols Work

The **Hypertext Transfer Protocol** (HTTP) has unified the entire world into a single 
global internet protocol, standardizing how we distribute and present information 
to each other. Traditionally, HTTP follows a simple `client-server` model. Basically,
files are accessed and retrieved based on their `server` location using a URL (Uniform 
Resource Locator). 

When a `client` computer across the world request a file from this server irrespective 
of their location, the URL is used to find its location on a computer network and its
retrieved and loaded on the client side server. But while HTTP has achieved many things, 
it's usefulness as a foundation for the distribution of the sum of human knowledge is 
crumbling to pieces right in front of us; For example, HTTP does not work in the offline 
case or in scenarios with limited bandwidth. 

Also, the way HTTP distributes content is fundamentally flawed, and no amount of performance 
tuneups or forcing broken CA SSL or anything else is going to fix that. Some of these flaws 
are:

* **HTTP Is Fragile** - If you've been using the internet for any given time then 
  you've come across a `404 Error` or `Not Found Error`. These error occur when a 
  HTTP web server connection to the client server fails. This can happen if web 
  servers have been powered down, if the links stopped working, if the server fails 
  or is no longer accessible at the same location, or even the worst possible flaw,
  the chain between the sites becomes permanently broken, and the ability to access 
  that content is lost forever.

  All these factors point to the brittleness of HTTP web servers and hightlights 
  the problem with HTTP: It `erodes`. When a site is no longer available on the 
  server at that linked location the content you're looking for is usually gone, 
  and it has no way to help you find it. And unless the [Internet Archive](https://archive.org/) 
  backed it up, you'll never find it again. It becomes lost, forever.

  Also, the older a web page is, the more likely it is you'll see 404 pages. HTTP 
  is inadequate for maintaining links between sites. While all the static content 
  stored with the site still loads, any links offsite or to dynamically served 
  content are dead. Whether eroding content is `timelessly useful`, it's still our 
  history, and we're losing a lot of it everyday and we're losing it fast.

* **HTTP Propagates Centralization** - The web was originally designed to be 
  decentralized how during the peak of internet commercialization billions of users 
  were left dependent on a small handful of services to use. While this commercialization 
  propagated a lot of new internet-based service solutions centralization didn't 
  come without its challenges. 

  Today, centralized web servers can be intercepted by multi-parties for various 
  reasons all affecting customer security and protection. Centralization makes it 
  easy for governments to `censor content` at their borders by blocking the access 
  to centralized sites. It also puts our communications at risk of being interrupted 
  by `DDoS attacks`. Customers also face the risk of `data breaches` through hackers 
  who can extort money for stolen data or even make it available on the black market.

  Distributing the web would make it less malleable by a small handful of powerful 
  organizations, and that improves both our freedom and our independence. It also 
  reduces the risk of the *"one giant shutdown"* that takes a massive amount of data 
  with it.
  
* **HTTP Is Cost Inefficient** - HTTP lowered the price of publishing, but it still 
  costs money, and these costs can really add up. Distributing a lot of data from 
  central datacenters is potentially very expensive if not done at economies of scale. 
  Latency and Bandwidth are the two keys to protocol performance. Latency is a measure 
  of the fixed costs of a transaction and does not change as documents get bigger or 
  smaller. Bandwidth is a measure of how long it takes to send data.

  If, for example, I had a file sized 117 Megabytes distributed and downloaded 2,344,327,696
  times, that means (at most) 274,286,340,432 Megabytes, or 274.3 Petabytes of data for the 
  file alone has been sent since it was published. If we assume a total expense of 1 
  cent per gigabyte (this would include bandwidth and all of the server costs), $2,742,860 
  has been spent on distributing this one file so far.

  The cost of opening a new connection for each transaction or to serve this much data 
  would be astronomical, especially when bandwidth rates for small players start around 
  $0.12 per gigabyte and go as high a $0.20 in Asia. We need options for less expensive 
  bandwidth to ensure we can keep running our infrastructure at low cost.

* **HTTP Creates Overdependence on The Internet Backbone** - Not only has web server 
  centralization made it highly dependent on the datacenter functionality model it has 
  also made it easy for governments to block and censor content. Even with redundancies,
  major architectural network backbones get damaged or go haywire each with drastic
  consequences to customers.

  The point is, this architectural network design isn't perfect, it's easy to attack it, 
  and it's easy for services to get affected by a few important fiber lines getting cut 
  for example.

[HTTP/2](https://http2.github.io/) is a welcome improvement, but it's a conservative update to 
a technology that's beginning to show its age. To have a better future for the web, we need more 
than a spiced up version of HTTP, we need a new foundation. And per the governance model of 
cyberspace, that means we need a new protocol. IPFS, I'm strongly hoping, becomes that new protocol.

## IPFS: A Suitable HTTP Replacement

<figure>
    <img src="/blog/wp-content/uploads/2018/02/what-is-ipfs.png" alt="" />
    <figcaption>Illustration: What Is IPFS?</figcaption>
</figure>

To understand why I'm keen on `replacing` HTTP with IPFS as the protocol
of the decentralized web, we first need to understand what it is, how it works,
and how it addresses all the critical flaws currently limiting HTTP. 

IPFS envisions a world where any resource is available via a locally mounted 
filesystem at paths like:

 **a mutable path**

    /ipns/my.host.com/some/file.txt

**or a permanent path**

    /ipfs/Qmc8vVBLPjc9CXaKtFK3wiq9zoXvuB4XDeY5Xra2LmhMKg/some/file.txt

Files don't necessarily have to reside on the local machine to be accessible if 
they exist on the IPFS, a global distributed storage system. IPFS Files in this 
namespace have: 

1. **High availability** - Files can be fetched from any host that stores 
    and is willing to provide the data.
2. **Easy Access** - The /ipns and /ipfs filesystems are usable as local 
    storage instead of remote servers, as in HTTP. In fact, nodes 
    chose which files they store locally.
3. **Trustless** - Like in git where you can trust files in a commit if you 
    trust the commit ID.
4. **Signature** - Files can be signed and publishers can be linked to %PATH%
    of publication. 
5. **Merkle-linking** - You can version and back up files using the merkle-dag.
    Creating a merkle forest of linked data structures.

To achieve these, IPFS integrates several successful techniques from the last 
15 years of distributed systems research. Central to the IPFS design is the `Merkle` 
`DAG`, a data structure that represents all the files. It’s like Git’s blob, tree, 
and commit, except IPFS has a more flexible model: you can define what your link 
structure is and how it works. This means you can implement Git on top, or a 
Blockchain like Bitcoin, or linked web pages.

IPFS is general purpose, and has little in the way of storage limitations. It can 
serve files that are large or small. It automatically breaks up larger files into 
smaller chunks, allowing IPFS nodes to download (or stream) files from not just 
one server like with HTTP, but hundreds of them simultaneously. 

<blockquote class="pull-quote  pull-quote--context">
  <p>IPFS is The Permanent Web, where links do not die</p>
  <b class="pull-quote__source">
    <a href="">realChainʕ •ᴥ•ʔ</a>
  </b>
</blockquote>

The IPFS network becomes a finely-grained, trustless, distributed, easily federated 
Content Delivery Network (CDN). This encrypted, integrity-checked CDN can be used for 
large static files including: images, video streaming, distributed databases, entire 
operating systems, blockchains, and most important for us, **static web sites.**

IPFS files can also be special IPFS directory objects, which allow you to use human 
readable filenames (which transparently link to other IPFS hashes). Using 
directory objects, IPFS allows you to make static web sites exactly the same way 
you make them today. It's a single command to add your web site to an IPFS node: 
`ipfs add -r yoursitedirectory`. After that, it's available from any IPFS node without 
requiring you to link to any hashes in the HTML.

IPFS has alot more features and functions that can be listed as use cases including:

  1. A mounted global filesystem, under /ipfs (permanent) and /ipns (mutable);
  2. A mounted personal sync folder that automatically versions, publishes, 
    and backs up any writes (like a versioned, distributed Dropbox);
  3. Encrypted file or data sharing system;
  4. Distributed mutable content (BitTorrent + Git);
  5. Distributed data structures;
  6. Versioned package manager for all software;
  7. Booting a virtual machine from the network;
  8. Booting a VM from a hash;
  9. Merkle DAG database model for versioning, caching, and distribution;
  10. Linked (and encrypted) communications platform

To get started with IPFS, stick around. In the next section we'll take a deep technical 
dive into IPFS. I'll show you how to set up IPFS on Windows, Mac & Linux. We'll also 
initialize the network and we'll add your first file to IPFS.  

## How It Works: IPFS Deep Dive

To get started you need to [download IPFS for your platform](https://dist.ipfs.io/#go-ipfs), 
by clicking `download go-ipfs`. This is a prebuilt package for the Go Implementation of the 
IPFS. 

Once the executible files have been downloaded they need to be moved to the proper location:

**On Mac/Linux:**

Unpack the archived folder, and move the `ipfs` file somewhere in your `$PATH`. To do this 
via Terminal:

    sudo mv ipfs /usr/local/bin/ipfs

**On Windows:**

Unzip the archive, and then cut `ipfs.exe` and paste somewhere in your `%PATH%`. To do this 
via Command Prompt: Run Command Prompt as Administrator

    C:\..>move .\go-ipfs\ipfs.exe C:\Windows


### Environment Setup

Before using IPFS for the first time you'll need to `initialize` the repository with the 
**ipfs init** command:

    ipfs init
    initializing ipfs node at /Users/realchainlife/.go-ipfs
    generating 2048-bit RSA keypair...done
    peer identity: QmU6vXuNb6P7H8hwrbNPWiLBikrdf1d6Q9kLAhEK4Kcmub
    to get started, enter:

      ipfs cat /ipfs/QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2/readme
  

The `repository` is a directory that's used by ipfs to stores all its settings and internal 
data. Run the suggested output command: 

    ipfs cat /ipfs/QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2/readme

The output should look something like this, notifying you that you have **successfully**
**installed IPFS.**

<figure>
    <img src="/blog/wp-content/uploads/2018/02/successful.png" alt="" />
    <figcaption>Output: Successfully Installed IPFS</figcaption>
</figure>

You can explore other objects in there. In particular, check out quick-start:

    ipfs cat /ipfs/QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2/quick-start

### Add Files To IPFS

Once `ipfs init` is completed successfully, we are ready to run a daemon and start running
things online; but first we'll start by creating a directory *ipfsdirectory* and writing a 
simple *hello.txt* file with the content *Hello World* 


    $ mkdir ipfsdirectory
    $ cd ipfsdirectory
    $ touch hello.txt

Now we can add this file to the IPFS:


    $ ipfs add hello.txt 
  
    added QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2 hello.txt


For other nodes on the IPFS network to know they can access the file from our machine, we 
need to pin the file we just added: 


    $ ipfs pin add QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2

    pinned QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2 recursively


Now the file no-longer exists only on our local machine.

### Connect IPFS Node to the IPFS Network

By this point we have successfully downloaded, initialized, added and pinned a file on the 
IPFS, however we are yet to introduce our `node` to the IPFS network. This allows other nodes/
participants on the network to listen to our machine and retrieve files from our machine, 
and vice versa.

To do this, run:

    $ ipfs daemon

and expect an output similar to this:

    Initializing daemon...
    Adjusting current ulimit to 2048...
    Successfully raised file descriptor limit to 2048.
    Swarm listening on /ip4/127.0.0.1/tcp/4001
    Swarm listening on /ip4/192.168.0.101/tcp/4001
    Swarm listening on /ip6/::1/tcp/4001
    Swarm listening on /p2p-circuit/ipfs/QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2
    Swarm announcing /ip4/127.0.0.1/tcp/4001
    Swarm announcing /ip4/192.168.0.101/tcp/4001
    Swarm announcing /ip4/71.75.18.38/tcp/23917
    Swarm announcing /ip6/::1/tcp/4001
    API server listening on /ip4/127.0.0.1/tcp/5001
    Gateway (readonly) server listening on /ip4/127.0.0.1/tcp/8080
    Daemon is ready

Once you’re connected to the network, you can search peer connections when you run:

    $ ipfs swarm peers
  

IPFS has a number of bootstrapping nodes that are actively looking for new content placed 
on the network. This will be your initial connections. From here, we can access any one 
of our files from their website, where they have mounted the IPFS system on their HTTP 
URL: `https://ipfs.io/ipfs/[yourHash]`. In my case to check the file *hello.txt* we'll run:

`https://ipfs.io/ipfs/QmqaxZwuMiUhyvYycToWiUfMtowAPMcX9Ba8nUH4Jz3Xf2`.

Best not to forget to kill the daemon if you want to disconnect from the network. This is 
pretty easy. Go to the terminal where daemon is running and press `CTRL+C`. IPFS allows 
users to create new hashes with every new network launch but nodes are incentivized to remain 
the same. 

## Getting Involved With The IPFS

IPFS is an open-source, MIT-licensed project. Now that you've been introduced to the IPFS 
basics I encourage you to `buidl` different new solutions with IPFS. It's still early, and 
there's much work to do before IPFS can replace HTTP without needing to describe the idea 
as crazy. But there's no time like the present to plan for the future. It's time for us 
to get to work and build the permanent & distributed web. **Let's Decentralize The Web**

The easiest way to start is to watch or star these repositories on GitHub to follow along:

* [ipfs protocol](https://github.com/ipfs/ipfs)
* [go-ipfs](https://github.com/ipfs/go-ipfs)
* [js-ipfs](https://github.com/ipfs/js-ipfs)

Also, you can read more [IPFS docs](https://github.com/ipfs/docs) or join #ipfs on irc.freenode.org.

## Quick Summary 

IPFS is a protocol:

* defines a content-addressed file system
* coordinates content delivery
* combines Kademlia + BitTorrent + Git

IPFS is a filesystem:

* has directories and files
* mountable filesystem (via FUSE)

IPFS is a web:

* can be used to view documents like the web
* files accessible via HTTP at http://ipfs.io/
* browsers or extensions can learn to use the ipfs:/ or fs:/ URI schemes directly
* hash-addressed content guarantees authenticity

IPFS uses crypto:

* cryptographic-hash content addressing
* block-level deduplication
* file integrity + versioning
* filesystem-level encryption + signing support

IPFS is p2p:

* worldwide peer-to-peer file transfers
* completely decentralized architecture
* no central point of failure

IPFS is a cdn:

* add a file to the filesystem locally, and it's now available to the world
* caching-friendly (content-hash naming)
* bittorrent-based bandwidth distribution

To learn even more about the Permanent Web check out Juan Benet's talk at Sourcegraph.

<figure class="c-video">
    <iframe class="c-video__media" src="https://www.youtube.com/watch?v=skMTdSEaCtA&t=2s" frameborder="0" allowfullscreen=""><iframe>
</figure>

