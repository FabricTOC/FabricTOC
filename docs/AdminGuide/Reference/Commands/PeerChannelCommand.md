# <a name="PeeChannelCommand"></a> `peer channel` command

The `peer channel` command allow administrators to perform channel related operations on a peer. Use this command when you want to perform channel related blockchain on a peer -- such as joining a channel.

## Syntax

The `peer channel` command has different commands within it:

```
peer channel [command]
```
as follows
```
peer channel create      
peer channel fetch       
peer channel join        
peer channel list        
peer channel update      
```

These commands relate to the different channel operations that are relevant to a peer. For example, use the `peer channel join` command to join a peer to a channel, or the `peer channel list` command to show the channels to which a peer is joined.

Within each command there are many different options available and because of this each command is described in its own topic. Follow the [links below](#reference) to understand these individual commands in more detail.

### `peer channel` flags

The `peer channel` command also has a set of associated flags.

```
peer channel [flags]
```
as follows
```
peer channel --cafile <string>    
peer channel --orderer <string>   
peer channel --tls                
```

These flags relate to all `peer channel` commands. Each of these commands also has its own set of flags, and these are described in the relevant [peer command reference below](#reference).

The global `peer` command flags also apply as described in the [`peer command`](./PeerCommand.md#flags).

#### <a name=flags> </a> Flag details

+ `--cafile <string>`

  a fully qualified path to orderer certificates.

* `--orderer <string>`

  the fully qualified IP address and port of the orderer being communicated with for this channel operation.  

* `--tls`

  Use this flag to enable TLS communications for the `peer channel` command. The certificates specified with `--cafile` will be used for TLS communications to authenticate the connected orderer.

## Usage

Here's some examples using the different available flags on the `peer` command.

* `--help` flag

  ```
  peer --help

  Usage:
    peer [flags]
    peer [command]

  Available Commands:
    chaincode   Operate a chaincode: install|instantiate|invoke|package|query|signpackage|upgrade.
    channel     Operate a channel: create|fetch|join|list|update.
    logging     Log levels: getlevel|setlevel|revertlevels.
    node        Operate a peer node: start|status.
    version     Print fabric peer version.

  Flags:
        --logging-level string       Default logging level and overrides, see core.yaml for full syntax
    -v, --version                    Display current version of fabric peer server

  Use "peer [command] --help" for more information about a command.
  ```  

* `--version` flag

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
+ [Peers](../../KeyConcepts/Peers/Peers.md)

## <a name=reference></a> Related Reference

+ [`peer channel create` command](./PeerChannelCreateCommand.md)
+ [`peer channel fetch` command](./PeerChannelFetchCommand.md)
+ [`peer channel join` command](./PeerChannelJoinCommand.md)
+ [`peer channel list` command](./PeerChannelListCommand.md)
+ [`peer channel update` command](./PeerChannelUpdateCommand.md)
