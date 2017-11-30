# <a name="PeeChannelFetchCommand"></a> `peer channel fetch` command

The `peer channel fetch` command allows administrators to fetch channel transaction blocks from the network orderer. The retrieved blocks will typically contain user transactions. The retrieved blocks can also contain configuration transactions such as the initial genesis block for the channel or any subsequent channel configuration update.

The peer must have joined the channel, and have read access to it, in order for the command to complete successfully.

## Syntax

The `peer channel fetch` command has the following syntax:

```
peer channel fetch <newest|oldest|config|(block number)> [flags]
```

where

* `newest`

  returns the most recent channel block available to the network orderer. This may be a user transaction block or a configuration transaction.

  This option will also return the block number of the most recent transaction.

* `oldest`

  returns the oldest channel block available to the network orderer. This may be a user transaction block or a configuration transaction.

  This option will also return the block number of the oldest available transaction.

* `config`

  returns the most recent channel configuration block available to the network orderer. This can only be a configuration transaction.

  This option will also return the block number of the most recent configuration transaction.

* `(block number)`

  returns the specified channel block. This may be a user transaction block or a configuration transaction.  

  Specifying 0 will result in the genesis block for this channel being returned, if it is still available to the network orderer.

  TBC: THE COMMAND DOES NOT COMPLETE IF THE (block number) IS TOO HIGH.

### `peer channel fetch` flags

  The `peer channel fetch` command has the following command specific flags:

#### <a name=flags> </a> Flag details
* `--channelID <string>`

  the name of the channel for which the blocks are to be fetched from the network orderer.

The global `peer` command flags also apply as described in the [`peer command`](./PeerCommand.md#flags).

*  `--cafile`
* `--orderer`
* `--tls`

## Usage

Output from the `peer channel fetch` command is written to a file named according to the fetch options. It will be one of the following:

* `<channelID>_newest.block`
* `<channelID>_oldest.block`
* `<channelID>_config.block`
* `<channelID>_(block number).block`

Here's some examples using the different available flags on the `peer channel fetch` command.

* Using the `newest` option to retrieve the most recent channel block.

  ```
  peer channel fetch newest  -c drivenet.channel.001 --orderer orderer.example.com:7050

  2017-11-30 17:02:56.234 UTC [msp] GetLocalMSP -> DEBU 001 Returning existing local MSP
  2017-11-30 17:02:56.234 UTC [msp] GetDefaultSigningIdentity -> DEBU 002 Obtaining default signing identity
  2017-11-30 17:02:56.237 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
  2017-11-30 17:02:56.237 UTC [msp] GetLocalMSP -> DEBU 004 Returning existing local MSP
  2017-11-30 17:02:56.237 UTC [msp] GetDefaultSigningIdentity -> DEBU 005 Obtaining default signing identity
  2017-11-30 17:02:56.240 UTC [msp] GetLocalMSP -> DEBU 006 Returning existing local MSP
  2017-11-30 17:02:56.240 UTC [msp] GetDefaultSigningIdentity -> DEBU 007 Obtaining default signing identity
  2017-11-30 17:02:56.240 UTC [msp/identity] Sign -> DEBU 008 Sign: plaintext: 0AC9060A1B08021A0608C0F380D10522...DC7F80E9BEE612080A020A0012020A00
  2017-11-30 17:02:56.241 UTC [msp/identity] Sign -> DEBU 009 Sign: digest: D3F6C959BCFCD78B5895A466276C181EEA3B54C1CF8E8707238FE3A3D358F769
  2017-11-30 17:02:56.245 UTC [channelCmd] readBlock -> DEBU 00a Received block: 32
  2017-11-30 17:02:56.246 UTC [main] main -> INFO 00b Exiting.....

  ls -alt

  total 276
  drwxr-xr-x 2 root root   4096 Nov 30 16:17 .
  -rw-r--r-- 1 root root  13307 Nov 30 17:02 drivenet.channel.001_newest.block
  drwxr-xr-x 3 root root   4096 Nov 21 13:38 ..

  ```  

  You can see that the retrieved block is number 32.

* Using the `(block number)` option to retrieve a specific block -- in this case, block number 16.

  ```
  peer channel fetch 16  -c drivenet.channel.001 --orderer orderer.example.com:7050

  2017-11-30 17:08:12.039 UTC [msp] GetLocalMSP -> DEBU 001 Returning existing local MSP
  2017-11-30 17:08:12.039 UTC [msp] GetDefaultSigningIdentity -> DEBU 002 Obtaining default signing identity
  2017-11-30 17:08:12.042 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
  2017-11-30 17:08:12.042 UTC [msp] GetLocalMSP -> DEBU 004 Returning existing local MSP
  2017-11-30 17:08:12.042 UTC [msp] GetDefaultSigningIdentity -> DEBU 005 Obtaining default signing identity
  2017-11-30 17:08:12.042 UTC [msp] GetLocalMSP -> DEBU 006 Returning existing local MSP
  2017-11-30 17:08:12.042 UTC [msp] GetDefaultSigningIdentity -> DEBU 007 Obtaining default signing identity
  2017-11-30 17:08:12.042 UTC [msp/identity] Sign -> DEBU 008 Sign: plaintext: 0AC9060A1B08021A0608FCF580D10522...B092120C0A041A02081012041A020810
  2017-11-30 17:08:12.042 UTC [msp/identity] Sign -> DEBU 009 Sign: digest: CD6F4ADB7E00E79E4FADBE627CBE7CAA6F2A4471A9A0BE780CD4BE65AF8B96DE
  2017-11-30 17:08:12.046 UTC [channelCmd] readBlock -> DEBU 00a Received block: 16
  2017-11-30 17:08:12.046 UTC [main] main -> INFO 00b Exiting.....

  ls -alt

  total 276
  drwxr-xr-x 2 root root   4096 Nov 30 16:17 .
  -rw-r--r-- 1 root root  10474 Nov 30 17:08 drivenet.channel.001_16.block
  -rw-r--r-- 1 root root  13307 Nov 30 17:02 drivenet.channel.001_newest.block
  drwxr-xr-x 3 root root   4096 Nov 21 13:38 ..

  ```  

    You can see that the retrieved block is number 16.

For configuration blocks, the file can be formatted using the [`configtxlator` command](../Config/ConfigtxlatorCommand.md). If you'd like to see an example of a formatted block, then refer to the [Formated configuration block](../Config/FormattedConfigBlock.md) or [Formatted user transaction block ](../Config/FormattedUserTransactionBlock.md) reference topics, respectively.

TBC: HOW TO FORMAT USER TRANSACTION BLOCKS?

## Related Concepts
* [Peers](../../KeyConcepts/Peers/Peers.md)
* [Channels](../../KeyConcepts/Channels/Channels.md)
* [Orderers](../../KeyConcepts/Orderers/Orderers.md)
* [Configuration](../../KeyConcepts/Configuration/Configuration.md)

## <a name=reference></a> Related Reference
* [`peer channel create` command](./PeerChannelCreateCommand.md)
* [`peer channel fetch` command](./PeerChannelFetchCommand.md)
* [`peer channel join` command](./PeerChannelJoinCommand.md)
* [`peer channel list` command](./PeerChannelListCommand.md)
* [`peer channel update` command](./PeerChannelUpdateCommand.md)
* [`configtxlator` command](../Config/ConfigtxlatorCommand.md)
* [Formated configuration block](../Config/FormattedConfigBlock.md)
* [Formatted user transaction block ](../Config/FormattedUserTransactionBlock.md)
