# <a name="PeerCommand"></a> Peer Command

The `peer` command allow administrators to interact with a peer.

## Syntax

The `peer` command has different commands within it:

```
peer [command]
```
specifically
```
peer chaincode
peer channel     
peer logging     
peer node        
peer version     
peer
```

These commands separate the different functions provided by a peer into their own category. For example, use the `peer chaincode` command to perform smart contract operations on the peer, or the `peer channel` command to perform channel related operations.

Within each command there are many different options available, and because of this, each command is described in its own topic. Follow the [links below](#reference) to understand these commands in more detail.

If a command option is not specified then the `peer` command will return some help text.

### Peer flags

The `peer` command also has a set of associated flags :

```
peer [flags]
```
as follows
```
peer --help
peer --logging-level <string>     
peer --test.coverprofile <string>     
peer --version   
```

These flags describe more information about the peer. A command option is not necessary.

#### Flag details

* `--help`

Use this flag to get brief help text for the `peer` command. The `help` flag can often be used at different levels to get some help text for an individual command, or even command option. See individual commands for more detail.

* `--logging-level <string>`

Use this flag to set the logging level for the peer.

* `--test.coverprofile <string>`

Use this flag to ...? TBC

* `--version`

Use this flag to determine the build version for the peer.  This flag provides a set of detailed information on how the peer was built.  See the reference topic [Peer version information](./Reference/Peer/VersionInfo.md) to understand the version information in detail.

## Related Concepts
+ [Peers](./KeyConcepts/Peers/Peers.md)

## Related Tasks

## <a name=reference></a> Related Reference
+ [`peer chaincode` command](./PeerChaincodeCommand.md)
+ [`peer channel` command](./PeerChannelCommand.md)
+ [`peer logging` command](./PeerLoggingCommand.md)
+ [`peer node` command](./PeerNodeCommand.md)
+ [`peer version` command](./PeerVersionCommand.md)
