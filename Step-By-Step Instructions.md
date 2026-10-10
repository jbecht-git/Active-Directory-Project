# Active Directory Home Lab Step-by-Step

---

# Instructions

*Setup Note:*

- Make sure your computer has virtualization capabilities and that any VM support is enabled from the BIOS (Restarts may be required)

1. **Download These Items:**  
   1. [Windows Server 2025 ISO](https://info.microsoft.com/ww-landing-evaluate-windows-server-2025.html?lcid=en-us&culture=en-us&country=us)  
   2. [Windows 11 ISO](https://www.microsoft.com/en-us/software-download/windows11)  
   3. [VirtualBox \+ Extension Pack](https://www.virtualbox.org/wiki/Downloads)  
2. **Open VirtualBox and Create a New Virtual Machine**
![Reference](https://github.com/jbecht-git/Active-Directory-Project/tree/0b46c15c9aa502bf4ac641bdbd04e211ad383cd9/Screenshots/Step%202%3A%20Create%20the%20Domain%20Controller%20VM)
   1. Name: Domain Controller  
   2. Version: Windows 11  
   3. ISO Image: Server 2025  
   4. Allocate hardware as needed  
   5. Make sure shared clipboard and drag’n’drop are set to bidirectional  
   6. Enable two network adapters, the first one should be set to NAT and the second one should be set to internal network  
   7. Start your Domain Controller VM  
3. **Set Up the Server**  ![Reference](https://github.com/jbecht-git/Active-Directory-Project/tree/0b46c15c9aa502bf4ac641bdbd04e211ad383cd9/Screenshots/Step%203%3A%20Set%20up%20the%20server)
    1. Install the Standard Desktop edition of the OS  
   2. If prompted, select custom install instead of upgrade  
   3. After installation apply a temp admin password (Password1)  
4. **Insert Guest Addition CD Image**  
   1. Click on the Devices Tab on the top of the screen and select Insert Guest Addition CD image  
   2. Navigate to File Explore and go to this PC  
   3. Select CD Drive (D:) VirtualBox Guest additions then run the .amd64 file inside  
   4. Press next twice then install and manually reboot the server VM  
5. **Setting Up IP Addressing**  ![Reference](https://github.com/jbecht-git/Active-Directory-Project/tree/6ccd9ae12002d838b06c8c6175525ea96432c82e/Screenshots/Step%205%3A%20Setting%20up%20IP%20addressing)
    1. Navigate to Advanced Network Settings in the Control Panel, you should see two adapters. Determine which is for the internal network and which is for the external network and rename accordingly.  
      1. External IP will probably be a 10.0 address  
      2. Internal Ip will have an APIPA address  
   2. Assign an IP to your Internal Network Adapter  
      1. Click the drop down menu and select the edit button then navigate to IPv4 and double-click  
      2. Input a manual IP, mask, and DNS  
   3. Rename computer to DC in system settings and restart  
6. **Install Active Directory Domain Service**  ![Reference](https://github.com/jbecht-git/Active-Directory-Project/tree/130cfc601a20dd9a834e486c69dd45b41dd10a1f/Screenshots/Step%206%3A%20Install%20Active%20Directory%20Domain%20Service)
    1. Navigate to your server manager and click add roles and features  
   2. Click next until you get to server roles and select Active Directory Domain Services and add feature and install  
7. **Promote to a Domain Controller**  ![Reference](https://github.com/jbecht-git/Active-Directory-Project/tree/3879d0c37508d5b45be606274c9f04fbadfe5fd2/Screenshots/Step%207%3A%20Promote%20to%20a%20Domain%20Controller)
    1. Click the flag in the top right corner of your server manager and click “Promote this server to a domain controller”  
   2. Select “Add a new forest” and specify the root domain name ([mydomain.com](http://mydomain.com))  
   3. Click next and add a DSRM password (Password1)  
   4. Click next several times then click install and restart  
8. **Create a Domain Admin Account**  ![Reference](https://github.com/jbecht-git/Active-Directory-Project/tree/045bcf542870f571053415ad6e4ebd737030b92e/Screenshots/Step%208%3A%20Create%20a%20Domain%20Admin%20Account)
   1. Press start and navigate to Active Directory Users and Computers  
   2. Right click the domain, add a new OU  
   3. Name the OU “\_Admins” and uncheck the box underneath “Protect container from accidental deletion”  
   4. Right-click on the new \_Admins OU and select new then user  
   5. Add your first and last name, then create your admin logon name (a-jbecht)  
   6. Add a password to the account (Password1), uncheck “user must change password at next logon, and check password never expires  
   7. Finish, then right-click the newly appeared profile and select properties, member of, and add  
   8. In the box titled “Enter the object names to select” type “Domain Admins” and click on Check Names  
   9. Click okay and apply changes  
   10. Sign out and sign back in on the administrator account  
9. **Install RAS and NAT**  ![Reference](https://github.com/jbecht-git/Active-Directory-Project/tree/c61cc0ccfff697f9aae79ddb817b87da778355d2/Screenshots/Step%209%3A%20Install%20RAS%20and%20NAT)
   1. Navigate to your server manager and click add roles and features  
   2. Click next until you get to server roles and select Remote Access  
   3. Click next again until you get to Role services, select and install Routing (Direct Access and VPN should automatically be selected after this)  
   4. Click next and install  
   5. On the server manager, select tools then Routing and Remote Access  
   6. Right-click on the server and select “Configure and Enable Remote Access”  
   7. Click next and then select Network Access Translation (NAT)  
   8. Click next and make sure “Use this public interface to connect to the internet” is selected and Internet is highlighted (might need to exit and try again)  
   9. Click next and finish  
10. **Set up DHCP server on the Domain Controller**  
   ![Reference](
     1. Navigate to your server manager and click add roles and features  
    2. Click next until you get to server roles, select DHCP and install  
    3. On the server manager, select tools then DHCP  
    4. Right-click the domains IPv4 and select new scope  
    5. Name the scope (172.16.0.100-200)  
    6. Click next and define the IP address range (Start: 172.16.0.100 End: 172.16.0.200)  
    7. Define the length as 24 (Class C) and click next until you get to Configure DHCP options  
    8. Click yes and next, then type the domain controllers IP address for the Gateway (172.168.0.1) and click add  
    9. Click next and finish  
    10. Right-click the domain and select authorize then refresh IPv4 (should turn green after this)  
11. **(Optional) Turn off IE Enhanced Security Configuration**  
    1. Navigate to your server manager and click Configure this local server  
    2. In the properties section, click on IE Enhanced Security configuration and turn it off for admins and users  
12. **Create All Users**  
   ![Reference](
     1. Paste this [link](https://www.youtube.com/redirect?event=video_description&redir_token=QUZZTVljRlU1NHdsdTRQN3JmdFJQeWVoeEpGa3xBSTVJdTV0WjlCVjQwZzZ0MlNRenF6MG5DSXlTNFVjWjJPSjUxT3NtdTE4NVlYbUpwTldtZ2Q3NlVMYWNicXJFYk9VTkVtWnVMMHNOaXFxczRQU0dzUzJhSlpad0Qwd2sxbW92&q=https%3A%2F%2Fgithub.com%2Fjoshmadakor1%2FAD_PS%2Farchive%2Frefs%2Fheads%2Fmaster.zip&v=MHsI8hJmggI) into a browser to download the script and names file  
    2. Navigate to the names.txt file and add your name at the top in first/last name format, close  
    3. Open PowerShell ISE as administrator and open 1\_CREATE\_USERS  
    4. Enter the powershell command \> `Set-ExacutionPolicy Unrestricted`  
    5. Enter another command \> `cd c: \users\[account]\[location]\AD_PS-master`  
    6. Run the script  
13. **Create the Client VM**  
   ![Reference](
     1. Name: Client1  
    2. Version: Windows 11  
    3. ISO Image: Windows 11 ISO  
    4. Allocate hardware as needed  
    5. Make sure shared clipboard and drag’n’drop are set to bidirectional  
    6. Have one network adapter enabled and change it from NAT to internal network  
    7. Start your Client VM  
14. **Install Windows 11 Pro and Join the Domain**  
  ![Reference](
    1. On startup, select install Windows 11 Pro  
    2. When asked for a product key select “I don’t have a product key”  
    3. Custom install if prompted  
    4. Continue without internet  
       1. *If this doesn’t work press Shift+F10 and type* `oobe\bypassNRO` *into the command prompt*  
    5. Name the account “user” with no password  
    6. Once loaded into the home screen, click on Windows then System and Rename this PC  
    7. From the System About tab, Click on Domain or Workgroup and join the domain ([mydomain.com](http://mydomain.com))  
    8. If prompted for a user/password, use the admin account credentials (a-jbecht)  
    9. Restart
