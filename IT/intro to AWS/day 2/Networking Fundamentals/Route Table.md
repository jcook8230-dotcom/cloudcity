A **Route Table** ==contains a set of logical rules—called routes—that determine where network traffic from your subnets or gateways is directed==. Think of it as the **central traffic router** or GPS map for your Amazon VPC.

Every single subnet you create inside a VPC must be associated with exactly one route table, which controls all outbound pathing for the resources inside that subnet.

1. Anatomy of a Route

Each rule inside a route table consists of two fundamental parameters:

- **Destination:** The destination IP address range (expressed in CIDR notation) where the traffic is trying to go.
- **Target:** The gateway, network interface, or connection through which the traffic should be sent to reach that destination.

```
Example Route Rule:
[ Destination: 0.0.0.0/0 (Everywhere) ] ───(Forwards To)───> [ Target: nat-0123456 (NAT Gateway) ]
```

---

2. The Core Route Table Rules Compared

To understand how network isolation works, consider how a single VPC routes internal, public, and private traffic using distinct targets:

|Route Table Type|Destination|Target|Practical Function|
|---|---|---|---|
|**All Tables (Local)**|`10.0.0.0/16`|`local`|**Implicit Local Route.** Allows all subnets inside the VPC to talk to each other by default. This cannot be deleted.|
|**Public Subnet**|`0.0.0.0/0`|`igw-xxxxxx`|**Internet Gateway.** Forwards all unknown/external traffic directly out to the open, public internet.|
|**Private Subnet**|`0.0.0.0/0`|`nat-xxxxxx`|**NAT Gateway.** Forwards all unknown/external traffic out through a secure, one-way outbound firewall gateway.|
|**Isolated Subnet**|None|None|**No Internet Path.** Only contains the `local` route. Resources can talk to the VPC, but have zero internet access.|

---

3. Key Operational Rules & Characteristics

- **The Main Route Table:** When you create a VPC, it automatically comes with a "Main Route Table." If you create a new subnet and forget to explicitly associate it with a specific route table, AWS will **implicitly associate it with the Main Route Table** by default.
- **Most Specific Route Wins (Longest Prefix Match):** If a route table contains multiple overlapping rules, AWS decides where to send traffic based on the most specific matching rule (the longest prefix match). For example:
    - Traffic heading to `10.0.1.5` matches a local VPC route (`10.0.0.0/16`) and a specific peering route (`10.0.1.0/24`).
    - Because `/24` is more specific than `/16`, the traffic takes the peering route.
- **Gateway Route Tables:** You can attach route tables directly to an Internet Gateway (IGW) or Virtual Private Gateway (VGW) to filter or redirect incoming external traffic _before_ it even reaches a subnet.

---

4. Advanced Network Routing Targets

As your cloud infrastructure scales, your route tables will include target types beyond standard internet gateways:

- **`pcx-xxxxxx` (VPC Peering Connection):** Routes traffic directly across the private AWS backbone to resources inside a completely separate VPC.
- **`vpce-xxxxxx` (VPC Gateway Endpoint):** Used exclusively to route traffic cleanly to Amazon S3 or Amazon DynamoDB without leaving the internal AWS network structure.
    
- **`tgw-xxxxxx` (Transit Gateway):** Centralizes multi-network routing by forwarding traffic to a regional hub that interconnects dozens of corporate VPCs and on-premises networks.