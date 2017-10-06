# <a name="HowOrganized"></a> How this section is organized

We have group the tasks in this section in groups that relate to the conceptual model of Hyperledger Fabric. For example, you'll find all the commands relating to Certificate Authorities under the same section, all the tasks relating to Peers under another section, and so on.

With any of these sections, we'll order the tasks in the same way as you'd expect to issue them, if that's possible.  For example, [Starting a Peer](./PeerTasks.md#StartingPeer) is listed before [Joining a Channel](./PeerTasks.md#JoiningChannel).

For each task, we'll show the generic form of the command, for example

`fabric-ca-server start --ca.certfile <certfile> --ca.keyfile <keyfile> -b <adminUser>:<adminPassword> -d`

where

`<certfile>` is the full path to public certificate of the CA
`<keyfile>` is the full path to the private key file of the CA
`<adminUser>` is the user name of the CA administrator
`<adminPassword` is the password of the CA administrator

Where possible, we'll also show an example command from the DRIVENET sample.

[-->Certificate Authority Tasks](./CATasks.md)
