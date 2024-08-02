# Overview of VPC networks


 A VPC network __connects to on-premises networks__ by using _Cloud VPN tunnels_ and _Cloud Interconnect_ attachments and distributes traffic from Google Cloud external load balancers to backends.

# network related iam role

![./pics/network%20related%20iam%20roles.png](./pics/network%20related%20iam%20roles.png)


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

# Multiple network interfaces