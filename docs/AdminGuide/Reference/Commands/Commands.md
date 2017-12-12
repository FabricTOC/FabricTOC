# <a name="HowOrganized"></a> How this section is organized

This topic lists all of the commands that an administrator can perform. We have
grouped these commands together according to topic with the same organizational
model as the Key Concepts section. For example, you'll find all the commands
relating to Certificate Authorities under the same section, all the tasks
relating to Peers under another section, and so on.

For each command, we'll show the general form of the command, for example

`fabric-ca-server start --ca.certfile <certfile> --ca.keyfile <keyfile> --b <adminUser>:<adminPassword> --d`

options:

`--ca.certfile` is the full path to public certificate of the CA

`--ca.keyfile` is the full path to the private key file of the CA

`--b` is the user name and password of the CA administrator, specified as <adminUser>:<adminPassword>

`--d`

Where possible, we'll also show an example command from the DRIVENET sample.

[-->Peer Command](./PeerCommand.md)
