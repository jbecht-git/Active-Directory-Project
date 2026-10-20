 # Active Directory Home Lab

<div align="center">

**Fully-configured Active Directory environment built from scratch on Oracle VirtualBox containing 1,000 user profiles, RAS/NAT, DHCP, and a Dual-NIC Domain Controller**

</div>

## Why I Started This Project

There are many different entry-level IT concepts that are incorporated by Active Directory; IP addressing/Routing, creating and joining domains, and a lot more that aren't necessarily easy to fully grasp without hands on experience.

In this lab, I built everything from scratch on my personal computer to gain realistic experience with all of these concepts and to further my understanding of enterprise-level directories.

## Lab Objectives

* **Build a functional Windows domain environment using Active Directory**

* **Ensure that clients connect to the internet through the internal network and are automatically provided IP addresses**

## Architecture
![alt text](https://github.com/jbecht-git/Active-Directory-Project/blob/864f593631940dbbdda22215d4b9fb4fe414b713/AD_Architecture.drawio.png)

## Network Configuration

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



| Setting | Info |
| -------- | -------- |
| Fully Qualified Domain Name  | mydomain.com  |
| Domain Controller Hostname  | DC  |
| Client Hostname | Client1 |
| Domain Admin | a-jbecht |
| Total Users | 1,000 |


## What I Used

### Oracle VirtualBox
Used to simulate the Client and Domain Controller OSs

### Windows 11 Pro
Installed on the Client VM to connect to the domain.

### Windows Server 2025
Installed on the Domain Controller VM to host the active directory.

### Remote Access Server w/ NAT
Installed onto the Active Directory so the Client could receive internet connection through the internal network. Also made it possible for the DC and Client to share a public IP, increasing security and limiting the amount of public IPs used from "office machines".

### DHCP
Provides automatic internal IP addressing to the Client VM. Also used by the external network to connect to the local router and establish a connection to the internet.

### Domain
Links the Client VM to the Active Directory, linking all accounts stored in the the AD accessible from one machine.

### Powershell
Ran a script that took 1,000 random names from a .txt file and added them as users in the domain with credentials ready to go.


## Step-By-Step
If you are interested in doing this project yourself or seeing how I did it, feel free to follow along using the instructions below.

<div align="center">
 
![Step-By-Step Instructions](https://github.com/jbecht-git/Active-Directory-Project/blob/de709646d99f324cf11fb87b8980829577c1d625/Step-By-Step%20Instructions.md)

</div>

## What I learned

### Virtualization
* Delegate hardware and run multiple VMs at the same time
* Install operating systems from ISO files onto a Virtual Machine


### Setting up an Active Directory and Domain
* Elevate users to the "Administrator" level
* Manage credentials for many users at once
* Set up and joined a domain


### Building and Maintaining a Network
* Install and configure DHCP addressing for an internal network
* Configure RAS and NAT to provide internet access to clients directly through the domain controller


