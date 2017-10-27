# The Principals in a Network

Three types of principals: users (which can also be an organization, or "entity"), roles, and organizational units.


## Organizations, Organizational Units, Roles, and Members

The ability to *read* relegates an org to a passive role in the network. Reading orgs receive ledger updates, query the ledger, and can join channels, but they don't participant in endorsement, can't administer, can't propose transactions (including configuration transactions), and can't instantiate chaincode.

Write permissions add the ability for an organization to propose transactions and install chaincode (though the ability to instantiate that chaincode is left to an administrator). Writers also can participate in endorsement (depending on the specific endorsement policy on a particular channel).  


## Identifying Principals with Digital Certificates

Principals are identified using a digital certificate. You can read more about digital certificates [here](./), but if they're new to you, think of a digital certificate like a government issued identity card, that holds information about a certain principal.  In the same way as an identity card might hold someone's name, date of birth and city of residence, a digital certificate stores the relevant information about a principal.  Hyperledger Fabric uses digital certificates that correspond to the [X509 standard](./), which are the most common kind of digital certificate, and specify things like a principals organization, their country, state and location, and the valid dates for the certificate -- along with a raft of other information.   

Two of the most important pieces of identity information used by Hyperledger Fabric are the principal's organization, and whether the principal has an administrator's role within that organization. For example, if an administrator submits a transaction to change the blocksize of the network, the network policy can defined that the transaction is valid only if it is signed by principals who are administrators of a specific set of organizations.


## Principals in DRIVENET




## The Principals in an organization
      + Organizations, Organizational Units, Roles and Members
      + Identifying Principals with Digital Certificates
      + Principals in DRIVENET


[Next: Identity and Chains of Trust](./IdentityandChainsofTrust.md)
