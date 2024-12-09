# Connecting networks to Google VPC

The following are several effective ways to connect __on-premises neworks__ or __networks in other clouds__ to a google vpc:

![ways to connect to google vpc](./pics/2-ways-to-connect-networks-to-vpc.png)

__How to choose network connectivity product doc__
[doc - Choosing a Network Connectivity product](https://cloud.google.com/network-connectivity/docs/how-to/choose-product)

## 1 - Cloud VPN

A "tunnel" connection __over the internet__.

Q: If a new subnet is added to an existing Google VPC, would a Cloud VPN automatically get routs to it?
A: Yes. A ___Cloud Router___ enables you to __dynamically__ exchange routes between a Google VPC and peer network by using _Border Gateway Protocol (BGP)_.

![how does HA(High Availability) Cloud VPN work](./pics/2-ha-vpn-gcp-to-on-prem.svg)

Usecases:
-  You cannot use Cloud VPN to route traffic to the public internet; it is __designed for secure communication between private networks__.

Pros:
- simple

Cons:
- security concerns
- bandwidth reilability

## 2 - [Direct Peering](https://cloud.google.com/network-connectivity/docs/direct-peering)

When established, Direct Peering provides a direct path from your on-premises network to Google services, __including Google Cloud products that can be exposed through one or more public IP addresses__. Traffic from Google's network to your on-premises network also takes that direct path, including __traffic from VPC networks in your projects__.

Usecases:
- Direct Peering __exists outside of Google Cloud__. Unless you need to access Google Workspace applications, the recommended methods of access to Google Cloud are _Dedicated Interconnect_ or _Partner Interconnect_. Those two are all google cloud products.


Pros:
- secure
- Does not use any Google Cloud resources; configuration is opaque to Google Cloud projects.

Limitations:
- Direct Peering __does not provide direct access__ to VPC network resources that have __only internal IP__ addresses.
- To change the destination IP address ranges for your on-premises network, contact Google.
- __Google does not offer a service level agreement (SLA)__ with Direct Peering.

## 3 - Carrier Peering

Similar to Direct Peering. But Carrier peering gives you direct access from your on-premises network __through a service provider's network__ to Google Workspace and to __Google Cloud products that can be exposed through one or more public IP addresses__.

Cons:
- __Google does not offer a service level agreement (SLA)__ with Carrier Peering.

## 4 - Dedicated Interconnect

Usecases:
- This option allows for __one or more direct, private connections to Google__. 

Pros:
- the __highest uptimes for interconnection__
  - If these connections have topologies that meet Google’s specifications, they can be __covered by an SLA of up to 99.99%__.
  - Also, these connections __can be backed up by a VPN for even greater reliability__. 

## 5 - Partner Interconnect

provides connectivity between an on-premises network and a VPC network __through a supported service provider__.

Usecases:
- a data center is in __a physical location that can't reach a Dedicated Interconnect colocation facility__
- the __data needs don’t warrant an entire 10 GigaBytes per second connection__.
-  to support __mission-critical services__ or applications that __can tolerate some downtime__.

Pros:
- As with Dedicated Interconnect, if these connections have topologies that meet Google’s specifications, they __can be covered by an SLA of up to 99.99%__.

Cons:
- but note that __Google isn’t responsible__ for any aspects of Partner Interconnect provided by the third-party service provider, nor any issues outside of Google's network. 


## 6 - Cross-Cloud Interconnect

Cross-Cloud Interconnect helps you establish __high-bandwidth dedicated connectivity__ between Google Cloud and __another cloud service__ provider. 

Cross-Cloud Interconnect connections are available in two sizes: 10 Gbps or 100 Gbps.

# Routes

Q: How to configure __internet access__ for external IP VMs? How about internal IP VMs?
A: First, a route to 0.0.0.0/0 to IGW for external IP VMs. Same route but to a NAT GW for internal IP VMs. 
Then, the EGRESS firewall that allows it.

Q: How to configure routes within subnet, so that __resources in the same subnet can route traffic to each other__ ? what about between subnets?
A: A route to subnets' CIDR, with next hop as the subnet itself. For between subnets => experiments to find out.

__Route Types__

- System-generated
  - priority 65534 => Google Cloud only uses a default route if a route with a more specific destination does not apply to a packet.
  - route to Internet => (If no more specific route is specified, the defalut route will be used to access Google API. The alternative to keep rounting within Google network rather than the Internet, would be using Private Google Access or Service Connect Endpoint)
  - default subnet routes to have resources in the same subnet can route traffic to each other
- Custom
  - custom static routes
    - pro: quicker & more secure than dynamic routing
    - con: requires more maintenance & can't point to a VLAN attachment
- Peering
  - ___Dynamic Routes___
    - _Cloud Routers_ is doing the dynamic routing
    - destinations always represent IP address ranges outside your VPC network, which are received from a BGP peer router
    - Dynamic routes are used by: Dedicated Interconnect, Partner Interconnect, HA VPN tunnels. Classic VPN tunnels that use dynamic routing Routes 


# network related iam role

![./pics/network%20related%20iam%20roles.png](./pics/network%20related%20iam%20roles.png)