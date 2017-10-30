# Peer Tasks

## CouchDB Configuration

CouchDB is enabled as the state database by changing the stateDatabase configuration option from goleveldb to CouchDB. Additionally, the couchDBAddress needs to configured to point to the CouchDB to be used by the peer. The username and password properties should be populated with an admin username and password if CouchDB is configured with a username and password. Additional options are provided in the couchDBConfig section and are documented in place. Changes to the core.yaml will be effective immediately after restarting the peer.

You can also pass in docker environment variables to override core.yaml values, for example CORE_LEDGER_STATE_STATEDATABASE and CORE_LEDGER_STATE_COUCHDBCONFIG_COUCHDBADDRESS.

Below is the stateDatabase section from core.yaml:

state:
  # stateDatabase - options are "goleveldb", "CouchDB"
  # goleveldb - default state database stored in goleveldb.
  # CouchDB - store state database in CouchDB
  stateDatabase: goleveldb
  couchDBConfig:
     # It is recommended to run CouchDB on the same server as the peer, and
     # not map the CouchDB container port to a server port in docker-compose.
     # Otherwise proper security must be provided on the connection between
     # CouchDB client (on the peer) and server.
     couchDBAddress: couchdb:5984
     # This username must have read and write authority on CouchDB
     username:
     # The password is recommended to pass as an environment variable
     # during start up (e.g. LEDGER_COUCHDBCONFIG_PASSWORD).
     # If it is stored here, the file must be access control protected
     # to prevent unintended users from discovering the password.
     password:
     # Number of retries for CouchDB errors
     maxRetries: 3
     # Number of retries for CouchDB errors during peer startup
     maxRetriesOnStartup: 10
     # CouchDB request timeout (unit: duration, e.g. 20s)
     requestTimeout: 35s
     # Limit on the number of records to return per query
     queryLimit: 10000

CouchDB hosted in docker containers supplied with Hyperledger Fabric have the capability of setting the CouchDB username and password with environment variables passed in with the COUCHDB_USER and COUCHDB_PASSWORD environment variables using Docker Compose scripting.

For CouchDB installations outside of the docker images supplied with Fabric, the local.ini file must be edited to set the admin username and password.

Docker compose scripts only set the username and password at the creation of the container. The local.ini file must be edited if the username or password is to be changed after creation of the container.

Note

CouchDB peer options are read on each peer startup.


## Peer tasks

    Starting a Peer
    DefAssociating an identity
    Submitting a Config transaction
    Adding an Organization to a network
    Changing Network Values
        Block height/size
        Hashing Algorithms
    Creating a channel
    Chaincode best practices
    Membership Services
        Using Fabric CA to set up an MSP
        Integrating LDAP Server Information
    Changing the policies on changing policies
        Mod Policy Best Practices
    Endorsement Policies
    Peer Operations
    Orderer operations

[-->Reference Material](./ReferenceMaterial/ReferenceMaterial.md)
