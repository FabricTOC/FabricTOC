# Updating the Network

## Configuration Transactions

The genesis block as just the first configuration transaction.

*Wasn't sure if you want to talk about configtx and/or configtxgen here or just configtxlator. I assumed the latter, so this is concept related stuff from the configtxlator doc:*

The configtxlator tool was created to support reconfiguration independent of SDKs. Channel configuration is stored as a transaction in configuration blocks of a channel and may be manipulated directly, such as in the bdd behave tests. However, at the time of this writing, no SDK natively supports manipulating the configuration directly, so the configtxlator tool is designed to provide an API which consumers of any SDK may interact with to assist with configuration updates.

The tool name is a portmanteau of configtx and translator and is intended to convey that the tool simply converts between different equivalent data representations. It does not generate configuration. It does not submit or retrieve configuration. It does not modify configuration itself, it simply provides some bijective operations between different views of the configtx format.

The standard usage is expected to be:

        SDK retrieves latest config
        configtxlator produces human readable version of config
        User or application edits the config
        configtxlator is used to compute config update representation of changes to the config
        SDK submits signs and submits config

The configtxlator tool exposes a truly stateless REST API for interacting with configuration elements. These REST components support converting the native configuration format to/from a human readable JSON representation, as well as computing configuration updates based on the difference between two configurations.

Because the configtxlator service deliberately does not contain any crypto material, or otherwise secret information, it does not include any authorization or access control. The anticipated typical deployment would be to operate as a sandboxed container, locally with the application, so that there is a dedicated configtxlator process for each consumer of it.


## Verifying Network Changes


## A DRIVENET Configuration Transaction



[-->Next](../Consortia/Consortia.md)
