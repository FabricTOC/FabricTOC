# Introduction


Fabric networks are complex, interdependent systems whose administration encompasses not just the initial configuration and bootstrapping of the network but also adaptation and expansion as new organizations and participants are added to it.

In this operations guide we’ll take you through this entire process. You’ll learn about the scope of what we call “network definitions” and how a Fabric network is established and managed, including:

1.	What “organizations” actually are and how to add them to a running network.
2.	How digital certificates are used to identify what we call “principals” and how permissions define not just what the principals in a Fabric network can do, but what they actually are.
3.	The nature of access control and policies. How policies change depending on the type of principal they apply to, how we change policies, and even how we change the policies for changing policies!
4.	How the network is actually bootstrapped, including the establishment of the so-called “genesis” block.
5.	How Fabric networks are organized as “groups within groups”.
6.	The creation and maintenance of channels, peers, and chaincode.

We’ll be looking at these concepts through the lens of a sample network called **DRIVENET**, where Mitchell, a car manufacturer in Detroit, and Regal, a manufacturer in Kentucky, come together to form a network to streamline information and processes related to their businesses. They decide that they will have equal and shared administrative rights over the network and will design it, in part, to interact with applications that will track car production and distribution.

After setting up the initial network, Mitchell and Regal will invite Cecil’s – a car dealership in Decatur, Illinois, who sells both types of cars – to DRIVENET. Mitchell and Regal are also required to invite the DMV to DRIVENET to ensure that cars are registered properly and that changes of ownership are recorded. These new parties will participate fully in the network, but with fewer administration rights. Developers at Cecil’s and the DMV write applications to sell cars and register their usage on DRIVENET.


Mitchell and Regal will later grow DRIVENET to include ZBS Insurance, who will offer insurance plans to Cecil’s customers. Separately, Regal invites Faster Autos, from Miami, Florida, who only sells Regal cars – which it receives at a significantly reduced price – to the network. Faster Autos also wants to make ZBS insurance plans available to its customers and will – like Cecil’s – employ developers to write applications to manage their plans.

# Links to more information

Configuring and administrating a Fabric network covers a lot of ground, but there's still a lot of information that won't be talked about in this guide.

Links here with short descriptors. 











[-->Next](./TheNetworkDefinition.md)
