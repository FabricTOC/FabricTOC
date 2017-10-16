# The Network Definition

We tend to think of systems as being comprised of *things*. You can think of a car, for example, as consisting of a series of components whose functions are rigid and defined. Transmissions are designed to fulfill an explicit function. They can't take the place of a fuel pump, which itself can't take the place of a radiator.  

In the world of computer science, this is known as a "type" system. Components are created and designed and "plugged in", whether physically or digitally, and the system they're a part of has likewise been designed to recognize and react to types.

Fabric networks are different. Instead of a series of *things* with set natures, the components in a network are defined through their **permissions** (what they are allowed to do), which is itself a function of their **identity**. We don't mean "identity" here in the sense that a name is an identity. But rather identity in the sense that a component can verify that it is itself (that it has the right public/private key pair) and was given certain rights and responsibilities over certain network functions (being able to endorse a transaction, for example, or to administrate an orderer) when it joined the network.  

At a fundamental level, then, there is really no such thing as a "peer" or an "application" or anything else. The network does not recognize "peer" as a valid designation that comes with rights and functionalities. The network only cares about permissions which it validates by checking the identity of whatever network address is trying to do something.

The interaction of these permissions and identities -- which we collectively call "policies" -- is the true nature of the network definition, to the extent that it is possible to define a network only by defining the variables in that network (block size, what constitutes a "version", etc) and the policies *without any running processes at all*!

Note: We still use terms like "users" and "peers" -- and will use them across this guide -- because it makes the concepts easier to understand. But it's important to remember that policies and permissions are what is king and that at a low level these terms are only colloquialisms. The "components" themselves are only addresses with identities that confer permissions.


[-->Next](./OrganizationsinaNetwork.md)
