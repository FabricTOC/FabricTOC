## Fabric CA Reference guide

### Fabric CA restrictions

In a blockchain network with multiple CAs, each Fabric CA will comprise a cluster of multiple servers, each of which share the same underlying database for certificates. The underlying database can be configured to be LDAP if required.  If it's not configured to use LDAP, then the CA must be configured with at least one pre-registered bootstrap identity to enable you to register and enroll other identities.
