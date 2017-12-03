# Identity and Membership

Identities really matter in a Hyperledger Fabric blockchain network! That's because a principal's **identity determines the exact permissions over resources that they have in a blockchain network**. Most importantly, **a principal's identity must have two qualities** -- it must be **verifiable** (a real identity, in other words), and it must also come from a **trusted** source.

These two identity concepts -- verification and trust -- are provided by a **Public Key Infrastructure** (PKI) and a **Membership Service Provider** (MSP), respectively. A PKI is a set of existing internet standards which provide secure communications for many different types of networks, whereas an MSP is a Hyperledger Fabric concept for managing identities in a blockchain network. In combination, PKIs and MSPs form the definition of the **members** of a blockchain network.

## <a name="Scenario"></a>A simple scenario to explain verification and trust

Imagine that you visit a supermarket to buy some groceries. At the checkout you see a sign that says that only Visa, Mastercard and AMEX cards are accepted. If you try to pay with a different card -- let's call it an "ImagineCard" -- it doesn't matter whether the card is authentic and you have sufficient funds in your account. It will be not be accepted.

| ![Scenario](./IdentityandMembership.diagram.6.png) |
| :---: |
| Having a valid credit card is not enough -- it must also be accepted by the store! PKIs and MSPs work together in the same way -- PKI provides a list of valid identities, and an MSP says which of these are members of a given blockchain network. |

PKIs and MSPs provide this combination of verification and trust. A PKI is like a card provider -- it dispenses many different types of verifiable identities. An MSP, on the other hand, is like the list of card providers accepted by the store -- determining which identities are the trusted members of the store payment network. **MSPs turn verifiable identities into the members of a blockchain network**.

Let's drill into these concepts in a little more detail.

## What are PKIs?

**A public key infrastructure (PKI) is a collection of internet technologies that provides secure communications in a network.** It's PKI that puts the **S** in **HTTPS** -- and if you're reading this documentation on a web browser, you're probably using a PKI to make sure it comes from a verified source.

| ![PKI](./IdentityandMembership.diagram.7.png) |
| :---: |
| The elements of Public Key Infrastructure (PKI). A PKI is comprised of Certificate Authorities who issue digital certificates to principals, who then use them in conjunction with public and private keys to authenticate and encrypt information. A CA's Certificate Revocation List (CRL) identifies the certificates that are no longer valid (this can happen for a number of reasons. A certificate might be compromised, for example). |

Although a blockchain network is more than a simple communications network, it makes sense for it to use the PKI standard as much as possible. You'll see that even though PKIs aren't sufficient for all the needs of a blockchain network, it's still the fundamental basis of blockchain security. It's therefore really helpful if you understand the basics of PKI and then why MSPs are so important.

There are four key elements to PKI:

 * **Digital Certificates**
 * **Public and Private Keys**
 * **Certificate Authorities**
 * **Certificate Revocation Lists**

Let's quickly describe these PKI basics, and if you want to know more details, then you can extend your knowledge [here](./https://en.wikipedia.org/wiki/Public_key_infrastructure).

## Digital Certificates

A digital certificate is a document which holds a set of attributes relating to a principal's identity. The most common type of certificate is an [X.509 certificate](https://en.wikipedia.org/wiki/X.509), which allows the encoding of a principal's identifying details in its structure. For example, Mary Morris of Mitchell Cars in Detroit, Michigan might have a digital certificate with a `SUBJECT` attribute of `C=US, ST=Michigan, L=Detroit, O=Mitchell Cars, OU=Manufacturing, CN=Mary Morris/UID=123456`. Mary's certificate is similar to her government identity card -- it provides information about Mary which she can use to prove key facts about her. There are many other attributes in an X.509 certificate, but forget about those for now.

| ![DigitalCertificate](./IdentityandMembership.diagram.8.png) |
| :---: |
| A digital certificate describing a principal called Mary Morris. Mary is the `SUBJECT` of the certificate, and the highlighted `SUBJECT` text shows key facts about Mary. The certificate also holds many more pieces of information, as you can see. Most importantly, Mary's public key is distributed within her certificate, whereas her private key is not. This private key must be kept private. |

What is important is that all of Mary's attributes can be written using a mathematical technique called cryptography (literally, "*secret writing*") so that tampering will invalidate the certificate. Cryptography allows Mary to present her certificate to others to prove her identity so long as the other party trusts the certificate issuer, known as a **Certificate Authority** (CA). As long as the CA keeps certain cryptographic information securely (meaning, its own **private key**), anyone reading the certificate can be sure that the information about Mary has not been tampered with -- it will always have those particular attributes for Mary Morris. Think of Mary's X.509 certificate as a digital identity card that is impossible to change.

## Public keys and private keys

There are two key elements to secure communication -- authentication and encryption, and these are made possible by the idea of public and private keys. **The unique relationship between a public-private key pair is the cryptographic magic that makes secure communications possible**.

Let's first recap the key ideas of authentication and encryption and then you'll see how they are made possible by public-private key pairs.

### Authentication and encryption

**Authentication** ensures that anything that might relate to a principal's identity, or information they generate, is not tampered with. For example, you might want to be sure you're communicating with the real Mary Mitchell rather than an impersonator. Or if Mary has sent you some information, you might want to be sure that it hasn't been changed by anyone else during transmission. In both cases, being able to established authenticity is of primary importance.

**Encryption**, on other hand, is quite different from authentication -- it enables the private transmission of information between Mary and other principals by ensuring that encrypted information can only be decrypted by its intended recipients and no one else.  

**To enable authentication and encrypted communications**, a principal can use a pair of mathematically related keys. **One of these keys is public and can be widely shared, while the other key is private and absolutely must not be shared**. The unique mathematical relationship between the keys is such that the private key can be used to transform information that only the public key can interpret, and vice-versa.    

### Using Public and Private Keys for Authentication

To authenticate a document, Mary uses her private key to attach a unique data signature to it. The signature is generated by a process called **hashing** in which the content of the document being signed is mathematically combined with Mary's private key to generate a small signature of fixed size. This signature can be verified by other principals in the network using Mary's **public key**.  

| ![AuthenticationKeys](./IdentityandMembership.diagram.9.png) |
| :---: |
| Authenticating data using private keys and public keys. Mary's private key is used to sign an original document with the unique signature (`X13vRZQql41`). |

Using the document as part of the signature in this way makes the document itself impossible to tamper with -- generating the same signature Mary would create is statistically impossible without Mary's private key.

### Using Public Keys and Private Keys for Encryption

To allow messages to be written in way such that only Mary can read them, Mary's public key can be used by anyone in a PKI to create a secret encoding of data that can only be transformed back to its original form by Mary's private key.

| ![EncryptionKeys](./IdentityandMembership.diagram.10.png) |
| :---: |
| Encrypting data using private keys and public keys. Any principal in the network who wishes to securely communicate with Mary can use Mary's public key to encrypt a document -- a document that only Mary can decrypt with her private key. |

Only Mary is able to decrypt the message as only she holds her private key -- that's why it's so important that private keys are not shared and remains secure. To prevent the encrypted message being tampered with it is also signed by the originating principal with their private key and this signature is checked by Mary (using the principal's public key) before she decrypts it.

If Mary wants to communicate securely back to another party she uses exactly the same process as others use to communicate with her, only using their public key to encrypt the data and her own private key to sign the data.

Again, if an intermediary tries to generate the same signature as the originating principal or Mary would do, it will be statistically impossible without that principal's private key -- again, the mathematics of cryptography at work!

## Certificate Authorities

As you've seen, an identity is brought to the blockchain network by a principal in the form of a cryptographically validated digital certificate issued by a Certificate Authority (CA). CAs are a common part of internet security protocols, and you've probably heard of some of the more popular ones: Symantec (originally Verisign), GeoTrust, DigiCert, GoDaddy, and Comodo, among others.  

| ![CertificateAuthorities](./IdentityandMembership.diagram.11.png) |
| :---: |
| A Certificate Authority dispenses certificates to different principals, which they use to authenticate and encrypt information. These certificates are signed by the CA using its private key. A principal's certificate includes their public key, but not their private key, and this applies to the CA's certificate too!   |

The digital certificate provided by a CA for a principal incorporates the principal's public key as well as a comprehensive set of their attributes. Crucially, CAs themselves also have a certificate, which they make widely available. This allows the consumers of identities issued by a given CA to verify them by checking that the certificate could only have been generated by the holder of the corresponding private key (the CA). Because every principal who wants to interact with a blockchain needs an identity, you might say that **a CA defines an organization's principals from a digital perspective**. It's the CA that provides the basis for an organization's principals to have a verifiable identity, expressed as a digital certificate.

If you're interested, you can read a lot more about CAs [here](./), but for now you should think of them as the system actors who issue digital certificates that convey a principal's identity.

### Root CAs, Intermediate CAs and Chains of Trust

CAs come in two flavors: **Root CAs** and **Intermediate CAs**. Because Root CAs (Symantec, Geotrust, etc) have to **securely distribute** hundreds of millions of certificates to internet users, it makes sense to spread this process out across what are called *Intermediate CAs*. These Intermediate CAs provide their certificates under the authority of the Root CA, and this linkage between a Root CA and Intermediate CAs establishes a **Chain of Trust** for any certificate that is issued by any CA in the chain. This ability to track back to the Root CA not only allows the function of CAs to scale while still providing security -- allowing organizations that consume certificates to use Intermediate CAs with confidence -- it limits the exposure of the Root CA, which, if compromised, would destroy the entire chain of trust. If an Intermediate CA is compromised, on the other hand, there is a much smaller exposure.

| ![ChainOfTrust](./IdentityandMembership.diagram.1.png) |
| :---: |
| A chain of trust is established between a Root CA and a set of Intermediate CAs using a simple chain. Many other configurations are possible to meet the needs of collaborating organizations. |

Intermediate CAs provide a huge amount of flexibility when it comes to the issuance of certificates across multiple organizations, and that's very helpful in a permissioned blockchain system. For example, you'll see that different organizations may use different Root CAs, or the same Root CA with different Intermediate CAs -- it really does depend on the needs of the network.

### Fabric CA

It's because CAs are so important that Hyperledger Fabric provides a built-in CA component to allow you to create CAs in the blockchain networks you form. You don't have to use the Fabric CA, but you will find it very helpful when you're starting to build a blockchain network for the first time, or using the [DRIVENET sample network](./).  

A Fabric CA is not as sophisticated as a full CA, but that's OK -- it's sufficient for many purposes. As you'll see, there are a few limitations to a Fabric CA. You can read more about these restrictions in the [Fabric CA reference section](../ReferenceMaterial/FabricCA.md)

## Certificate Revocation Lists

A Certificate Revocation List (CRL) is easy to understand -- it's just a list of certificates that a CA knows to be revoked for one reason or another. If you recall the [store scenario](#Scenario), a CRL would be like a list of stolen credit cards.  

When a third party wants to verify a principal's identity, it first checks the issuing CA's CRL to make sure that the certificate has not been declared invalid. A verifier doesn't have to check the CRL, but if they don't they run the risk of accepting a compromised identity.

| ![CRL](./IdentityandMembership.diagram.12.png) |
| :---: |
| Using a CRL to check that a certificate is still valid. If an impersonator tries to pass a compromised digital certificate to a validating principal, it can be first checked against the issuing CA's CRL to make sure it's not listed as no longer valid. |

Note that a certificate being revoked is very different from a certificate expiring. Revoked certificates have not expired -- they are, by every other measure, a fully valid certificate.

## Membership Service Provider

You've now seen how a PKI can provide verifiable identities through a chain of trust, so let's see how these identities can be used to represent the trusted members of a blockchain network. That's where a Membership Service Provider (MSP) comes into play -- **it identifies the principals who are the members of a given organization in the blockchain network**.

Whereas a PKI provides a verifiable identity, an MSP complements this by identifying which Root CAs and Intermediate CAs are trusted to define which principals are considered the members of an organization. An MSP can also recognize other things related to membership of a network -- a list identities that have been revoked, for example -- but those things will be covered later. For now, **think of an MSP as providing a list of administrators of a given organization**, with the MSP either holding certificates itself or by listing which CAs can issue valid certificates, or -- as will usually be the case -- through some combination of both.

If an MSP is defined on the local file system of a peer node, orderer node, or user (client application or administrator), it is a **Local MSP**. If it's found in the policy configuration of the network or each channel, it is a **Global MSP**. You'll hear more about local and global MSPs and why the distinction between them is important later.

### Mapping MSPs to Organizations

Organizations will usually manage their members under a single MSP. Note that this is organizational concept different from that of an X.509 organization, which we'll talk about later.

The exclusive relationship between an organization and its MSP makes it sensible to name the MSP after the organization, a convention you'll find adopted in most policy configurations. For example, organization `ORG1` would have an MSP called `ORG1.MSP`. In some cases an organization may require multiple membership lists -- for example, where channels are used to perform very different business functions with other organizations. In these cases it makes sense to have multiple MSPs and name them accordingly, e.g., `ORG2.MSP.NATIONAL` and `ORG2.MSP.GOVERNMENT`, reflecting the different membership roots of trust within `ORG2` in the NATIONAL sales channel compared to the GOVERNMENT channel.

| ![MSP1](./IdentityandMembership.diagram.3.png) |
| :---: |
| Two different MSP configurations for an organization. The first configuration shows the typical MSP relationship -- a single MSP defines the list of verifiable members of an organization. In the second configuration, different MSPs are used to support different identity providers for national, international, and governmental memberships.|

#### <a name="OUMSP"> Organizational Units and MSPs

An organization is often divided up into multiple **organizational units** (OUs), each of which has a certain set of responsibilities. For example, the `MITCHELL` organization might have both `MITCHELL.MANUFACTURING` and `MITCHELL.DISTRIBUTION` OUs to reflect these separate lines of business. When a CA issues X.509 certificates, the `OU` field in the certificate specifies the line of business to which the identity belongs.

We'll see later how OUs can be helpful to control the parts of an organization who are considered to be the members of a blockchain network. For example, in DRIVENET, only identities from the `MITCHELL.MANUFACTURING` OU might be able to access a channel, whereas `MITCHELL.DISTRIBUTION` cannot.

Finally, though this is a slight mis-use of OUs, they can sometimes be used by *different* organizations in a consortium to identify each other. In such cases, the different organizations use the same Root CAs and Intermediate CAs for their chain of trust, but assign the `OU` field appropriately to identify membership of each organization. We'll also see how to configure MSPs to achieve this later.

### Local and Global MSPs

There are two different types of MSPs: local and global. **Local MSPs are defined for nodes** (peer or orderer) and **users** (administrators that use the CLI or client applications that use the SDK). **Every node and user must have a local MSP defined**.

In contrast, **global MSPs are defined either for channels or the entire network**, and they apply to all of the nodes that are part of a channel or network. Every channel or network must have at least one MSP defined for it, and peers and orderers on a channel will all share the same global MSP. The key difference here between local and global MSPs is not how they function, but their **scope**.  

| ![MSP2](./IdentityandMembership.diagram.4.png) |
| :---: |
| Local and Global MSPs. The MSPs for the peers are local, whereas the MSPs for the channel are global. Each peer is managed by its own organization, ORG1 or ORG2. This channel is managed by both ORG1 and ORG2. Similar principles apply for the network, orderers and users, but these are not shown here for simplicity. |

You can see that **local MSPs are only defined on the file system of the node or user** to which they apply. Therefore, physically and logically there is only one local MSP per node or user. However, as **global MSPs apply to all nodes in a channel or network**, they are logically defined once for the network or the channel. However, **a global MSP is instantiated on the file system of every node and kept synchronized via consensus**. So while there is a copy of a global MSP on the local file system of every node, logically the global MSP exists on the channel or the network.

You may find it helpful to see how local and global MSPs are used by seeing what happens when a blockchain administrator installs and instantiates a smart contract, as shown in the [diagram above](MSP2).

An administrator `B` connects to the peer with an identity issued by `RCA1` and stored in their **local MSP**. When `B` tries to install a smart contract on the peer, the peer checks its **local MSP**, `ORG1.MSP`, to verify that the identity of `B` is indeed a member of `ORG1`. A successful verification will allow the install command to complete successfully. Subsequently, `B` wishes to instantiate the smart contract on the channel. Because this is a channel operation, all organizations in the channel must agree to it. Therefore, the peer must check the **global MSP** in the channel policy before it can successfully complete this command.  (Other things must happen too, but ignore those for now.)

You can see that the channel and the ledger are really **logical constructs** when they are defined at the channel level. It is **only when they are instantiated on a peer's local filesystem and managed by it that they become physical**. It's really important to understand how concepts like global MSPs, channel policies and even the ledger itself are **defined at the channel level, but instantiated and managed on the peers** of the different organizations in the channel.

### MSP Levels

The split between **global and local MSPs reflects the needs of organizations to administer their local resources**, such as a peer or orderer nodes, **and their global resources**, such as ledgers, smart contracts, and consortia, which operate at the channel or network level. It's helpful to think of these MSPs as being at different **levels**, with **MSPs at a higher level relating to network administration concerns** while **MSPs at a lower level handle identity for the administration of private resources**. This tiering is helpful because it supports the mix of both broad and narrow administrative control depending on how the network needs to be constituted. MSPs are mandatory at every level of administration -- they must be defined for the network, channel, peer, orderer and users.

| ![MSP3](./IdentityandMembership.diagram.2.png) |
| :---: |
| MSP Levels. The MSPs for the peer and orderer are local, whereas the MSPs for the channel and network are global. Here, the network is administered by ORG1, but the channel can be managed by ORG1 and ORG2. The peer is managed by ORG2, whereas ORG1 manages the orderer. ORG1 trusts identities from RCA1, whereas ORG2 trusts identities from RCA2. Note that these are **administration** identities, reflecting who can administer these components. So while ORG1 administers the network, ORG2.MSP does exist in the network definition. |

 * **Network MSP:** These MSPs are defined in the configuration policy of the whole network, so by definition, **there is only one set of network MSPs**. Every principal who uses a network must be a member as defined by the MSPs in the network policy before they can perform an administrative task. This means that the MSPs that are defined for the network should define **the organizations who are trusted to have administrative control over the network**. An example of a network-wide administrative permission might be to define or change the organizations who can create channels.

 * **Channel MSP:** These MSPs are defined inside the configuration policy of each channel, and therefore there is a set of MSPs for each channel that is defined. It is helpful for a channel to have its own set of MSPs because a channel provides private communications between a particular set of organizations which in turn have administrative control over it. You can see that the need for **a separate set of channel MSPs stems from the need for local autonomy** -- the organizations in a channel can, and will often need to be, largely independent from the rest of the network. It also means that administrative control over the network doesn't necessarily imply control over any particular channel; again reflecting the real administrative needs of collaborating organizations who may sometimes require separation of control. We see this kind of separation at the levels of control in the real world, too. The authority of the President of the United States, for example, exists at the federal level. He or she has no authority to veto state laws.

 * **Peer MSP:** This local MSP is defined on the file system of each peer. Conceptually, it performs exactly the same function as global MSPs with the restriction that it only applies to the peer where it is defined. As peers are owned by a particular organization and connect applications from that organization to the ledger, there is only a single MSP for a peer. It's possible to specify multiple different CAs in this MSP, but in practice a local MSP will usually refer to many fewer CAs than a set of global MSPs. An example of a peer permission might be the ability to install or upgrade smart contract chaincode on that peer.

 * **Orderer MSP:** Like a peer MSP, an orderer local MSP is also defined on the file system of the node and only applies to that node. Like peer nodes, orderers are also owned by a single organization and therefore have a single MSP to list its trusted principals, though again it's possible to specify multiple Root CAs.

### MSP Structure

So far, you've seen that the two most important elements of an MSP are the identification of the root and intermediate CAs that are used to used to establish a principal's membership of an organization. There are, however, more elements that are used in conjunction with these two to assist with membership functions.

| ![MSP4](./IdentityandMembership.diagram.5.png) |
| :---: |
| The figure above shows how a **local MSP** is stored on a local filesystem. Even though global MSPs are not physically structured in exactly the same way, it's still helpful to think about global MSPs this way. |

As you can see, there are nine elements to an MSP. It's easiest to think of these elements in a directory structure, where the MSP name is the root folder name with each subfolder representing different elements of an MSP.

Let's describe these folders in a little more detail and see why they are important.

 * **Root CAs**

 This folder contains a list of self-signed X.509 certificates of the Root CAs trusted by this organization. There must be at least one Root CA X.509 certificate in this MSP folder.

 This is the most important folder because it identifies the CAs from which all other certificates must be derived to be considered members of this organization.

 * **Intermediate CAs**

 This folder contains a list of X.509 certificates of the Intermediate CAs trusted by this organization. Each certificate must be signed by one of the Root CAs in the MSP or by an Intermediate CA -- or a chain of ICAs -- that ultimately lead back to a trusted Root CA. It is possible to have a functioning network that does not have any Intermediate CAs, in which case this folder would be empty. However, this is not a best practice.

 Like the Root CA folder, this folder defines the CAs from which certificates must be issued to be considered members of the organization. It's slightly less important than the Root CA folder, because it's not the root of trusted membership.

 * **Organizational Units (OUs)**

 These are listed in the msp/config.yaml and contain a list of organizational units that are considered to be part of the MSP. This is particularly useful when you want to restrict membership to only those principals who are part of a particular organization, as will be the case when an organization has a rich structure, [as discussed earlier](#OUMSP). You can see [how to configure the list of trusted OUs](../ReferenceMaterial/MembershipServicesProvider.md) in the reference material.

 Specifying OUs is optional. If no OUs are listed all of the principals that are part of an MSP -- as identified by the Root CA and Intermediate CA folders -- will be considered members of the organization.

 * **Administrators**

 This folder contains a list of X.509 certificates that define the principals who have the role of administrators of this organization. Typically there should be one or more certificates in this list.  

 It's worth noting that just because a principal has the role of an administrator it doesn't mean that they can administer particular resources! This seems strange, but will make more sense after you learn about the nature of policy permissions and how those permissions -- and not a principal's "role" -- are what define what any given organization's administrators can actually do. For example, a channel policy might specify that `MITCHELL.MANUFACTURING` administrators have the rights to add new organizations to the channel, whereas the `MITCHELL.DISTRIBUTION` administrators have no such rights. You can read more about policies [here](../PoliciesforAccessControl.md).

 It's worth noting that even though an X.509 certificate has a `ROLE` attribute (specifying, for example, that a principal is an "admin"), this refers to a principal's role within its organization rather than on the blockchain network. This is distinctly different from the purpose of the `OU` attribute, which -- if it has been defined -- refers to a principal's place in the network. Indeed, this is why we need the Administrators folder - because the blockchain role is quite different to the X.509 `ROLE`.

 The `ROLE` attribute **can** be used to confer administrative rights at the channel level if the policy for that channel has been written to allow any administrator from an organization (or certain organizations) permission to perform certain channel functions (such as instantiating chaincode). In this way **an organizational role can confer a network role**. We'll learn more about how policies can be written that way and how this functionality imparts significant operational advantages later.

 * **Revoked Certificates**

 If the X.509 certificate of a principal has been revoked, identifying information about the cert -- not the cert itself -- is held in this folder. These identifiers -- known as a Subject Key Identifier (SKI) and Authority Access Identifier (AKI) -- are checked whenever a certificate is being used to make sure the certificate is still valid.

 This list is conceptually the same as a CA's Certificate Revocation List (CRL), but relates to revocation of membership from the organization rather than revocation from the CA. As a result, the administrator of an MSP, local or global, can quickly revoke a principal from an organization without having to resort to revoking their certificate from a CA -- which, of course, might not be appropriate.

 This "list of lists" is optional. It will only become populated as certificates are revoked.

 * **Signing Certificate**

 This folder contains the **public X.509 certificate** used by a node or user when the need to identify themselves to another principal in the network. This is the certificate a peer places in a transaction proposal response, for example, to indicate that a peer's organization has endorsed it -- which can subsequently be checked against an endorsement policy (containing the organizations that must endorse a transaction) by a validating node.

 This folder is mandatory for local MSPs, and there must be exactly one X.509 certificate for the node. It is not used for global MSPs.

 * **KeyStore for Private Key**

 This folder is defined for the local MSP of a peer or orderer node (or in a user's local MSP), and contains the **private key**. This key is used to sign or encrypt data -- for example to sign a transaction proposal response, indicating that a peer's organization has endorsed it.

 This folder is mandatory for local MSPs, and must contain exactly one private key. Obviously, access to this folder must be limited only to those operators administrators who have responsibility for local MSPs.

 **Global MSPs** do not include this folder or any private keys, as by their nature they are shared across the network or channel.

 * **TLS Root CA**

 This folder contains a list of self-signed X.509 certificates of the Root CAs trusted by this organization **for TLS communications**. An example of a TLS communication would be when a peer needs to connect to an orderer so that it can receive ledger updates.

 If you look at [this diagram](./ABlockchainNetwork.md#NetworkPrincipals2), you can see how the MSP TLS information relates to the principals inside the network -- the peers and the orderers -- rather than those that consume the network -- applications and administrators.

 There must be at least one TLS Root CA X.509 certificate in this MSP folder.

 * **TLS Intermediate CA**

 This folder contains a list of X.509 certificates of the Intermediate CAs trusted by this organization **for TLS communications**.

 By analogy to the TLS Root CA folder, this folder is kept separate to the MSP Intermediate CA folder for the same reason. There do not need any Intermediate CA X.509 certificates in this MSP folder -- they are optional.

## MSPs in DRIVENET

*This section still needs some work*

Root of Trust established -- or used, more likely -- by Mitchell and Regal (and the two dealerships, possibly). Could be that the entire car industry uses -- for convenience sake -- the same root of trust.

Will ZBS use the same root of trust as Mitchell and Regal? Possibly.

The DMV wouldn't, which means that either the initial configuration would have to recognize its CA or there'd have to be a config transaction to update the network definition to include it. *That's my read of it anyway.*  

## That's it!

OK, we've now finished our extensive tour of identities and membership of a blockchain network!

In summary, Hyperledger Fabric uses a PKI and MSPs to identify the principals who are the members of each organization collaborating in a blockchain network.


[Next: Policies for Access Control](./PoliciesforAccessControl.md)
