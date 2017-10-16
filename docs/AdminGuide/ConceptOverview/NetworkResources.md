# The Resources in a Network definitions

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
