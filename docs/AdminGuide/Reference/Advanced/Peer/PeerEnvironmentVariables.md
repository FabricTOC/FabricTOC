# Peer environment variables

A peer executes in the context of an operating system process, and can be controlled by a set of peer specific environment variables.  These variables are typically set in the peer configuration of the docker image, and apply to the peer while it is running.  Sometimes, environment variables can also  but can also be set when the `peer` command is run in which case they apply during the command invocation only.

# List of environment variables

Here's a full list of peer environment variables, their values, and what they do.

*  CORE_LOGGING_LEVEL

   Use this variable to set the logging level for the peer.  The logging level can be one of the following values

    * X
    * Y
    * Z

*  CORE_VARIABLE_2

   Use this variable to <blah>.  The logging level can be one of the following values

    * X2
    * Y2
    * Z2

## Related Concepts
+ [Peers](../../KeyConcepts/Peers/Peers.md)

## <a name=reference></a> Related Reference

+ [`peer chaincode` command](./PeerChaincodeCommand.md)
+ [`peer channel` command](./PeerChannelCommand.md)
+ [`peer logging` command](./PeerLoggingCommand.md)
+ [`peer node` command](./PeerNodeCommand.md)
+ [`peer version` command](./PeerVersionCommand.md)    
