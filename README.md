<h1>Active Directory Home Lab</h1>

<h2>Description</h2>
Project creates a virtual network environment with one server (DC) and a client (Client1). The Active Directory on the server is configured with 1000+ accounts using a simple PowerShell script. 
<br />

<h2>Software & Tools Used</h2>

- <b>Active Directory</b> 
- <b>PowerShell</b>
- <b>Virtualbox</b>
- <b>Windows Server 2019</b>
- <b>Windows 11</b>

<h2>Project walk-through</h2>

<h3>Network plan for project environment</h3> 
<br />
<img src="https://i.imgur.com/vpqGEXe.png" height="80%" width="80%" />

<h3>Virtualbox performance issues</h2>
I was creating a virtual machine to install Windows Server 2019 and ran into strong performance issues: The mouse was so slow it became impossible to click on things. When typing, the letters would show up only about a minute later. I had different theories about what could be the problem. So, I went through them one-by-one:

 1. Performance of my laptop: Ruled out because of i7 Intel processor and 8Gb RAM on my host device.
 2. Not enough hardware resources allocated to virtual machine (VM): Increased RAM from 1Gb to 2Gb and gave it 2 instead of 1 CPU core. No significant change in performance.
 3. Virtualisation not activated in BIOS (UEFI in my laptop's case): This ended up being the solution. However, I had to research the difference between Windows own Hyper-V technology which is not what Virtualbox uses and Intel's VT-x which is what I needed. After activating VT-x, Virtualbox performed as expected.
<br />
<img src="https://i.imgur.com/YSYWoaM.png" height="80%" width="80%" />
<br />
<br />
With Virtualbox now running as intended, I went ahead and created the first VM to serve as our Windows Server 2019 and Active Directory Domain Services ('DC' on the Network plan). <br />
<br />
<img src="https://i.imgur.com/U44F7td.png" height="80%" width="80%" />
<br />
<br />
Then, I installed the Remote Access and DHCP features on our server to allow our client system (Client1) to access the internet through the sever in the future. <br />
<br />
<img src="https://i.imgur.com/FaRqFu1.png" height="80%" width="80%" />
<br />
<br />
The last configuration was to define the IP address range for the DHCP and make sure the feature is  running. <br />
<br />
<img src="https://i.imgur.com/ZES08fo.png" height="80%" width="80%" />
<br />
<br />
Time for the PowerShell script that creates 1000 users. It essentially uses a text file with 1000 names to automatically create a username, password, and account for each name in the file.<br />
<br />
<img src="https://i.imgur.com/uPBlV91.png" height="80%" width="80%" />
<br />
<br />
It's time to create the Client1 VM. Originally, I wanted to install Windows 11 on a machine with one CPU core and 1024Gb RAM allotted to it. However, that lead to an error message. <br />
<br />
<img src="https://i.imgur.com/gqlLZVo.png" height="80%" width="80%" />
<br />
<br />
Turns out the minimum requirements from Microsoft for Windows 11 machines are 4Gb RAM. My host system has 8Gb RAM and it needs to run the host OS, the server VM, as well as the client VM. This is too much for my laptop. The solution I came to was installing Windows 10 which only requires 2Gb RAM in 64-Bit systems. That way my laptop would not be overburdened.<br />
<br />
<img src="https://i.imgur.com/73txff3.png" height="80%" width="80%" />
<br />
<br />
After installing Windows 10 the DHCP automatically gave the Client1 an IP address and connectivity to the internet worked as well.<br />
<br />
<img src="https://i.imgur.com/NREpAyM.png" height="80%" width="80%" />
<br />
<br />
To make sure the local domain works (mydomain.com), I restarted Client1 and logged into the system using an account I created with the PowerShell script on the server earlier.<br />
<br />
<img src="https://i.imgur.com/yOfkwdn.png" height="80%" width="80%" />
<br />
<br />
Now, I can login with any user created with the PowerShell script from Client1 and the system is connected to the server and the internet.<br />
<br />
<img src="https://i.imgur.com/WjUyiUw.png" height="80%" width="80%" />
<br />
<br />
