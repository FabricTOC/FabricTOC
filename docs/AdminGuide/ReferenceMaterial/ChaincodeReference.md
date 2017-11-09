# Chaincode Reference material




Ledger state created by a chaincode is scoped exclusively to that chaincode and can’t be accessed directly by another chaincode. Given the appropriate permission, a chaincode may invoke another chaincode to access its state within the same network.

## Packaging

Before a chaincode can be installed or instantiated, it must be packaged.

The chaincode package consists of 3 parts:

        the chaincode, as defined by ChaincodeDeploymentSpec or CDS. The CDS defines the chaincode package in terms of the code and other properties such as name and version,
        an optional instantiation policy which can be syntactically described by the same policy used for endorsement and described in Endorsement policies, and
        a set of signatures by the entities that “own” the chaincode.

The signatures serve the following purposes:

        to establish an ownership of the chaincode,
        to allow verification of the contents of the package, and
        to allow detection of package tampering.

The creator of the instantiation transaction of the chaincode on a channel is validated against the instantiation policy of the chaincode.

A chaincode package that was signed at creation can be handed over to other owners for inspection and signing. The workflow supports out-of-band signing of chaincode package.

If the instantiation policy is not specified, the default policy is any MSP administrator of the channel.

## Creating the Package

There are two approaches to packaging chaincode. One for when you want to have multiple owners of a chaincode, and hence need to have the chaincode package signed by multiple identities. This workflow requires that we initially create a signed chaincode package (a SignedCDS) which is subsequently passed serially to each of the other owners for signing.

The simpler workflow is for when you are deploying a SignedCDS that has only the signature of the identity of the node that is issuing the install transaction.

We will address the more complex case first. However, you may skip ahead to the Installing chaincode section below if you do not need to worry about multiple owners just yet.

To create a signed chaincode package, use the following command:

peer chaincode package -n mycc -p github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02 -v 0 -s -S -i "AND('OrgA.admin')" ccpack.out

The -s option creates a package that can be signed by multiple owners as opposed to simply creating a raw CDS. When -s is specified, the -S option must also be specified if other owners are going to need to sign. Otherwise, the process will create a SignedCDS that includes only the instantiation policy in addition to the CDS.

The -S option directs the process to sign the package using the MSP identified by the value of the localMspid property in core.yaml.

The -S option is optional. However if a package is created without a signature, it cannot be signed by any other owner using the signpackage command.

The optional -i option allows one to specify an instantiation policy for the chaincode. The instantiation policy has the same format as an endorsement policy and specifies which identities can instantiate the chaincode. In the example above, only the admin of OrgA is allowed to instantiate the chaincode. If no policy is provided, the default policy is used, which only allows the admin identity of the peer’s MSP to instantiate chaincode.
Package signing

A chaincode package that was signed at creation can be handed over to other owners for inspection and signing. The workflow supports out-of-band signing of chaincode package.

The ChaincodeDeploymentSpec may be optionally be signed by the collective owners to create a SignedChaincodeDeploymentSpec (or SignedCDS). The SignedCDS contains 3 elements:

        The CDS contains the source code, the name, and version of the chaincode.
        An instantiation policy of the chaincode, expressed as endorsement policies.
        The list of chaincode owners, defined by means of Endorsement.

Note

Note that this endorsement policy is determined out-of-band to provide proper MSP principals when the chaincode is instantiated on some channels. If the instantiation policy is not specified, the default policy is any MSP administrator of the channel.

Each owner endorses the ChaincodeDeploymentSpec by combining it with that owner’s identity (e.g. certificate) and signing the combined result.

A chaincode owner can sign a previously created signed package using the following command:

peer chaincode signpackage ccpack.out signedccpack.out

Where ccpack.out and signedccpack.out are the input and output packages, respectively. signedccpack.out contains an additional signature over the package signed using the Local MSP.


**Copy most of this doc (including formatting): hyperledger-fabric.readthedocs.io/en/latest/chaincode4noah.html**
