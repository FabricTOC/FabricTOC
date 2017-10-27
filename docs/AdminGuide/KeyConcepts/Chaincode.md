# Chaincode

## What is Chaincode?

Chaincode is a program, written in Go, node.js, that implements a prescribed interface. Eventually, other programming languages such as Java, will be supported. Chaincode runs in a secured Docker container isolated from the endorsing peer process. Chaincode initializes and manages the ledger state through transactions submitted by applications.

A chaincode typically handles business logic agreed to by members of the network, so it similar to a “smart contract”. Ledger state created by a chaincode is scoped exclusively to that chaincode and can’t be accessed directly by another chaincode. Given the appropriate permission, a chaincode may invoke another chaincode to access its state within the same network.

A chaincode typically handles business logic agreed to by members of the network, so it may be considered as a “smart contract”. State created by a chaincode is scoped exclusively to that chaincode and can’t be accessed directly by another chaincode. However, within the same network, given the appropriate permission a chaincode may invoke another chaincode to access its state.

The Hyperledger Fabric API enables interaction with the various nodes in a blockchain network - the peers, orderers and MSPs - and it also allows one to package, install, instantiate and upgrade chaincode on the endorsing peer nodes. The Hyperledger Fabric language-specific SDKs abstract the specifics of the Hyperledger Fabric API to facilitate application development, though it can be used to manage a chaincode’s lifecycle. Additionally, the Hyperledger Fabric API can be accessed directly via the CLI, which we will use in this document.

We provide four commands to manage a chaincode’s lifecycle: package, install, instantiate, and upgrade. In a future release, we are considering adding stop and start transactions to disable and re-enable a chaincode without having to actually uninstall it. After a chaincode has been successfully installed and instantiated, the chaincode is active (running) and can process transactions via the invoke transaction. A chaincode may be upgraded any time after it has been installed.

Packaging

The chaincode package consists of 3 parts:

        the chaincode, as defined by ChaincodeDeploymentSpec or CDS. The CDS defines the chaincode package in terms of the code and other properties such as name and version,
        an optional instantiation policy which can be syntactically described by the same policy used for endorsement and described in Endorsement policies, and
        a set of signatures by the entities that “own” the chaincode.

The signatures serve the following purposes:

        to establish an ownership of the chaincode,
        to allow verification of the contents of the package, and
        to allow detection of package tampering.

The creator of the instantiation transaction of the chaincode on a channel is validated against the instantiation policy of the chaincode.

A chaincode package that was signed at creation can be handed over to other owners for inspection and signing. The workflow supports out-of-band signing of chaincode package.

If the instantiation policy is not specified, the default policy is any MSP administrator of the channel.





A way of establishing rules over transactions ("business logic") and automating them (not just more efficient but provides utility -- use case here temperature of flowers in shipping container). Similar to the concept of smart contracts (which are written in chaincode).

What is a contract? Why are they important? What are their weaknesses? How does chaincode and smart contracts address these weaknesses? *This part briefly*

## System Chaincode

System chaincode has the same programming model except that it runs within the peer process rather than in an isolated container like normal chaincode. Therefore, system chaincode is built into the peer executable and doesn’t follow the same lifecycle described above. In particular, install, instantiate and upgrade do not apply to system chaincodes.

The purpose of system chaincode is to shortcut gRPC communication cost between peer and chaincode, and tradeoff the flexibility in management. For example, a system chaincode can only be upgraded with the peer binary. It must also register with a fixed set of parameters compiled in and doesn’t have endorsement policies or endorsement policy functionality.

System chaincode is used in Hyperledger Fabric to implement a number of system behaviors so that they can be replaced or modified as appropriate by a system integrator.

The current list of system chaincodes:

    LSCC Lifecycle system chaincode handles lifecycle requests described above.
    CSCC Configuration system chaincode handles channel configuration on the peer side.
    QSCC Query system chaincode provides ledger query APIs such as getting blocks and transactions.
    ESCC Endorsement system chaincode handles endorsement by signing the transaction proposal response.
    VSCC Validation system chaincode handles the transaction validation, including checking endorsement policy and multiversioning concurrency control.

Care must be taken when modifying or replacing these system chaincodes, especially LSCC, ESCC and VSCC since they are in the main transaction execution path. It is worth noting that as VSCC validates a block before committing it to the ledger, it is important that all peers in the channel compute the same validation to avoid ledger divergence (non-determinism). So special care is needed if VSCC is modified or replaced.


## Chaincode and the Ledgers

Chaincode is written to the ledger(s) for a **specific channel** and exists/functions on the channel level. This makes it immutable just like any other block (though new versions of a chaincode can be installed/instantiated -- more on this in "Upgrading Chaincode"). There is system chaincode (which is part of the initial config block -- ie the "genesis block") and serves as the chaincode for the system channel (ie, the "network").


## Installing Chaincode

Chaincode funtions at the channel level -- and is written to the ledger for that channel -- but it is installed at the peer level. Channels can have multiple chaincodes/smart contracts functioning on it simultaneously and every endorsing peer node of a channel that will run your chaincode must have it installed. If a peer is not endorsing it will still write transactions to its copy of the channel ledger. Chaincode should only be installed on endorsing peer nodes of the owning members of the chaincode to protect the confidentiality of the chaincode logic from other members on the network. Those members without the chaincode can’t be the endorsers of the chaincode’s transactions; that is, they can’t execute the chaincode. However, they can still validate and commit the transactions to the ledger.

Chaincode can be created by anyone. 


## Instantiating Chaincode

Happens at the channel level (though the same chaincode can be installed on multiple channels, it's actions are kept isolated -- not unlike any program that's been installed on different computers). This instantiation is when the chaincode is written to the ledger. Must have admin rights over that channel to instantiate. Only happens once.

The instantiate transaction invokes the lifecycle System Chaincode (LSCC) to create and initialize a chaincode on a channel. This is a chaincode-channel binding process: a chaincode may be bound to any number of channels and operate on each channel individually and independently. In other words, regardless of how many other channels on which a chaincode might be installed and instantiated, state is kept isolated to the channel to which a transaction is submitted.

The creator of an instantiate transaction must satisfy the instantiation policy of the chaincode included in SignedCDS and must also be a writer on the channel, which is configured as part of the channel creation. This is important for the security of the channel to prevent rogue entities from deploying chaincodes or tricking members to execute chaincodes on an unbound channel.

For example, recall that the default instantiation policy is any channel MSP administrator, so the creator of a chaincode instantiate transaction must be a member of the channel administrators. When the transaction proposal arrives at the endorser, it verifies the creator’s signature against the instantiation policy. This is done again during the transaction validation before committing it to the ledger.

The instantiate transaction also sets up the endorsement policy for that chaincode on the channel. The endorsement policy describes the attestation requirements for the transaction result to be accepted by members of the channel.


## Upgrading Chaincode

Has a version.

A chaincode may be upgraded any time by changing its version, which is part of the SignedCDS. Other parts, such as owners and instantiation policy are optional. However, the chaincode name must be the same; otherwise it would be considered as a totally different chaincode.

Prior to upgrade, the new version of the chaincode must be installed on the required endorsers. Upgrade is a transaction similar to the instantiate transaction, which binds the new version of the chaincode to the channel. Other channels bound to the old version of the chaincode still run with the old version. In other words, the upgrade transaction only affects one channel at a time, the channel to which the transaction is submitted.

Note

Note that since multiple versions of a chaincode may be active simultaneously, the upgrade process doesn’t automatically remove the old versions, so user must manage this for the time being.

There’s one subtle difference with the instantiate transaction: the upgrade transaction is checked against the current chaincode instantiation policy, not the new policy (if specified). This is to ensure that only existing members specified in the current instantiation policy may upgrade the chaincode.

Note

Note that during upgrade, the chaincode Init function is called to perform any data related updates or re-initialize it, so care must be taken to avoid resetting states when upgrading chaincode.




## DRIVENET Chaincode

Similar to chaincode that would be exist for any supply chain network. Customized to take specific regulations in the car industry (and American laws) into account.



[Next: Starting DRIVENET](../DriveNetSample/StartingDRIVENET.md)
