# The Resources in a Network Definition

*Still a little unsure what this doc is about*

All groups have (at every level):

  1. A **version**. It's update level. When a component gets updated it gets a new version number. This applies to anything that can get updated. When it's updated, it gets a new version. Critical because you have to be careful. Rules about what constitutes a version. Non trivial. *Need more info here.*
  2. A **value**. The hashing algorithm being used, for example. Or the maximum block size or consensus type being used.
  3. A **policy**. Describes who can do what in that group.
  4. **Groups**. This is what gives the network its recursive structure.
  5. A **mod_policy**. What allows the policies to be changed. Every component of a group has its own mod_policy.

These are the valid kinds of groups:

  1. Application.
  2. Orderer.
  3. Consortium.

Below that channel level. Channels are not groups but they're all defined within the root of a channel.

What does the network definition actually *define*.

A set of policies, which control access to resources.

A set of peers, which host the ledger and smart contracts.

An ordering service, the network administration point.

A set of channels, which partition the network for privacy.

A set of configurations, applying to different elements of the network.

A set of MSPs which provide a trust store for identities.
