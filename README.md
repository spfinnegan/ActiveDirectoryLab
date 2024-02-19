<h1>Active Directory Home Lab</h1>


<h2>Description</h2>
Project consists of creating an Active Directory home lab environment within virtual box, to include setting up routing, NAT, and users to login to the domain via a second virtual machine. Project assumes knowledge of how to set up virtual machines within virtual box. ISO's are downloaded directly from Windows. Setup the DC in virtual box as any normal virtual machine, with one notable change at the beginning. 

<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Windows Server 2019</b>
- <b>Oracle Virtual Box</b>

<h2>Program walk-through:</h2> 


<p align="center">
Make sure your DC has two NICS set up in the network tab; one for the external internet and one for the internal. Then, turn on the VM and let the OS load onto the VM: <br/>
<img src="https://imgur.com/kA7H1OL.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
First thing we want to check after all the setup gets done is to verify we have two NICS:  <br/>
<img src="https://imgur.com/noflJFd.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
By looking in the properties of both NICS, we can see which one has a working IP and which has an APIPA address. We name the workking one Internet. : <br/>
<img src="https://imgur.com/jfpsU4S.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
We assign our internal NIC to an IP address we want it to be:  <br/>
<img src="https://imgur.com/Ci1pLjC.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
Now we want to install Active Directory Domain services, so we click on "Add Roles and Features":  <br/>
<img src="https://imgur.com/NQhhwWf.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
We select the Active Directory Domain Services and then use the default settings and install:  <br/>
<img src="https://imgur.com/Iyq3MVU.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
After this installs, there's a little attention flag in the upper right hand corner because we set up the software to create a domainm but we don't actually have a domain. We click on that and see this. We will add a new forest and name it what we want the domain to be called. We can use default settings and select next from here until it installs:  <br/>
<img src="https://imgur.com/QLSjwib.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
The server will automatically restart after this and we will now be logging into our domain:  <br/>
<img src="https://imgur.com/M6CHFIW.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
After logging in, click on start and go to Active Directory Users and Computers:  <br/>
<img src="https://imgur.com/CcDpKdD.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
</p>

  
<p align="center">
Right click on my domain and creare a new organizational unit for admins:  <br/>

</p>

<p align="center">
<img src="https://imgur.com/gvH7anC.png" height="80%" width="80%" alt="AD setup steps"/>
Within that admin folder, create an admin users:  <br/>
<img src="https://imgur.com/QfWQ0tc.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
Go to member of and add into domain admins:  <br/>
<img src="https://imgur.com/I6sH9Xl.png" height="80%" width="80%" alt="AD setup steps"/>
Log in with your newly created admin account and now lets create routing. Go into server manager and add roles and features and select next until we get to select "Remote Access":  <br/>
<img src="https://imgur.com/gOb1cxd.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
Make sure to install Routing:  <br/>
<img src="https://imgur.com/WrPKcCL.png" height="80%" width="80%" alt="AD setup steps"/>
Default settings and next through all of this:  <br/>
<img src="https://imgur.com/qurMpdu.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
After installation, we go to tools and select routing and remote access and see this:  <br/>
<img src="https://imgur.com/ozzLIR5.png" height="80%" width="80%" alt="AD setup steps"/>
Right Click on DC(local) and select routing and enable:  <br/>
<img src="https://imgur.com/eHlpPT8.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
Default through all of this and make sure that NAT is checked, as this is how our second virtual machine will connect to the internet:  <br/>
<img src="https://imgur.com/ENrE9UG.png" height="80%" width="80%" alt="AD setup steps"/>
Both our NICS are visible and we want to make sure our internet NIC is selected. This is why we named them earlier:  <br/>
<img src="https://imgur.com/cUcrilS.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
Add roles and features and setup a DHCP Server:  <br/>
<img src="https://imgur.com/qZFjOpu.png" height="80%" width="80%" alt="AD setup steps"/>
Next through all of this:  <br/>
<img src="https://imgur.com/9T47Pwz.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
Now we need to setup our scope:  <br/>
<img src="https://imgur.com/lnpkQhr.png" height="80%" width="80%" alt="AD setup steps"/>
This is the range we want to use:  <br/>
<img src="https://imgur.com/ZgxDSyj.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
This is the router we want our machines to use, which is the server. This is why we set up NAT earlier:  <br/>
<img src="https://imgur.com/pxp1skm.png" height="80%" width="80%" alt="AD setup steps"/>
DHCP is all set up:  <br/>
<img src="https://imgur.com/KWPuCMA.png" height="80%" width="80%" alt="AD setup steps"/>
Now that my domain, NAT, and routing for my clients is done, now we need some users! This is a powershell script to create a thousand users, plus some custom ones, to make a user group and users to save time:  <br/>
<img src="https://imgur.com/WumxLEI.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
It finsihed running and now I have a group called _USERS full of objects:  <br/>
<img src="https://imgur.com/PprquCb.png" height="80%" width="80%" alt="AD setup steps"/>
Now I setup a windows 10 machine in virtual box in the same one, making sure my network settings are to use an internal NIC only:  <br/>
<img src="https://imgur.com/v7Lm03k.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
We setup the machine, ensuring to use Windows Pro and not Home as Home versions cannot join domains. Make sure to select "Domain Join Instead" when doing the initial setup. After it finishes setting up, this is what IP address we have:  <br/>
<img src="https://imgur.com/6RmI9o8.png" height="80%" width="80%" alt="AD setup steps"/>
We have successfully recieved an IP from our DC within our range and can travel the internet through it. Now, lets join the domain. Click on "View Advanced System Settings" and go to computer name and select change. We see this, and now we give the machine a name and join the domain we created earlier:  <br/>
<img src="https://imgur.com/TuzrGdZ.png" height="80%" width="80%" alt="AD setup steps"/>
Back on the server, we can see that the pc we just named and added to the domain is in the computers folder:  <br/>
<img src="https://imgur.com/nv4jd7k.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />
I created a username with my wifes name on the server, and now she can log in to the Windows 10 machine to join the domain:  <br/>
<img src="https://imgur.com/7qMHzg1.png" height="80%" width="80%" alt="AD setup steps"/>
And now, to verify the Windows 10 machine is only getting internet through my server, I turned my server virtual machine off and tried to go online with my Windows 10 machine, but I can't:  <br/>
<img src="https://imgur.com/8Ek3x9P.png" height="80%" width="80%" alt="AD setup steps"/>
<br />
<br />









</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
