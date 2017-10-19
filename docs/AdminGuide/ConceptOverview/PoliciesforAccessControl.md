# Policies for Access Control

Network definitions are managed by multiple organizations in a consortium.

An **image** here to show what this looks like.

Your rights are at the channel level. It's not a top down system in which having admin rights at a high level (the system channel, for example) means you have any rights over any other channels (or, if you're a member of a channel, means you automatically have admin rights over that channel). Also a user might have admin rights for the network but no rights over org1 and org2 but they do have admin rights over org3. Important to stress that rights are not just at the channel level but also at the organization level. You could potentially have admin rights over a channel even though you don't have admin rights over an organization. 


## What are Policies?

Define access rights for different organizational users (principals) over any network component. For example, the ability to add organizations to the consortium. Without policies, you don't have access to anything. You can't change anything. You can't do anything.



## Principals and Resource Access Control


## Implicit and Explicit Policies

Policies can be explicit (ie tied to users specifically -- User Joe_Schmoe has the right to do x, y, and z). Or there are implicit metapolicies (all admins of org1 have certain rights). So all you have to become is an admin of org1 to have those rights. You can setup your policies more generally this way, saying that any admin of org1 and org2 can administer the network but no admins from orgs3 and org4 can administer it.

The implicit metapolicy allows a network to grow more organically while still allowing there to be rules behind who has certain rights. No matter how many users or orgs join, implicit metapolicies will still apply where explicit policies will need to be updated to reflect new admins and users. Implicit metapolicies can be written to allow "any, all, some" -- any number of combinations of admins over different orgs to have rights. The farther down you get the more likely there is to have an explicit policy (within orgs). The higher up you go the more likely there is to be an implicit metapolicy.

These policies are stored in the config block.


## Policies for Changing Policies -- Mod policies!

Use with extreme care -- can break the network. This is the policy for changing how you change policies. Befitting the nested structure of Fabric networks, all policies have a mod policy attached to them. Policies for how we relate, and then policies that change how we can change how we relate. Might seem silly or pedantic, but this is kind of thing you end up with when you have this sort of structure.


## Policies in DRIVENET




## Policies for Access Control
      + What are policies?
      + Why are policies important?
      + Principals and resource access control
      + Implicit and Explicit policies
      + Policies for Changing Policies - Mod_Policies!
      + Policies in DRIVENET

[Next: Creating and Updating a Network](./CreatingandUpdating.md)
