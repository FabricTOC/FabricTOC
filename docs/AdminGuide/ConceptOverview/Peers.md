# Peers

## What is a Peer?

Peers are a part of organization. They're where applications live and are therefore the action point for end users to access/write to the ledger. Endorsement. Validation.

Leading Peer (intra-organizational designation). Peers within an org use gossip to communicate with each other (to stay up to date). A new peer brought into a channel will get the ledger from the leading peer of that organization. Anchor Peers (inter-organizational designation) communicate with each other with gossip as well. Peers can get the ledger from a fellow Anchor Peer on that channel if the orderer goes down, but this is not a best practice.



## Peers and the Ledger

Ledgers are stored on a peer's file system (and are, therefore, written by the peer, although peers may only write after the transaction flow is complete, and must write what they're told to write). Different ledgers for every channel.



## Peers and Identity

Local MSP. 




## Starting and Stopping Peers




## Joining a Channel




## Changing a Peer





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
