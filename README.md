## Active Directory Home Lab

### Description
This project involves creating an Active Directory home lab environment within VirtualBox, including setting up routing, NAT, and users to log in to the domain via a second virtual machine. It assumes knowledge of setting up virtual machines in VirtualBox. Make sure you have Oracle VirtualBox, Server 19, Windows 10 ISO's. The steps start with configuring Server 19 in a normal way, with a notable exception of making sure it has two NIC's enabled.

### Languages and Utilities Used
- **PowerShell**

### Environments Used
- **Windows 10**
- **Windows Server 2019**
- **Oracle VirtualBox**

### DC Network Setup and AD Installation

Make sure your DC has two NICs set up in the network tab; one for external internet and one for internal. Then, turn on the VM and let the OS load onto the VM.

![AD setup steps](https://imgur.com/kA7H1OL.png)

First, verify that you have two NICs:

![AD setup steps](https://imgur.com/noflJFd.png)

Check the properties of both NICs and name the working one Internet:

![AD setup steps](https://imgur.com/jfpsU4S.png)

Assign an IP address to the internal NIC:

![AD setup steps](https://imgur.com/Ci1pLjC.png)

Install Active Directory Domain Services by clicking on "Add Roles and Features":

![AD setup steps](https://imgur.com/NQhhwWf.png)

Select Active Directory Domain Services, use default settings, and install:

![AD setup steps](https://imgur.com/Iyq3MVU.png)

After installation, add a new forest and name it:

![AD setup steps](https://imgur.com/QLSjwib.png)

The server will restart, and you will log into your domain:

![AD setup steps](https://imgur.com/M6CHFIW.png)

After logging in, go to Active Directory Users and Computers:

![AD setup steps](https://imgur.com/CcDpKdD.png)

### Creating Admin Organizational Unit

Right-click on the domain and create a new organizational unit for admins:

![AD setup steps](https://imgur.com/gvH7anC.png)

### Creating Admin User and Setting Up Routing

Within the admin folder, create an admin user:

![AD setup steps](https://imgur.com/QfWQ0tc.png)

Go to "Member Of" and add to domain admins:

![AD setup steps](https://imgur.com/I6sH9Xl.png)

Log in with the new admin account. To set up routing, go to Server Manager, add roles and features, and select "Remote Access":

![AD setup steps](https://imgur.com/gOb1cxd.png)

Install Routing and enable it:

![AD setup steps](https://imgur.com/eHlpPT8.png)

Default settings and next through all installations:

![AD setup steps](https://imgur.com/ENrE9UG.png)

Ensure NAT is checked, as this is how the second VM will connect to the internet:

![AD setup steps](https://imgur.com/cUcrilS.png)

### Setting Up DHCP Server

Add roles and features and set up a DHCP Server:

![AD setup steps](https://imgur.com/qZFjOpu.png)

Next through all of this, and set up the scope:

![AD setup steps](https://imgur.com/lnpkQhr.png)

Specify the range you want to use:

![AD setup steps](https://imgur.com/ZgxDSyj.png)

Specify the router (server) for the machines to use:

![AD setup steps](https://imgur.com/pxp1skm.png)

DHCP is now set up:

![AD setup steps](https://imgur.com/KWPuCMA.png)

### User Creation with PowerShell

Use a PowerShell script to create users:

![AD setup steps](https://imgur.com/WumxLEI.png)

Finished running, and now there's a group called _USERS full of objects:

![AD setup steps](https://imgur.com/PprquCb.png)

### Windows 10 Machine Setup and Domain Join

Set up a Windows 10 machine in VirtualBox using an internal NIC:

![AD setup steps](https://imgur.com/v7Lm03k.png)

Ensure it uses Windows Pro and not Home. Select "Domain Join Instead" during setup. After setup, the IP address is:

![AD setup steps](https://imgur.com/6RmI9o8.png)

Successfully received an IP from the DC within the range. Join the domain by changing the computer name:

![AD setup steps](https://imgur.com/TuzrGdZ.png)

On the server, see the PC added to the computers folder:

![AD setup steps](https://imgur.com/nv4jd7k.png)

Create a username on the server for login:

![AD setup steps](https://imgur.com/7qMHzg1.png)

Verify the Windows 10 machine gets internet through the server. Turn off the server VM and try to go online with Windows 10:

![AD setup steps](https://imgur.com/8Ek3x9P.png)

The Windows 10 machine can't go online without the server.
