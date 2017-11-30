# <a name="PeeChannelCommand"></a> `peer channel` command

The `peer channel` command allows administrators to perform channel related operations on a peer -- such as joining a channel, or instantiating s smart contract chaincode.

## Syntax

The `peer channel` command has the following syntax:

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

### `peer channel` flags

Each `peer channel` command has different flags available to it, and because of this, each flag is described in the relevant command topic. Follow the [links below](#reference) to understand these individual commands in more detail.

The `peer channel` command also has a set of flags that relate to every `peer channel` command.

```
peer channel [flags]
```
as follows
```
peer channel --cafile <string>    
peer channel --orderer <string>   
peer channel --tls                
```

The global `peer` command flags also apply as described in the [`peer command`](./PeerCommand.md#flags).
* `--help`
* `--logging-level <string>`
* `--version`

#### <a name=flags> </a> Flag details

+ `--cafile <string>`

  a fully qualified path to a file containing PEM-encoded certificates for the orderer being communicated with.  

  TBC: CAN THERE BE MORE THAN ONCE CERTIFICATE, IF SO, HOW ARE THEY SEPARATED PER ORDERER?

* `--orderer <string>`

  the fully qualified IP address and port of the orderer being communicated with for this channel operation.  If the port is not specified, it will default to port 7050. An IP address must be specified if the `--orderer` flag is used.

* `--tls`

  Use this flag to enable TLS communications for the `peer channel` command. The certificates specified with `--cafile` will be used for TLS communications to authenticate the connected orderer.

## Usage

Here's some examples using the different available flags on the `peer channel` command.

* Using the `--orderer` flag to list the channels to which a peer is joined.

  ```
  peer channel list --orderer orderer.example.com:7050

  2017-11-30 12:07:51.317 UTC [msp] GetLocalMSP -> DEBU 001 Returning existing local MSP
  2017-11-30 12:07:51.317 UTC [msp] GetDefaultSigningIdentity -> DEBU 002 Obtaining default signing identity
  2017-11-30 12:07:51.321 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
  2017-11-30 12:07:51.323 UTC [msp/identity] Sign -> DEBU 004 Sign: plaintext: 0A8A070A5C08031A0C0897E9FFD00510...631A0D0A0B4765744368616E6E656C73
  2017-11-30 12:07:51.323 UTC [msp/identity] Sign -> DEBU 005 Sign: digest: D170CD2D6FEB04E49033B54B0AC53744991ADAA320C5733074BC5227BD19E863
  2017-11-30 12:07:51.335 UTC [channelCmd] list -> INFO 006 Channels peers has joined to:
  2017-11-30 12:07:51.335 UTC [channelCmd] list -> INFO 007 drivenet.channel.001
  2017-11-30 12:07:51.335 UTC [main] main -> INFO 008 Exiting.....
  ```  

  You can see that the peer joined to a channel called `drivenet.channel.001`.


## Related Concepts
+ [Peers](../../KeyConcepts/Peers/Peers.md)
+ [Channels](../../KeyConcepts/Channels/Channels.md)

## <a name=reference></a> Related Reference

+ [`peer channel create` command](./PeerChannelCreateCommand.md)
+ [`peer channel join` command](./PeerChannelJoinCommand.md)
+ [`peer channel list` command](./PeerChannelListCommand.md)
+ [`peer channel update` command](./PeerChannelUpdateCommand.md)
