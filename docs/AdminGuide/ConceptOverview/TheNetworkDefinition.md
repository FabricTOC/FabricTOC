# The Network Definition

It's common to think of a system as being comprised of *things*. If you imagine a car -- to use our running example -- as being a system, for example, you can see that it consists of a series of components whose functions are rigid and defined. Transmissions are designed and built for one job. They can't take the place of a fuel pump, which itself can't take the place of a radiator.   

That kind of system is known as a "type" system in computer science. Components are created and designed and "plugged in", whether physically or digitally, and the system is designed to recognize types and react to them in a certain way (structuring the data they produce, for example).  

Fabric networks are different. Instead of a series of *things* with set natures, the components in a network are defined through their **permissions** (what they are allowed to do), which is itself a function of their **identity**. We don't mean "identity" here in the sense that a name is an identity. But rather identity in the sense that a component can verify that it is itself (that it has the right public/private key pair) and was given certain rights and responsibilities over certain network functions (being able to endorse a transaction, for example, or to administrate an orderer) when it joined the network.  

At a fundamental level, then, there is really no such thing as a "peer" or an "application" or anything else. The network does not recognize "peer" as a valid designation that comes with rights and functionalities. The network only cares about permissions which it validates by checking the identity of whatever network address is trying to do something.

The interaction of these permissions and identities -- which we collectively call "policies" -- is the true nature of the network definition, to the extent that it is possible to define a network only by defining the variables in that network (block size, what constitutes a "version", etc) and the policies without any running processes at all!

Note: We still use terms like "users" and "peers" -- and will use them across this guide -- because it makes the concepts easier to understand. But it's important to remember that policies and permissions are what is king and that at a low level these terms are only colloquialisms. The "components" themselves are only addresses with identities that confer permissions.

## The resources in a network definition

Network definitions have a recursive structure based on the concept of "groups within groups." This is, as we've just discussed, a policy structure rather than a physical structure.

All groups have (at every level):   

  1. A **version**. It's update level. Every time any  gets updated we get a new version. This applies to anything that can get updated. When it's updated, it gets a new version. Critical because you have to be careful. Rules about what constitutes a version. Non trivial. Need more info here. At what level what version needs to be upgraded. See existing docs.
  2. A **value**. The hashing algorithm being used, for example. Or the maximum block size or consensus type being used.
  3. A **policy**. Describes who can do what in that group.
  4. **Groups**. This is what gives the network its recursive structure.
  5. A **mod_policy**. What allows the policies to be changed. Every part of the group has its own mod_policy.

These are the valid kinds of groups:

  1. The network. IE, the system channel.
  2. Channels.
  3. Nodes (for example, peers and orderers). These are just addresses.
  4. Consortia (consortiums).
  5. Organizations. Application groups.

What does the network definition actually *define*.

A set of policies, which control access to resources.

A set of peers, which host the ledger and smart contracts.

An ordering service, the network administration point.

A set of channels, which partition the network for privacy.

A set of configurations, applying to different elements of the network.

A set of MSPs which provide a trust store for identities.

## The resources in DRIVENET

We'll talk more about all of the policies in the DRIVENET network when we actually bootstrap it. 



[-->Next](./OrganizationsinaNetwork.md)
