# Peers

## What is a Peer?

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
