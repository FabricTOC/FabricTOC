# Determining the Version of a Peer

It is often helpful to determine the version of a peer -- you might need to determine whether you have to upgrade a peer to the latest release of Hyperledger Fabric to get a particular function. For example, if you want to install smart contract chaincode written in JavaScript to a peer, then it must be running Version 1.1.0 or higher.

## Commands

You can determine the exact version of a peer with the `peer --version` command.

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

You can see that there are many different pieces of version-related information.  See the reference topic [Peer version information](../Advanced/Peer/VersionInfo.md) to understand the version information in detail.

## Related Concepts
+ [Peers](../../KeyConcepts/Peers/Peers.md)

## Related Reference
+ [Peer version information](../Advanced/Peer/VersionInfo.md)
