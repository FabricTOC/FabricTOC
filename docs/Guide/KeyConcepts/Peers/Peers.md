# Peers

As you've seen, **two of the most important concepts in a blockchain network are ledgers and smart contracts**. That's because smart contracts and ledgers are used to encapsulate the shared **information** and shared **processes** in the business network, respectively. When a developer writes a blockchain application, the ledgers and smart contracts allow a network participant to provide or consume services in the network.

What makes peers important is that **they are the place where ledgers and smart contracts physically reside**. Because of this, peers -- and their connections to other nodes (to peers and to orderer nodes) -- **are what actually form the physical structure of blockchain network**.

## Peers form the blockchain network

A blockchain network is formed by a set of peer nodes.  Peers are the most important elements of the network because they host ledgers and smart contract chaincodes.  Without peers, there cannot be a blockchain network, and they are the first physical concept to understand.  Other elements are important, such as orderers, channels and policies -- you'll learn about these elsewhere, but you'll find it easiest to start with peers.

| ![Peer1](./Peers.diagram.1.png) |
| :---: |
| An example blockchain network formed by three peers. A blockchain is primarily formed from peer nodes, each of which can hold copies of a ledger and smart contracts. In this example, each peer holds a copy of the same ledger and smart contracts. |

It's helpful to remember that the blockchain network only comes into existence when peers and certain other objects -- such as policies, orderers, and MSPs -- are defined. It means that **blockchain networks are not objects in themselves** -- administration of a blockchain network amounts to the management of these objects, rather than any separate object called a "network".

 **Peers are the primary objects that administrators manage on a day-to-day basis using the `peer` command**. Peers can be created, started, stopped, reconfigured, and even deleted. You'll see later how peers are represented as operating system processes to provide the functionality to application programs who wish to consume key services provided by a peer.

## Peers host smart contracts and ledgers

Let's look at a peer in a little more detail.  We can see that it's the peer that hosts both the ledger and smart contracts.  More accurately, the peer actually hosts *instances* of the ledger, and *instances* of smart contract chaincode.

| ![Peer2](./Peers.diagram.2.png) |
| :---: |
| A Peer hosts ledgers and smart contracts. There can be many smart contracts hosted on a peer for a ledger.  |

Because a peer is a *host* for smart contracts and ledgers, if a network participant wants to provide or consume smart contracts and ledgers, they must interact with a peer.  A network participant might be using an application, or might be an administrator -- but it's always the peer that provides the key services that relate to ledgers and smart contracts.  That's why peers are often considered the most fundamental building blocks of a blockchain network.

## Hosting multiple ledgers

The number of ledgers and peers and smart contracts that will be hosted on a peer can vary wildly. A peer can technically (though rarely, outside of a specialized test scenario) hold zero ledgers, but will in practice hold a ledger for every channel to which it's a member. Likewise a peer can hold as few as zero smart contracts but will often have several per channel.

| ![Peer3](./Peers.diagram.3.png) |
| :---: |
| Peers hosting different numbers of ledgers and smart contracts. Peers have one or more ledgers, and each ledger has zero or more smart contracts that apply to them. Moreover, some smart contracts may apply to multiple ledgers.  

Typically, a peer will have many more smart contracts than ledgers on its file system, but there is a fairly common scenario in which a peer will have a ledger and no smart contracts -- when a peer is owned by a regulator (such as the DMV, or another government agency) that wants to monitor transactions on the channel. This peer will still receive ledger updates -- peers receive updates to the ledger for a channel regardless of the smart contracts it has installed on it -- but without a smart contract it won't be able to initiate a ledger update.

The same smart contract can also be instantiated (i.e., be running) on several different channels. This is particularly useful if an organization in the network -- an insurance company, for example -- wants to be able to offer the same services to organizations across several different channels.  

## Hosting multiple smart contracts

## Peer Container  

When a peer does host smart contracts.



Moreover a peer can host multiple smart contracts for the same ledger, because different smart contracts can encapsulate different





That's not the whole story, however, because these different *physical* copies of the ledger need to be kept synchronized with each other, so that they can be considered to be the same *logical* ledger. This is achieved by a process called consensus -- which keeps the individual physical ledgers in step with each other. We'll discuss the logical/physical nature of the ledger and smart contracts later, as well as how peers take part in the consensus mechanism. First let's understand a little more about individual peers.

## Peers and decentralization

**Peers are what makes a blockchain a distributed ledger**, because a network comprises many peers, and it's these peers which hold a copy of the ledger and the smart contracts which interact with it.


## Applications and peers

| ![NetworkPeers1](./Peers.diagram.2.png) |
| :---: |
| Peers in a Hyperledger Fabric blockchain network. An application interacts with the smart contracts and ledgers in a blockchain network by communicating with a one or more peers on a particular channel. Smart contracts can be used to query or update the ledger. |

| ![NetworkPeers2](./Peers.diagram.3.png) |
| :---: |
| Applications connect to peers to invoke smart contracts which query or update the ledger. Queries are returned  |

## Organizations and peers

## Channels and Peers

## The services provided by a peer

### Material to be incorporated

## Logical Network

You might have noticed that the example above does not show an orderer, but as you've seen, orderers -- like peers -- are not necessary to form a blockchain network on a logical level (just as the rules of the road can be written before there are highway interchanges).

The physical structure of the peers and orderers separates them from the logical framework of the policies that govern how peers and the orderer nodes interact. This is similar to how a *set of laws* -- the rules of driving, for example -- are different from the people, cars, and physical structures that actually make up the *highway system*.  

## Applications and peers

The peers in a Fabric network function both as **providers** of services to the network and as **consumers** of those services. A rough analogy might be to a co-op -- a grocery store where the people who shop there are also the stockers and cashiers.

This combination of tasks and responsibilities makes the exact "role" of a peer somewhat difficult to pin down -- it has, as a practical matter, **many** roles. Consider that in the course of a transaction flow, a peer might be involved in all of the following:

  1. Proposing the transaction (either directly through its own application or as a medium for an outside application using the peer as an access point to the network).
  2. Checking the endorsement policy for the transaction to make sure the correct number -- or a particular set of peers specified in the endorsement policy -- have signed the transaction.
  3. Executing a version check of the ledger (held by the peers on a channel -- more on this later) to make sure that there have been no other transactions written to the ledger since the proposal was made.
  4. Receiving the transaction response from the ordering service.
  5. Writing the transaction to its ledger (assuming all goes well).  

Peers are owned and controlled by consortia members. Each member organization can have one peer or several, depending on its needs. Within an organization, one peer must be specified as the **Leading Peer**. It is this peer that interacts with the network at large and disseminates ordered transactions to the other peers in its organization. If this peer goes down, another peer within that organization will take over its role until the leading peer is back functioning. For the purpose of communication between organizations using gossip, an **Anchor Peer** is also specified. This peer will often but not necessarily be the same peer as the leading peer. We'll talk more about gossip later.

## Peers and the Ledger

Ledgers are stored on a peer's file system (either locally or externally depending on the type of database the peer is using). Peers will have a separate ledger for every channel they're a member of.

Link here to TheLedger.md.


## Peers and Identity

Local MSP (at the peer level). Who is allowed to do what on that peer? The peer will have the same MSP as its organization (since peers belong to organizations). Will go back to the RCA of the ORG. This org msp structure is what allows intraorganizational gossip and the function of the leading/anchor peers.

Peers will also maintain Global MSP for every channel they're a part of. Regulates permissions on those channels. Peers may be a part of many channels and will maintain a Global MSP for each channel.

Sign certs.

Also, at the channel level -- what are admins for that peer allowed to do on the channel (instantiate chaincode, for example -- implicit metapolicies)?



## Starting and Stopping Peers

The state database will automatically get recovered (or generated if needed) upon peer startup, before transactions are accepted.



## Joining a Channel

Get the ledger from the Leading Peer. Or, if there's no Leading Peer, from the orderer. It could also be gotten from another Anchor Peer in a channel, but this is not a best practice.

Difference between being added to a channel that's already running and being part of the founding of a channel. If peer is part of the creation of a channel, it's ORG MSP will be part of the initial config block of the channel. If peer is being added to a channel that doesn't recognize its ORG MSP, the MSP of that ORG must be added by the admins of the channel.

Specify that even if ORG1 and ORG2 use the same RCA -- Verisign, for example -- the specific ORG MSP must be added to the channel first (since peers must be tied to an organization). *I think that's right, anyway*.


## Changing a Peer

All of the components in a Fabric network have a version.

What are the configurations of a peer that are optional (ie **can** be updated)? Admin policy.



## Gossip

Peers leverage gossip to broadcast ledger and channel data in a scalable fashion. Gossip messaging is continuous, and each peer on a channel is constantly receiving current and consistent ledger data from multiple peers. Each gossiped message is signed, thereby allowing Byzantine participants sending faked messages to be easily identified and the distribution of the message(s) to unwanted targets to be prevented. Peers affected by delays, network partitions or other causations resulting in missed blocks, will eventually be synced up to the current ledger state by contacting peers in possession of these missing blocks.

The gossip-based data dissemination protocol performs three primary functions on a Hyperledger Fabric network:

    1. Manages peer discovery and channel membership, by continually identifying available member peers, and eventually detecting peers that have gone offline.
    2. Disseminates ledger data across all peers on a channel. Any peer with data that is out of sync with the rest of the channel identifies the missing blocks and syncs itself by copying the correct data.
    3. Bring newly connected peers up to speed by allowing peer-to-peer state transfer update of ledger data.

Gossip-based broadcasting operates by peers receiving messages from other peers on the channel, and then forwarding these messages to a number of randomly-selected peers on the channel, where this number is a configurable constant. Peers can also exercise a pull mechanism, rather than waiting for delivery of a message. This cycle repeats, with the result of channel membership, ledger and state information continually being kept current and in sync. For dissemination of new blocks, the leader peer on the channel pulls the data from the ordering service and initiates gossip dissemination to peers.

Online peers indicate their availability by continually broadcasting “alive” messages, with each containing the public key infrastructure (PKI) ID and the signature of the sender over the message. Peers maintain channel membership by collecting these alive messages; if no peer receives an alive message from a specific peer, this “dead” peer is eventually purged from channel membership. Because “alive” messages are cryptographically signed, malicious peers can never impersonate other peers, as they lack a signing key authorized by a root certificate authority (CA).

In addition to the automatic forwarding of received messages, a state reconciliation process synchronizes world state across peers on each channel. Each peer continually pulls blocks from other peers on the channel, in order to repair its own state if discrepancies are identified. Because fixed connectivity is not required to maintain gossip-based data dissemination, the process reliably provides data consistency and integrity to the shared ledger, including tolerance for node crashes.





## Peers in DRIVENET

Regal might choose to have two different peers to put on the two channels they're on (but they don't need to).




          + What is a peer?
          + Peers and the ledger
          + Peers and Identity
          + Starting and Stopping Peers
          + Joining a channel
          + Changing a Peer
          + Peers in DRIVENET

[Next: Chaincode](./Chaincode.md)
