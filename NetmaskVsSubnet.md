# Netmask vs Subnet mask

The terms **netmask** and **subnet mask** are often used interchangeably in networking, but they have subtle differences in context.

### Netmask
- **Definition**: A **netmask** is a 32-bit binary mask used to divide an IP address into its network and host portions. It specifies which part of the IP address identifies the network and which part identifies individual devices (hosts) within that network.
- **Usage**: The term "netmask" can refer to any mask used to describe a network's IP range, regardless of whether it's a default network or a subnet.
- **Example**: In IPv4 addressing, a netmask of `255.0.0.0` (or `/8`) would indicate that the first 8 bits are for the network, while the remaining bits are for hosts.

### Subnet Mask
- **Definition**: A **subnet mask** is a specific type of netmask used when a larger network is divided into smaller subnetworks (or subnets). It defines the division between the network portion and the subnet/host portion within a network.
- **Usage**: Subnet masks are commonly used in the context of subdividing an IP network into smaller, manageable subnets. The concept is especially useful in complex networks to organize IP address space, control traffic, and enhance security.
- **Example**: In a `/24` subnet mask, written as `255.255.255.0`, the first 24 bits represent the network and subnet portion, while the last 8 bits are for hosts. This means the IP address space can support up to 256 addresses, with 254 usable for hosts.

### Key Differences
1. **Context**: 
   - **Netmask** refers broadly to any mask for identifying network/host boundaries.
   - **Subnet Mask** specifically refers to a mask used to define subnets within a larger network.

2. **Scope**: 
   - **Netmask** is often used in general terms for the primary network identifier.
   - **Subnet Mask** is used to define a smaller network segment within a larger network.

### Example in Practice
If you have a network `192.168.0.0` with a default netmask of `255.255.0.0`, this netmask indicates that `192.168.x.x` belongs to the same network. To create subnets, you could apply a subnet mask like `255.255.255.0` to break it into smaller segments, with each subnet supporting up to 254 hosts.

### In Summary
While the terms are closely related, **"netmask"** can apply generally to any network boundary mask, whereas **"subnet mask"** specifically indicates a mask used to divide a network into subnets.

<img width="793" alt="17" src="https://github.com/user-attachments/assets/f2c25971-2006-4dbb-a3ba-b865d724fcbc">

# CIDR notation

**CIDR (Classless Inter-Domain Routing)** is a method used to allocate IP addresses and route IP packets more efficiently. CIDR replaces the older, class-based IP addressing system, which grouped IP addresses into fixed classes (A, B, C, etc.). It was introduced to help conserve IP addresses and allow more flexible IP address allocation and subnetting.

### How CIDR Works
CIDR notation represents an IP address followed by a forward slash (`/`) and a number, which specifies the number of bits in the **network prefix**. This prefix determines how many bits are used for the network portion of the address, with the remaining bits available for hosts within that network.

#### Example of CIDR Notation
- `192.168.1.0/24`
  - Here, `/24` means the first 24 bits are the network portion, leaving the last 8 bits for host addresses.
  - The corresponding subnet mask is `255.255.255.0`.
  - This allows for 256 total IP addresses (254 usable for hosts, as two addresses are reserved).

- `10.0.0.0/8`
  - In this case, `/8` means the first 8 bits are for the network, leaving 24 bits for hosts.
  - The subnet mask here is `255.0.0.0`.
  - This CIDR block can support up to 16,777,214 usable IP addresses.

### Benefits of CIDR
1. **Efficient Address Allocation**: CIDR enables networks to use only the number of IP addresses they need, reducing waste and conserving IP address space.
2. **Flexible Subnetting**: Unlike class-based addressing, CIDR allows for creating networks of various sizes by adjusting the subnet mask length.
3. **Simplified Routing**: CIDR allows IP addresses to be aggregated (or "summarized") to reduce the size of routing tables, improving routing efficiency.

### Calculating Network Range in CIDR
To determine the range of IP addresses in a CIDR block:
- **Network Address**: The first address in the range, where all host bits are set to 0.
- **Broadcast Address**: The last address in the range, where all host bits are set to 1.
  
For example, `192.168.1.0/24` covers addresses from `192.168.1.0` to `192.168.1.255`.

### CIDR vs. Subnet Mask
While CIDR notation uses a prefix length (like `/24`), a **subnet mask** is a 32-bit number written in dotted-decimal format (e.g., `255.255.255.0`). Both represent the same network boundary but in different formats.

### Common CIDR Blocks
| CIDR Notation | Subnet Mask       | Number of Addresses | Usable Hosts |
|---------------|-------------------|----------------------|--------------|
| /8            | 255.0.0.0         | 16,777,216          | 16,777,214   |
| /16           | 255.255.0.0       | 65,536              | 65,534       |
| /24           | 255.255.255.0     | 256                 | 254          |
| /30           | 255.255.255.252   | 4                   | 2            |

### CIDR in Practice
CIDR is widely used in network design and is the standard notation in cloud environments like AWS, Azure, and GCP, where VPCs or subnets are often created with CIDR blocks (e.g., `10.0.0.0/16`). CIDR makes it easy to divide IP ranges efficiently for subnets, improving resource allocation and network management.

# Calculators

- https://www.davidc.net/sites/default/subnets/subnets.html
- https://mxtoolbox.com/subnetcalculator.aspx
- https://jodies.de/ipcalc?host=10.0.0.0&mask1=16&mask2=
