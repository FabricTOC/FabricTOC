# Channels

## What is a channel?

In many networks, it may be preferable -- or even legally necessary -- for transactions to not be seen by every participant in the network nor written to every ledger. For that reason Hyperledger Fabric was designed with the ability to create *channels*, a method that allows two or more participants to transact privately.

As a practical matter, channels exist as private messaging paths through the ordering service (these transactions are also encrypted). Crucially, these transactions are written to a separate ledger that exists just for that channel, which means that the consortia members will have a separate ledger for every channel they belong to.

## Channel Creation Policy

The ordering system channel needs to define ordering parameters and consortiums for creating channels. There must be exactly one ordering system channel for an ordering service, and it is the first channel to be created (or more accurately bootstrapped). Note that any member with read access to the ordering system channel may see all channel creations, so this channel’s access should be restricted.

Channel configuration has the following important properties:

    1. Versioned: All elements of the configuration have an associated version which is advanced with every modification. Further, every committed configuration receives a sequence number.

    2. Permissioned: Each element of the configuration has an associated policy which governs whether or not modifications to that element are permitted (and by who, if anyone). Anyone with a copy of the previous configtx can therefore verify the validity of a new config based on those policies.

    3. Hierarchical: A root configuration group contains sub-groups, and each group of the hierarchy has associated values and policies. These policies can take advantage of the hierarchy to derive policies at one level from policies of lower levels.

## Defining a Channel

When the orderer receives a CONFIG_UPDATE for a channel which does not exist, the orderer assumes that this must be a channel creation request and performs the following.

    1. The orderer identifies the consortium which the channel creation request is to be performed for. It does this by looking at the Consortium value of the top level group.

    2. The orderer verifies that the organizations included in the Application group are a subset of the organizations included in the corresponding consortium and that the ApplicationGroup is set to version 1.

    3. The orderer verifies that if the consortium has members, that the new channel also has application members (creation consortiums and channels with no members is useful for testing only).

    4. The orderer creates a template configuration by taking the Orderer group from the ordering system channel, and creating an Application group with the newly specified members and specifying its mod policy to be the Channel Creation Policy as specified in the consortium config. Note that the policy is evaluated in the context of the new configuration, so a policy requiring ALL members would require signatures from all the new channel members, not all the members of the consortium.

    5. The orderer then applies the CONFIG_UPDATE as an update to this template configuration. Because the CONFIG_UPDATE applies modifications to the Application group (its version is 1), the config code validates these updates against the ChannelCreationPolicy. If the channel creation contains any other modifications, such as to an individual org’s anchor peers, the corresponding mod policy for the element will be invoked.

    6. The new CONFIG transaction with the new channel config is wrapped and sent for ordering on the ordering system channel. After ordering, the channel is created.

It is recommended never to define an Application section inside of the ordering system channel genesis configuration, but may be done for testing.

## Updating a Channel

When the CONFIG_UPDATE is received, the orderer computes the resulting CONFIG by doing the following:

    1. Verifies the channel_id and read_set. All elements in the read_set must exist at the given versions.

    2. Computes the update set by collecting all elements in the write_set which do not appear at the same version in the read_set.

    3. Verifies that each element in the update set increments the version number of the element update by exactly 1.

    4. Verifies that the signature set attached to the ConfigUpdateEnvelope satisfies the mod_policy for each element in the update set.

    5. Computes a new complete version of the config by applying the update set to the current config.

    6. Writes the new config into a ConfigEnvelope which includes the CONFIG_UPDATE as the last_update field and the new config encoded in the config field, along with the incremented sequence value.

    7. Writes the new ConfigEnvelope into a Envelope of type CONFIG, and ultimately writes this as the sole transaction in a new configuration block.

When the peer (or any other receiver for Deliver) receives this configuration block, it should verify that the config was appropriately validated by applying the last_update message to the current config and verifying that the orderer-computed config field contains the correct new configuration.

*Note: if we're going to use the information in these lists, they really must become paragraphs. I'm leaving them as lists for now in case we decide to not use this information or to add other information.*

## DRIVENET Channels

When DRIVENET is first bootstrapped, the only channel will be the system channel containing the two organizations: Michell and Regal. This system channel will be updated when Cecil's joins the network (since these three members will all transact with each other on the system channel).

The first private channel creation will occur after Faster Autos joins the network. Because they are getting a special price to sell Regal cars, they'll join a channel with Regal and Regal alone (to ensure that Cecil's doesn't find out about Faster Auto's special price, and because there is no reason for Mitchell to be involved).

[Next: Peers](./Peers.md)
