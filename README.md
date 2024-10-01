<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
The purpose of this project is to explain the process of setting up Active Directory using the Azure platform including connection to an endpoint and user creation.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Remote Desktop and a laptop that is capable of  using Remote Desktop Protocol
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2019
- Windows 11 (23H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory & Promotion To Domain Controller
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create an additional users and attempt to log into client-1 with one of the users


<h2>Prerequisites</h2>

- Microsoft Azure Subscription
- Creation of the following
	- Resource Group
	- Virtual Machines (Windows Server 2019 & Windows 11 Pro
	- Virtual Networks & Subnets
- Both Virtual Machines are to be set up under the same virtual network


<h2>Deployment and Configuration Steps</h2>

Environments & Technologies Used
- Microsoft Azure (Virtual Machines)
- Active Directory Domain Services
- Remote Desktop and a laptop that is capable of  using Remote Desktop Protocol
- Windows Powershell

<h3>Step 1 - Setup Resources in Azure</h3>

- Resource Group - rg-lab-03
- Virtual Machine 1 (Windows Server): DC-01
- Virtual Machine 2 (Windows 11 pro client): CL-01
- Initial username: testadmin
- Network: provided by platform or can be suggested

Resource Group creation

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/5022b374-ce96-4753-8634-a3583ad67dd4)

Virtual Machine Setup

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/e86ca4c4-9e9e-4339-b6ed-2ee9997a2c43)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/b040e942-6f94-4b61-87b0-59da47e9d493)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/26d21cbe-dd58-4215-ad66-68cb7614b55d)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/72739f65-cf78-4638-b3f0-ec9b28878931)

Click Next

Disk field has already being filled based on the settings in the previous tab, but amend if required

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/e5228ef6-6dc9-40ca-9587-aa1399ce7fae)


Networking Tab
![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/54e24a74-7776-4180-bc8e-c988c221463f)


Select Create new for the Virtual network
![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/1c89350b-b343-4019-9cd7-02aa5a14d868)


Then click Review and Create

The server will now be created and deployed (Note, duration may vary)
![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/3dbbec73-2bfe-46cb-ad77-2b36794965a0)


NOTE: As part of this, the "NetworkWatcher RG resource group is also automatically created in addition to the Network Interface, Network Security Group, Publick IP Address

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/d8f3ae2a-2838-40ee-9fb5-c871c47231d2)


Creating the Client (Windows 11 Pro)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/22cc24bd-766f-44a3-9c20-d01d6c09b82d)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/37624d94-7ac5-4a3f-bb36-d19b6dbf5f58)


Disk tab

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/2a6db5d6-553d-40ee-9f3c-e0404004c704)


Network tab

Ensure the virtual network is the same as the windows server created previously

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/940ea0f9-b9e4-4a50-b59e-67cf1ee1432f)

Review & Create


Resource group post creation
![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/f39ea608-703d-48fa-9678-84d06d5dcb77)


<h3>Step 2 - Ensure Connectivity between the client and Domain Controller</h3>

Required

-Public IP address and private IP address of the both server and client

-Server IP addresses

Select the Virtual Machine DC-01

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/733dd69d-87c6-4314-996f-b5bbcd8af0c2)

Client IP Addresses
Select the Virtual Machine CL-01

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/2611d4f7-ae58-44a4-8e2f-6194ebb15e48)


Using the remote desktop tool, log into both client and server

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/b404bcde-6e1f-45f2-8f72-c952a2286959)

Connection to server completed

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/ed5ea5b5-2a3a-484d-9713-81135edab063)

Connection to Client via remote desktop

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/269e5f7d-3cd5-4d7a-860c-b5708a561d5d)

Connection to Windows 11 Pro successful

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/1641ff7a-8d0b-4e2c-9f61-fb024e4a99f8)


Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)

To enter the  Windows Powershell (Admin), right click on the start button and select Windows Powershell (Admin)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/fa3a2810-4325-4dbe-b38c-4e2d3dd03c9c)


Pinging the client CL-01  private ip address with a pepetual ping
- ping -t 10.0.0.5

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/23188a9a-403a-4a55-ab20-ffcdff56b770)

Ping unsuccessful due to ICMPv4 protocol being deactivated

Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall, repeat on the client as well

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/c0830c51-fccf-4057-a819-5e81703a038d)

Sort protocol by ICMP and view the Core Networking Diagnostics highlighted below

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/fd289f6c-e928-4c8b-a35a-660b678c728e)

Enable rule for both by highlighting and right-clicking and selecting enable rule

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/748b2ec0-6cf2-4991-b7df-9f210914bcf7)


Check back at Client-1 to see the ping succeed

Pinging DC-01 from the client CL-01 is successful


You can attempt to ping the client CL-01 from DC-01

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/5b0b3994-6e1a-464a-bc86-e3e4b618cb0e)

You can see the ping become successful once the rules have been enabled

<h3>Step 3 - Install Active Directory & Promotion To Domain Controller</h3>

Active Directory Installation 

While in Server Manager, click Add roles and features

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/94dc7f40-bfbe-4ff7-abe1-2a9701740f3d)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/dded5e47-85fa-430b-b156-a61eb9756842)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/b8648b75-4894-462e-a423-cc1dffb47c32)

Click Next, Select Active Directory Domain Services

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/7d9520c4-d33e-4f4a-854d-2cac7335004a)

On the next screen, click Add features and then Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/8c2695a6-a94e-4059-871c-977f97d7acb7)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/72c80a52-106e-41e9-81ec-1c30d76e70ae)

Click Install![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/a4774643-168d-48cf-ac37-d28153db8524)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/ff3d6194-cc5c-40d3-a802-c3481ee58dbb)

Once complete, there is a yellow flag in server manager![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/37bd0d74-5d68-411f-bdea-08694560cd08)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/a7593147-3180-4873-b7cd-c8d92054031f)

Promote as a DC: Setup a new forest as testdomain.com 

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/088802b6-6fe7-4891-9290-7ece40c1ae31)

Select Add a new forest and specify the root domain name and click next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/0e3378cb-bb73-4e61-b114-0c7b396df566)

Enter the password and click next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/21044514-bc71-4a1a-86bd-919f706fdd70)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/136a2b65-f923-4b4e-90d8-d0b2d969304c)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/028711c3-a903-49ca-a353-a47a14d970aa)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/1b761f34-b5a2-42ab-acb0-3104aced81af)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/9beb030d-81d3-4fd5-88ab-8c0835aaa4ca)

Click Next

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/c078b6f8-7575-44ce-a2ea-197ce8996b5f)

Click install

Please NOTE -You may be signed out as the system will restart


Restart and then log back into DC-1 as user: testdomain.com\testuser

<h3>Step 4 - Create an Admin and Normal User Account in AD</h3>

In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” & “_ADMINS”

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/555cf0dd-6fb2-4127-8bea-5aee14f1c646)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/d8ac5681-dbbd-4320-b373-06eda10f4721)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/6729bc35-7d47-48c1-b002-28d86f207d88)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/36907a06-64e9-4d9a-9495-496052becd6a)

Create a new employee named “john_admin” (same password) with the username of “john_admin”

Right click on _ADMINS and select "New", then "User"

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/d1ee1ff1-7e04-4204-a154-ab0721a30a93)

Enter the name of the user and add it to the user logon name

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/820e8757-a449-43e1-a9d3-55d16465f445)

Provide password

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/724f3b11-c3fb-424c-912f-737b01f939b6)

Click Next and Finish

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/54243167-2141-4b5d-a83b-11d101154194)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/35831ffc-70f9-4fb4-9bed-0c977bdd489c)

Add john_admin to the “Domain Admins” Security Group

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/b46db970-3ba0-4f57-ac0c-3d7a17dc06b2)

Right click on the user and click properties. Select Member Of and click Add

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/7460140c-1bf6-4a75-ba9d-37829e3f6f82)

Type domain and click Check names (shows all the available names. Select Domain Admins (to add the user to this group)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/6203d67c-bf5c-42e6-942d-45d969b6b7cf)

Click Apply & Ok. Updated membership below

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/b4d316cd-05ae-4651-b470-4e2aa2c8a4e0)

Log out/close the Remote Desktop connection to DC-01 and log back in as “testdomain.com\john_admin”

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/9daf18df-7c98-4ad0-be0e-c85006f5cef4)


<h3>Step 5 - Join Client-1 to your domain (testdomain.com)</h3>

From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address and restart Client-1

Go to Client-01 in Azure Portal and select Network settings, click Network Interface

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/5ad798e8-e429-4202-b605-c11cc71adb09)

Select DNS server

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/b61c4661-33f9-4c86-bf5f-7eb19499df60)

Change the setting to Custom and enter the private ip address for DC-01 (10.0.0.4), click save. This flushes the DNS cache and requires the use of the Domain Controller as the DNS

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/319daa4d-e5ac-469f-81f7-6515aa315edd)

Login to Client-1 (Remote Desktop) as the original local admin (testuser) and join it to the domain (computer will restart)

Go to the CL-01 page and click restart

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/fdfa183e-5fa8-489a-86f2-e68d189a18bf)

Once logged back in, click  start, and about. Then clock Domain or workgroup, Change

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/49b8d2c5-1835-483a-8869-7a541cdd3864)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/069e7fd5-438c-4eb6-be83-30e2dcc9fbf6)

Enter the domain "testdomain.com"

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/35ca9032-7213-4123-82be-4a47980dc2c7)

Sign in with testdomain.comj\ohn_admin and click ok.

Connection successful

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/2bb70090-fc7d-405b-abb5-3903c718d02a)

NOTE: The system will restart



Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/fd06277e-9458-45f1-baba-bd399e03c931)


<h3>Step 6 - Setup Remote Desktop for non-administrative users on Client-1</h3>

Log into Client-1 as mydomain.com\john_admin and open system properties

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/79ef33bf-35a8-4c69-9e6d-a8e8a81fa0ae)

Right click start and select system

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/42e5fccb-598e-47ed-89a1-58f2d9dec4a9)

Click “Remote Desktop”

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/5e2b3745-96ff-4dc3-9e21-08e74ed73905)

Select Remote Desktop Users

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/16b3a2b5-a635-45ef-9973-63018949d024)

Click add, enter domain and click check names

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/2826eb0f-417a-4235-9a02-f2cd2e545c18)

Allow “domain users” access to remote desktop

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/2d6cb82f-a164-466e-9996-708e3212c308)

You can now log into Client-1 as a normal, non-administrative user now


<h3>Step 7 - Create an additional users and attempt to log into client-1 with one of the users</h3>

Login to DC-1 as jane_admin
Create a new user Steph Curry  scurry

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/e9204122-96da-4ca3-8732-a0b462a41f0c)

When finished, open ADUC and observe the accounts in the appropriate OU attempt to log into Client-1 with one of the accounts 



![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/61a53861-ac93-4f34-aaa7-d9dc1be3f9ac)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/16aa81b8-2d65-48ad-b0c9-bdd734a411d2)

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/edf3cceb-b3b6-4125-ba6a-8b6a1ffa1c5f)

Log in as Steph Curry completed

![image](https://github.com/EmmanuelAOlu/configure_ad/assets/173094278/ecc5ddbd-295c-48a2-9999-6b8e272f8030)


<h2>Guide Complete</h2>


