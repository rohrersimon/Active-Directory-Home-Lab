<h1>Active Directory Home Lab</h1>

<h2>Description</h2>
Project creates a virtual network environment with one server (DC) and a client (Client1). The Active Directory on the server is configured with 1000+ accounts through a PowerShell script. 
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
I was creating a virtual machine to install Windows Server 2019 and ran into strong performance issues: The mouse was so slow it became impossible to click on things. When typing, the letters would show up only about a minute later. I had different theories about what could be the problem. I went through the troubleshooting process step-by-step:

 - Performance of my laptop: Ruled out because of i7 Intel processor and 8Gb RAM on my host device.
 - Hardware ressources allocated to virtual machine: Increased from 1Gb to 2Gb RAM and gave it 2 instead of 1 CPU core. No significant change in performance.
 - Virtualisation not activated in BIOS (UEFI in my laptop's case): This ended up to be the solution. However, I had to research the difference between Windows own Hyper-V technology which is definitely not what Virtualbox uses and Intel's VT-x which is what I needed. After activating VT-x Virtualbox performed as expected.
<br />
<img src="https://i.imgur.com/YSYWoaM.png" height="80%" width="80%" />
<br />
<br />
With Virtualbox now running as intended, I went ahead and created the first virtual machine to serve as our Windows Server 2019 and Active Directory Domain Services (DC on the Network plan). <br />
<br />
<img src="https://i.imgur.com/U44F7td.png" height="80%" width="80%" />
<br />
<br />
Then, I installed the Remote Access and DHCP features on our server to allow our client system (Client1) to access the internet through our sever in the future. <br />
<br />
<img src="https://i.imgur.com/FaRqFu1.png" height="80%" width="80%" />
<br />
<br />
The last server configuration is to define the IP address range for the DHCP and make sure the feature is actually running. <br />
<br />
<img src="https://i.imgur.com/ZES08fo.png" height="80%" width="80%" />
<br />
<br />
Run a PowerShell script that creates 1000 users. Full disclosure: I did not write this script myself but I made sure I understand what each line does. It essentially uses a text file with 1000 names in it to automatically create a useranme, password, and account for each one. <br />
<br />
<img src="https://i.imgur.com/uPBlV91.png" height="80%" width="80%" />
<br />
<br />
It's time to create the Client1 virtual machine (VM). I originally wanted to install Windows 11 on a machine with one CPU core and 1024Gb RAM allotted to it. However, that lead to an error message. <br />
<br />
<img src="https://i.imgur.com/gqlLZVo.png" height="80%" width="80%" />
<br />
<br />
Turns out the minimum requirements from Microsoft for Windows 11 machines are 4Gb RAM. My actual PC has 8Gb RAM and it needs to run the host OS, the server VM, as well as the client VM. My solution is to install Windows 10 which only requires 2Gb RAM in 64-Bit systems.<br />
<br />
<img src="https://i.imgur.com/73txff3.png" height="80%" width="80%" />
<br />
<br />
