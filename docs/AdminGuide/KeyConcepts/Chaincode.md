# Chaincode

## What is Chaincode?

A way of establishing rules over transactions and automating this "business logic". Similar to the concept of smart contracts.


## Chaincode and the Ledgers

Chaincode is written to the ledger(s). This makes it immutable just like any other block.


## Installing Chaincode

Happens at the peer level (except for the system chaincode, which is bootstrapped into the initial configuration block). Chaincode can be created by anyone. Every peer on the channel must install the chaincode for it to be used on that channel.


## Instantiating Chaincode

Happens at the channel level. Must have admin rights over that channel to instantiate. Only happens once.


## Upgrading Chaincode

Has a version.



## DRIVENET Chaincode

Similar to chaincode that would be exist for any supply chain network. Customized to take specific regulations in the car industry (and American laws) into account.



[Next: Starting DRIVENET](../DriveNetSample/StartingDRIVENET.md)
