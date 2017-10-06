# <a name="HowOrganized"></a> How this section is organized

This section lists all of the tasks that an administrator can perform.  
We have grouped these tasks together according to topics. For example, you'll find all the commands relating to Certificate Authorities under the same section, all the tasks relating to Peers under another section, and so on.

Within any of these sections, we order the tasks in the same way as you'd expect to normally issue them, if that's possible.  For example, [Starting a Peer](./PeerTasks.md#StartingPeer) is listed before [Joining a Channel](./PeerTasks.md#JoiningChannel).

For each task, we'll show the generic form of the command, for example

`fabric-ca-server start --ca.certfile <certfile> --ca.keyfile <keyfile> -b <adminUser>:<adminPassword> -d`

where

`<certfile>` is the full path to public certificate of the CA

`<keyfile>` is the full path to the private key file of the CA

`<adminUser>` is the user name of the CA administrator

`<adminPassword` is the password of the CA administrator

Where possible, we'll also show an example command from the DRIVENET sample.

[-->Certificate Authority Tasks](./CATasks.md)
