# Peer Version Information

The `peer` command can be used to determine build version of the peer.

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

## Understanding the version information

* `Version`

  This is the Hyperledger Fabric version of the code from which the peer is built.  The different versions of Hyperledger Fabric are described [here](https://github.com/hyperledger/fabric/releases).

* `Go version`

  This is the version of GOLANG with which the peer was built.  The different versions of GOLANG are described [here](https://golang.org/doc/devel/release.html).

  This version is important because any smart contract chaincode that is developed in GOLANG must be compatible with the version of GOLANG that the peer is built with.  Usually this means that the smart contract chaincode GOLANG version must be greater than or equal to the peer GOLANG version.

* `OS/Arch: linux/amd64`

  This is the operating system (`OS`) and processor architecture (`Arch`) that the peer is built with. Hyperledger Fabric peers are built for many different combinations of `OS` and `Arch`, and for the peer to work correctly, it must be compatible with the `OS` and `Arch` of the machine it's running on.  

  `OS` can be one of

    * `linux`

    Linux operating system compatible.

  `Arch` can be one of

    * `amd64`   

    AMD64 processor compatible. More information at this [link](https://en.wikipedia.org/wiki/X86-64).

    * `ppc64le`   

    OPEN POWER processor compatible. More information at this [link](https://openpowerfoundation.org/).

    * `s390x`   

    IBM system z in 64 bit processor mode. More information at this [link](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.3.0/com.ibm.swg.im.iis.productization.iisinfsv.install.doc/topics/wsisinst_set_envars_cpp_gcc64z.html).

  In many cases, a peer will be running in a Docker container, so the OS will be `linux`. The `Arch` will vary according to the processor where the the Docker container was built.

* `Chaincode`

  * `Base Image Version`

  * `Base Docker Namespace`

  * `Base Docker Label`

  * `Docker Namespace`
