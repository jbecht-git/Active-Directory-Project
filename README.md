 # Active Directory Home Lab

<div align="center">

**Fully-configured Active Directory environment built from scratch on Oracle VirtualBox containing 1,000 user profiles, NAT, DHCP, and a Dual-NIC Domain Controller**

</div>

# Why I Started This Project

There are many different entry-level IT concepts that are incorporated by Active Directory; IP addressing, group policy, creating and joining domains, and a lot more that aren't necessarily easy to fully grasp without hands on experience.

In this lab, I built everything from scratch on my personal computer to gain realistic experience with all of these concepts and further my understanding of Information Technology.

# Architecture
![alt text](https://github.com/jbecht-git/Active-Directory-Project/blob/864f593631940dbbdda22215d4b9fb4fe414b713/AD_Architecture.drawio.png)

# Network Configuration

### IP Addressing


| Device | Address | Assignment |
| -------- | -------- | -------- |
| DC External NIC  | Dynamic  | DHCP from Router  |
| DC Internal NIC  | `172.16.0.1`  | Static  |
| DC Internal DNS | `127.0.0.1` | Loopback |
| Client Internal NIC | Dynamic | DHCP from DC |
| DHCP Scope | `172.16.0.100-200` | Pool |
| Subnet Mask | `255.255.255.0` | /24 |
| Default Gateway (Client) | `172.168.0.1` | DC Internal NIC |
| DNS Server (Client) | `172.16.0.1` | DC Internal NIC |


### Domain Configuration



|  |  |
| -------- | -------- |
| Fully Qualified Domain Name  | mydomain.com  |
| Domain Controller Hostname  | DC  |
| Client Hostname | Client1 |
| Total Users | 1,000 |


# What I Used

### Oracle VirtualBox


##

# What I Built


# Step-By-Step


# Screenshots


# What I learned
