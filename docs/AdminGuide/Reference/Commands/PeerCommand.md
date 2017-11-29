# <a name="PeerCommand"></a> Peer Command

The `peer` command allow administrators to interact with a peer.

## Syntax

The `peer` command has different commands within it:

```
peer [command]
```
as follows
```
peer chaincode
peer channel     
peer logging     
peer node        
peer version     
peer [no command]
```

These commands separate the different functions provided by a peer into their own category. For example, use the `peer chaincode` command to perform smart contract operations on the peer, or the `peer channel` command to perform channel related operations.

Within each command there are many different options available and because of this each command is described in its own topic. Follow the [links below](#reference) to understand these commands in more detail.

If a command option is not specified then the `peer` will return some high level help text about the command.

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

These flags describe more information about the peer. Notice that a command option is not necessary when a flag is used.

#### Flag details

* `--help`

  Use `help` to get brief help text for the `peer` command. The `help` flag can often be used at different levels to get individual command help, or even a help on a command option. See individual commands for more detail.

* `--logging-level <string>`

  Use this flag to set the logging level for the peer. TBC

* `--test.coverprofile <string>`

  Use this flag to ...? TBC

* `--version`

  Use this flag to determine the build version for the peer.  This flag provides a set of detailed information on how the peer was built. See the reference topic [Peer version information](./Reference/Peer/VersionInfo.md) to understand the version information in detail.

  Here's an example of the output

```
peer --version

peer:
 Version: 1.0.4
 Go version: go1.7.5
 OS/Arch: linux/amd64
 Chaincode:
  Base Image Version: 0.3.2
  Base Docker Namespace: hyperledger
  Base Docker Label: org.hyperledger.fabric
  Docker Namespace: hyperledger
```


## Related Concepts
+ [Peers](./KeyConcepts/Peers/Peers.md)

## Related Tasks

## <a name=reference></a> Related Reference
+ [`peer chaincode` command](./PeerChaincodeCommand.md)
+ [`peer channel` command](./PeerChannelCommand.md)
+ [`peer logging` command](./PeerLoggingCommand.md)
+ [`peer node` command](./PeerNodeCommand.md)
+ [`peer version` command](./PeerVersionCommand.md)
