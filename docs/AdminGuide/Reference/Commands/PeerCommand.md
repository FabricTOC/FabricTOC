# <a name="PeerCommand"></a>`peer` command

## Description

The `peer` command allows administrators to interact with a peer. Use this command when you want to perform peer operations such as deploying a smart contract chaincode, or joining a channel.

## Syntax

The `peer` command has different subcommands within it:

```
peer [subcommand]
```
as follows
```
peer chaincode
peer channel     
peer logging     
peer node        
peer version     
peer
```

These subcommands separate the different functions provided by a peer into their own category. For example, use the `peer chaincode` command to perform smart contract chaincode operations on the peer, or the `peer channel` command to perform channel related operations.

Within each command there are many different options available and because of this each command is described in its own topic. Follow the [links below](#reference) to understand these individual commands in more detail.

If a command option is not specified then `peer` will return some high level help text as described in in the `--help` flag [below](#flags).

### `peer` flags

The `peer` command also has a set of associated flags :

```
peer [flags]
```
as follows

These flags provide more information about a peer, and are designated *global* because they can be used at any command level. For example `--help` will provide help on the command or command option to which it is applied:

```
peer --help
peer channel --help
peer channel list --help
```

#### <a name=flags> </a> Flag details

+ `--help`

  Use `help` to get brief help text for the `peer` command. The `help` flag can often be used at different levels to get individual command help, or even a help on a command option. See individual commands for more detail.

* `--logging-level <string>`

  Use this flag to set the logging level for the peer.  This flag only has meaning on the individual commands. It does not apply at the top level.

  This command is overridden by the `CORE_LOGGING_LEVEL` environment variable if it is set.  A full list of peer environment variables is described in the [peer environment variables reference topic](../Advanced/Peer/PeerEnvironmentVariables.md).

* `--version`

  Use this flag to determine the build version for the peer.  This flag provides a set of detailed information on how the peer was built.

  See the reference topic [Peer version information](../Advanced/Peer/VersionInfo.md) to understand the version information in detail.

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

## Related Tasks

+ [Determining a peer's version](../../AdminTasks/Peer/PeerVersion.md)

## <a name=reference></a> Related Reference

+ [`peer chaincode` command](./PeerChaincodeCommand.md)
+ [`peer channel` command](./PeerChannelCommand.md)
+ [`peer logging` command](./PeerLoggingCommand.md)
+ [`peer node` command](./PeerNodeCommand.md)
+ [`peer version` command](./PeerVersionCommand.md)   
+ [Peer environment variables](../Advanced/Peer/PeerEnvironmentVariables.md)    
