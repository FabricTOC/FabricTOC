# Chaincode and Smart Contracts

## What is Chaincode?

In any group of businesses, rules must be established that govern not just the general roles and responsibilities of the members of the group, but the specific rules that govern individual transactions.

In the past, these rules were established by paper contracts and disputes were resolved by fleets of lawyers. Blockchains allow these rules to be digitized into what are called "smart contracts", which are **programs -- comprised of business logic -- that have been agreed to by the members of a channel**. This business logic **defines and enforces the rules for reading or altering the ledger for that channel**. We'll talk more about why smart contracts exist within the scope of a channel -- rather than the network -- in a minute. 

In Hyperledger Fabric, smart contracts are written in **chaincode**, to the point where the terms are often use interchangably. But "chaincode" actually encompasses more than this business logic -- system chaincode, for example, which we'll talk about later.

Chaincodes are not just important, they're necessary -- **reading or writing to the ledger does not happen without them**. This makes chaincode of particular interest to **application developers**, though the lifecycle of a chaincode -- as well as the scope of system chaincode (more on this later) -- is also of importance to network and channel administrators.

The rules that can be defined with chaincodes cover a huge number of possible functions, from comparatively simple tasks like storing and managing endorsement policies (more on these later) to -- in the case of more complex chaincodes -- automatically invoking transactions when certain conditions have been met. As a result, a channel will sometimes have more than one chaincode instatiated (i.e. "running") on it.

Let's say the channel you're on involves the buying and selling of cars. There are 20 peers on this channel. A few peers belong to an insurance company, others belong to government regulators, with the rest of the peers representing the car businesses. In addition to the system chaincode (which we'll talk about later), the chaincode(s) would define, in part:

  1. **The initial state of the car market** (represented by a set of key/value pairs). This would be instantiated on the channel and installed on all of the peers when they join the channel and on any new peer joining the channel.

  2. **Defining certain parameters**. The price of shipping a car, for example, or perhaps the price of cars themselves. These parameters can -- and in many business use cases will be -- updated over time. We'll talk more about the process for updating chaincode later.

  3. **The endorsement policy**. This defines which peers need to endorse (to sign off, in other words) on a transaction. These endorsement policies can be specific or general, meaning that they can be written to say that an explicitly defined peer or peers have to sign off on a transaction or that only a certain **number** of peers (15 of the 20 total peers, to use our car example) have to sign off. It can also be written as a combination of these (specifying for example that the DMV has to sign any transaction **and** that any 10 of the 15 car dealership peers have to sign it). In general, chaincodes specifying an endorsement policy will only be installed on peers involved in endorsements on that channel (more on this later).

  4. **Queries and updates possible using the chaincode**. Chaincodes can be written as broadly or as narrowly as a developer wants or needs them to be. It's possible, for example, to write a chaincode that only permits a simple query of the entire ledger and allows no arguments (variables) to be passed along with it. More often, a chaincode will allow multiple different kinds of queries and updates to be written to the ledger by changing these arguments. For example, a chaincode can be written with a function called `CreateCAR` that allows cars to be put on the ledger (there's more to it than just the chaincode, but forget about that for a minute). The arguments -- specifying the make, model, color, VIN number, or other information about the car -- would be passed along with `CreateCAR` (in an order defined in the chaincode, preventing "black" from being passed as the "year" of the car, for example) and written to the ledger. It's important to note that arguments can always be passed along with ledger **updates**, but if the storage format is binary or some other non-rich format, it will be impossible to make rich **queries** (such as asking the ledger to return every "black" car that's been created). For more information on ledgers and storage formats, see the documentation on [ledgers](./TheLedger.md). **Whatever the storage format, once a functionality has been written into a chaincode, application developers can leverage it to allow end users to perform a variety of tasks using the application**.

Crucially, because chaincodes must go through the endorsement process before they're instantiated on a channel, invocations proposed by a chaincode are both automatic and binding, bypassing the normal signing and verifying a typical transaction has to go through. This automation is what allows chaincodes to increase the efficiency of business practices, permitting the conditions of a deal -- whether a product has been delivered on time, for example -- to correspond automatically to a particular (agreed upon) price.

Now that you can see the basics of what chaincodes are and the role they play, let's see how they interact with different parts of a Fabric network.

## Chaincode and the Ledgers

Chaincodes manage access to the ledger by defining which Hyperledger Fabric APIs can be accessed and how they can be accessed by applications.







## Installing Chaincode

Fabric APIs allow for the packaging, installation, instantiation, and upgrading of chaincode on a channel's endorsing peers. Chaincodes run in secure Docker containers.

Before a chaincode can be installed, it must be packaged correctly. To see how this is done, refer to the [chaincode reference section](./ReferenceMaterial/ChaincodeReference.md).



The Hyperledger Fabric API enables interaction with the various nodes in a blockchain network -- the peers, orderers and MSPs -- and it also allows one to package, install, instantiate and upgrade chaincode on the endorsing peer nodes. The Hyperledger Fabric language-specific SDKs abstract the specifics of the Hyperledger Fabric API to facilitate application development, though it can be used to manage a chaincode’s lifecycle. Additionally, the Hyperledger Fabric API can be accessed directly via the CLI.

We provide four commands to manage a chaincode’s lifecycle: package, install, instantiate, and upgrade. In a future release, we are considering adding stop and start transactions to disable and re-enable a chaincode without having to actually uninstall it. After a chaincode has been successfully installed and instantiated, the chaincode is active (running) and can process transactions via the invoke transaction. A chaincode may be upgraded any time after it has been installed.

Chaincodes physically run in Docker containers and function at the channel level. Chaincode must also be installed on the endorsing peers in a channel.

Channels can have multiple chaincodes/smart contracts functioning on it simultaneously and every endorsing peer node of a channel that will run your chaincode must have it installed.

If a peer is not endorsing it will still write transactions to its copy of the channel ledger. It will not be executing the chaincode. However, they can still validate and commit the transactions to the ledger.

Chaincode should only be installed on endorsing peer nodes of the owning members of the chaincode to protect the confidentiality of the chaincode logic from other members on the network.





## Instantiating Chaincode

The creator of the instantiation transaction of the chaincode on a channel is validated against the instantiation policy of the chaincode.

A chaincode package that was signed at creation can be handed over to other owners for inspection and signing. The workflow supports out-of-band signing of chaincode package.

If the instantiation policy is not specified, the default policy is any MSP administrator of the channel.


Happens at the channel level (though the same chaincode can be installed on multiple channels, it's actions are kept isolated -- not unlike any program that's been installed on different computers). This instantiation is when the chaincode is written to the ledger. Must have admin rights over that channel to instantiate. Only happens once.

The instantiate transaction invokes the lifecycle System Chaincode (LSCC) to create and initialize a chaincode on a channel. This is a chaincode-channel binding process: a chaincode may be bound to any number of channels and operate on each channel individually and independently. In other words, regardless of how many other channels on which a chaincode might be installed and instantiated, state is kept isolated to the channel to which a transaction is submitted.

The creator of an instantiate transaction must satisfy the instantiation policy of the chaincode included in SignedCDS and must also be a writer on the channel, which is configured as part of the channel creation. This is important for the security of the channel to prevent rogue entities from deploying chaincodes or tricking members to execute chaincodes on an unbound channel.

For example, recall that the default instantiation policy is any channel MSP administrator, so the creator of a chaincode instantiate transaction must be a member of the channel administrators. When the transaction proposal arrives at the endorser, it verifies the creator’s signature against the instantiation policy. This is done again during the transaction validation before committing it to the ledger.

The instantiate transaction also sets up the endorsement policy for that chaincode on the channel. The endorsement policy describes the attestation requirements for the transaction result to be accepted by members of the channel.


## Upgrading Chaincode

Has a version.

Attribute based access control (ABAC) for chaincode, using attributes included in Fabric CA generated certificates. This provides another means of enforcing access control in chaincode. FAB-5346

A chaincode may be upgraded any time by changing its version, which is part of the SignedCDS. Other parts, such as owners and instantiation policy are optional. However, the chaincode **name** must be the same; otherwise it would be considered as a totally different chaincode.

Prior to upgrade, the new version of the chaincode must be installed on the required endorsers. Upgrade is a transaction similar to the instantiate transaction, which binds the new version of the chaincode to the channel. Other channels bound to the old version of the chaincode still run with the old version. In other words, the upgrade transaction only affects one channel at a time, the channel to which the transaction is submitted.

There’s one subtle difference with the instantiate transaction: the upgrade transaction is checked against the current chaincode instantiation policy, not the new policy (if specified). This is to ensure that only existing members specified in the current instantiation policy may upgrade the chaincode.

Since multiple versions of a chaincode may be active simultaneously, the upgrade process doesn’t automatically remove the old versions, so users must manage this for the time being.

During an upgrade, the chaincode Init function is called to perform any data related updates or re-initialize it, so care must be taken to avoid resetting states when upgrading chaincode.

## System Chaincode

System chaincodes are specialized chaincodes that run as part of the peer process as opposed to user chaincodes that run in separate docker containers. As such they have more access to resources in the peer and can be used for implementing features that are difficult or impossible to be implemented through user chaincodes. Examples of System Chaincodes are ESCC (Endorser System Chaincode) for endorsing proposals, QSCC (Query System Chaincode) for ledger and other fabric related queries and VSCC (Validation System Chaincode) for validating a transaction at commit time respectively.

Unlike a user chaincode, a system chaincode is not installed and instantiated using proposals from SDKs or CLI. It is registered and deployed by the peer at start-up.

System chaincodes can be linked to a peer in two ways: statically and dynamically using Go plugins.

A system chaincode is a program written in Go and loaded using the Go plugin package.

Existing chaincodes such as the QSCC can also serve as templates for certain features - such as access control - that are typically implemented through system chaincodes. The existing system chaincodes also serve as a reference for best-practices on things like logging and testing.


Peers come loaded with certain chaincode functions. These cover a spectrum of behaviors typical of a peer in a Fabric network and allow the peer to

System chaincode functions similarly to other chaincodes except that it runs within the peer process rather than in an isolated container. Therefore, system chaincode is built into the peer executable and doesn’t follow the same lifecycle. In particular, install, instantiate and upgrade do not apply to system chaincodes.

The purpose of system chaincode is to shortcut gRPC communication cost between peer and chaincode, and tradeoff the flexibility in management. For example, a system chaincode can only be upgraded with the peer binary. It must also register with a fixed set of parameters compiled in and doesn’t have endorsement policies or endorsement policy functionality.

System chaincode is used in Hyperledger Fabric to implement a number of system behaviors so that they can be replaced or modified as appropriate by a system integrator.

The current list of system chaincodes:

    1. LSCC Lifecycle system chaincode handles lifecycle requests described above.
    2. CSCC Configuration system chaincode handles channel configuration on the peer side.
    3. QSCC Query system chaincode provides ledger query APIs such as getting blocks and transactions.
    4. ESCC Endorsement system chaincode handles endorsement by signing the transaction proposal response.
    5. VSCC Validation system chaincode handles the transaction validation, including checking endorsement policy and multiversioning concurrency control.

Care must be taken when modifying or replacing these system chaincodes, especially LSCC, ESCC and VSCC since they are in the main transaction execution path. It is worth noting that as VSCC validates a block before committing it to the ledger, it is important that all peers in the channel compute the same validation to avoid ledger divergence (non-determinism). So special care is needed if VSCC is modified or replaced.

## How Chaincodes are Accessed and Manipulated

Applications use APIs to invoke chaincode, which is hosted in the network and identified by name and version.

Wide range of possible APIs that a chaincode can call. Not all are needed in every chaincode. Writing a chaincode is about figuring out which APIs you need and including them (and the relevant arguments you'll need).

Package shim provides APIs for the chaincode to access its state variables, transaction context and call other chaincodes. ChaincodeStub is an object passed to chaincode for shim side handling of APIs.

https://godoc.org/github.com/hyperledger/fabric/core/chaincode/shim



The Hyperledger Fabric API enables interaction with the various nodes in a blockchain network -- the peers, orderers and MSPs -- and it also allows one to package, install, instantiate and upgrade chaincode on the endorsing peer nodes. The Hyperledger Fabric language-specific SDKs abstract the specifics of the Hyperledger Fabric API to facilitate application development, though it can be used to manage a chaincode’s lifecycle. Additionally, the Hyperledger Fabric API can be accessed directly via the CLI.

We provide four commands to manage a chaincode’s lifecycle: package, install, instantiate, and upgrade. We'll talk about how to install, instantiate, and upgrade in this section, while we'll cover how to package chaincodes in the [reference section on chaincode][./ReferenceMaterial/ChaincodeReference.md].




[Next: Starting DRIVENET](../DriveNetSample/StartingDRIVENET.md)
