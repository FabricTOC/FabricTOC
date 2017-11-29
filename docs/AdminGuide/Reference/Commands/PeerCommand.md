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
```

These commands separate the different functions provided by a peer into their own category. For example, use the `peer chaincode` command to perform smart contract operations on the peer, or the `peer channel` command to perform chanel related peer operations.

Within each command there are many different options available, and because of this, a separate topic covers each command. Follow the [links below](#reference) to understand these commands in detail.

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

These flags are used to understand more about the peer. Notice that a command is not necessary. These flags are described in more detail [below](#flags)

## <a name=commands></a> Peer Commands

### `chaincode` subcommand

### `channel` subcommand

### `logging` subcommand

### `node` subcommand

### `version` subcommand

## <a name=flags></a>Peer Flags


## Related Concepts
+ [Peers](./KeyConcepts/Peers/Peers.md)

## Related Tasks

## <a name=reference></a> Related Reference
+ [`peer chaincode` command](./PeerChaincodeCommand.md)
+ [`peer channel` command](./PeerChannelCommand.md)
+ [`peer logging` command](./PeerLoggingCommand.md)
+ [`peer node` command](./PeerNodeCommand.md)
+ [`peer version` command](./PeerVersionCommand.md)
