Absolutely! Let's build your SOC Analyst Home Lab Notes – Kali Linux + Windows 10 (VirtualBox).
This will be your practical cybersecurity portfolio project. The goal is to create a small Security Operations Centre (SOC) environment where you practise monitoring computers, collecting security logs, investigating suspicious activity and identifying potential threats.
I'll structure these as learning notes that you can follow on your laptop and eventually use as evidence of practical experience on your CV.
SOC ANALYST HOME LAB
Project 1: Building a SOC Environment Using Kali Linux and Windows 10
1. Understanding your home lab
First, what exactly are we building?
A SOC (Security Operations Centre) is a team or department responsible for monitoring an organisation's computers and networks to identify and respond to cybersecurity threats.
As a SOC analyst, your responsibilities include:
1. Monitoring security events.
2. Identifying suspicious activities.
3. Investigating security alerts.
4. Analysing network traffic.
5. Detecting potential malware.
6. Documenting incidents.
7. Reporting security threats.
We will simulate some of these responsibilities at home.
Your lab architecture
You will use two virtual machines (VMs).
Virtual machine	Purpose
Kali Linux	Security analyst workstation
Windows 10	Monitored computer (victim/endpoint)
VirtualBox	Runs both virtual machines
How they work together:
• Windows 10 generates activity.
• Kali Linux helps you analyse network traffic and investigate the environment.
• You examine Windows security logs to understand what happened.
Think of Windows as the computer you're protecting and Kali as your investigation workstation.

2. Preparing your virtual machines
Before installing security tools, we need to prepare the environment.
Task 1: Check your VirtualBox configuration
Open VirtualBox.
Check that you have:
Kali Linux
• RAM: 3–4 GB.
• Processors: 2 (if available).
• Storage: At least 30 GB recommended.
Windows 10
• RAM: 4 GB.
• Processors: 2 (if available).
• Storage: At least 40 GB recommended.
Your laptop has 16 GB RAM, so these allocations should be manageable, although avoid running other demanding applications simultaneously.
Task 2: Configure networking
We need the two virtual machines to communicate.
VirtualBox provides different networking modes.
Network mode	Explanation
NAT	Allows a VM to access the internet.
Bridged	Connects a VM directly to your physical network.
Host-only	Allows communication between your host and VMs.
Internal Network	Allows VMs on the same internal network to communicate.
For this project, use Host-only networking.
Steps:
1. Open VirtualBox.
2. Select your Kali VM.
3. Open Settings.
4. Select Network.
5. Under Adapter 1, select Host-only Adapter.
6. Choose your VirtualBox host-only network.
7. Repeat for Windows 10.
8. Start both machines.
Use NAT temporarily when you need internet access for updates or downloading software. Return to the isolated network for lab exercises.
Important: Keep this lab isolated from your everyday home network.

3. Learning your Kali Linux tools
Kali Linux is a Linux distribution containing cybersecurity and network analysis tools.
You don't need to learn every tool. Focus on the ones useful for entry-level SOC work.
Task 3: Update Kali Linux
Open your Kali terminal.
Run:

sudo apt update
Then:

sudo apt upgrade
These commands update your package information and installed software.
Task 4: Install essential tools
Install Wireshark:

sudo apt install wireshark
Install Nmap:

sudo apt install nmap
Install tcpdump:

sudo apt install tcpdump
Install curl:

sudo apt install curl
Understand what each tool does
Tool	SOC application
Wireshark	Analyses network traffic.
Nmap	Identifies devices and open services on a network.
tcpdump	Captures network packets through the terminal.
curl	Makes HTTP requests and helps investigate web connections.
Terminal	Runs commands and performs investigations.
Your learning objective: Understand what each tool does and when a SOC analyst would use it.

4. Preparing Windows 10 for security monitoring
This is one of the most important parts of your lab.
SOC analysts need visibility into what happens on computers.
This information is collected through something called logs.
A log is a record of an event that happened on a computer.
Examples:
• Someone logged into Windows.
• Someone entered an incorrect password.
• A program started.
• A new file was created.
• A network connection was established.
Task 5: Explore Windows Event Viewer
Windows has a built-in tool called Event Viewer.
It records events happening on your computer.
Steps:
1. Start Windows 10.
2. Press Windows + R.
3. Type:

eventvwr
4. Press Enter.
5. Expand Windows Logs.
You will see:
Log	What it records
Application	Events involving applications.
Security	Security-related events.
System	Windows system events.
Setup	Windows installation and configuration events.
Your practical exercise:
1. Open Security.
2. Examine the recorded events.
3. Find Event ID 4624.
4. Identify what happened.
5. Find Event ID 4625.
6. Identify what happened.
Important Event IDs:
Event ID	Meaning
4624	Successful login.
4625	Failed login.
4634	Account logged out.
4648	Login using explicit credentials.
4688	New process created.
4720	User account created.
These are useful events to recognise during security investigations.

5. Installing Sysmon
Task 6: Install Microsoft Sysmon
This is one of the most valuable tools for your SOC home lab.
Sysmon (System Monitor) is a Microsoft tool that records detailed information about activities on Windows computers.
It provides additional visibility beyond ordinary Windows logs.
For example:
• Programs being executed.
• Network connections.
• File creation.
• DNS queries.
• Process activity.
Download it from Microsoft's official Sysinternals website:
Microsoft Sysmon Download
Installation:
1. Download Sysmon.
2. Extract the ZIP file.
3. Open Command Prompt as Administrator.
4. Navigate to the extracted folder.
5. Run:

sysmon64.exe -accepteula -i
This installs Sysmon with its default configuration.
Task 7: Explore Sysmon logs
Open Event Viewer.
Navigate to:

Applications and Services Logs
    Microsoft
        Windows
            Sysmon
                Operational
Look for these Event IDs:
Event ID	Activity
1	Process creation
3	Network connection
11	File creation
22	DNS query
Practical exercise:
1. Open Notepad.
2. Create a new text document.
3. Save it.
4. Open Event Viewer.
5. Examine the Sysmon logs.
6. Look for evidence of the activity you performed.
This is how you start learning endpoint monitoring.

6. Network traffic analysis
Now we move to Kali Linux.
A SOC analyst needs to understand what happens when computers communicate over a network.
Task 8: Discover your IP addresses
An IP address is a numerical address assigned to a device on a network.
On Kali:

ip addr
On Windows:

ipconfig
Record both IP addresses.
You should see that both computers have addresses belonging to the same host-only network.
Task 9: Test connectivity
From Kali, try communicating with your Windows VM:

ping WINDOWS_IP_ADDRESS
Replace WINDOWS_IP_ADDRESS with the actual Windows IP.
For example:

ping 192.168.56.101
If successful, Kali and Windows can communicate.
Note: Windows Firewall may block ping requests, so an unsuccessful result doesn't automatically mean your network configuration is wrong.
Task 10: Capture network traffic using Wireshark
Open Wireshark on Kali.
1. Select your host-only network interface.
2. Start capturing packets.
3. Generate some normal network activity between your two VMs.
4. Observe the packets.
5. Stop the capture.
Learn these basic protocols:
Protocol	Purpose
TCP	Reliable communication between devices.
UDP	Connectionless communication.
DNS	Converts domain names into IP addresses.
HTTP	Transfers web information.
HTTPS	Encrypted web communication.
ICMP	Used for network diagnostics, including ping.
Try these Wireshark filters:

dns

tcp

icmp

http
Your objective is to recognise different types of network traffic.

7. SOC investigation exercises
Now we start behaving like actual SOC analysts.
These exercises will help you practise investigating events instead of simply learning commands.
Exercise	What you must investigate	Tool
1	Successful Windows login	Event Viewer
2	Failed login event	Event Viewer
3	Process creation	Sysmon
4	File creation	Sysmon
5	Network connections	Wireshark
6	DNS requests	Wireshark / Sysmon
7	Identify network devices	Nmap
8	Investigate suspicious-looking activity	Event Viewer / Sysmon
Only investigate activity within your own lab.
Example investigation
Imagine Windows records a new process being created.
As a SOC analyst, you should ask:
1. What program was executed?
2. When was it executed?
3. Which user executed it?
4. What was the parent process?
5. Was the activity expected?
6. Is there anything suspicious that requires further investigation?
This is called security event investigation.

8. Learning SIEM tools
Eventually, we want to introduce a SIEM.
SIEM = Security Information and Event Management.
A SIEM collects logs from different computers, organises them and helps security analysts identify suspicious activity.
Some popular SIEM platforms:
SIEM	Description
Splunk	Collects and analyses security data.
Wazuh	Open-source security monitoring platform.
Microsoft Sentinel	Microsoft's cloud-based SIEM.
Elastic Security	Security monitoring and threat detection.
My recommendation is to learn Wazuh first.
Why?
• It has a free, open-source option.
• It provides endpoint monitoring.
• It collects and analyses security events.
• It supports security alerting.
• It is relevant to SOC analyst skills.
Official website:
Wazuh Documentation
We can make installing Wazuh your second major home lab project. It may require another Linux VM, so we'll plan its resource requirements before installing it.

9. Your SOC home lab task checklist
Here is your practical roadmap.
No.	Task	Status
1	Install VirtualBox	☐
2	Install Kali Linux	☐
3	Install Windows 10	☐
4	Configure host-only networking	☐
5	Update Kali	☐
6	Install Wireshark	☐
7	Install Nmap	☐
8	Install tcpdump	☐
9	Explore Windows Event Viewer	☐
10	Install Sysmon	☐
11	Investigate Windows Event IDs	☐
12	Capture network traffic	☐
13	Investigate DNS requests	☐
14	Complete SOC investigation exercises	☐
15	Install and configure Wazuh	☐
16	Investigate SIEM alerts	☐
17	Document your investigations	☐
18	Publish your project on GitHub	☐

10. Building your CV portfolio
This is extremely important.
Don't just install tools. Document what you learn and what you accomplish.
Create a GitHub repository called:
SOC-Analyst-Home-Lab
Organise it like this:

SOC-Analyst-Home-Lab/
│
├── README.md
│
├── 01-Lab-Setup/
│   └── VirtualBox-Configuration.md
│
├── 02-Kali-Linux/
│   └── Tools-and-Commands.md
│
├── 03-Windows-Monitoring/
│   └── Event-Viewer.md
│
├── 04-Sysmon/
│   └── Sysmon-Installation.md
│
├── 05-Network-Analysis/
│   └── Wireshark-Analysis.md
│
├── 06-Investigations/
│   └── Investigation-Reports.md
│
└── 07-SIEM/
    └── Wazuh-Analysis.md
Example CV entry once completed
SOC Analyst Home Lab – Personal Cybersecurity Project
• Built an isolated cybersecurity home lab using Kali Linux, Windows 10 and VirtualBox.
• Configured Windows security monitoring using Microsoft Sysmon.
• Investigated Windows authentication and process creation events.
• Analysed network traffic using Wireshark.
• Practised identifying DNS requests, TCP connections and network activity.
• Configured SIEM monitoring and investigated security alerts using Wazuh.
Only list the activities you have actually completed.

11. Your recommended learning order
I don't want you rushing into 15 different tools without understanding what they do.
Follow this order:
Week	Focus	Main outcome
Week 1	VirtualBox and networking	Working home lab
Week 2	Windows Event Viewer	Understanding security logs
Week 3	Sysmon	Endpoint monitoring
Week 4	Wireshark	Network traffic analysis
Week 5	SOC investigations	Investigation reports
Week 6	Wazuh	SIEM monitoring
Week 7	Alert investigation	Practical SOC experience
Week 8	GitHub portfolio	Documented project
You can adjust the pace depending on your NetGuardians classes.

My advice: Start with these three priorities
Since you're beginning your SOC analyst journey, I would prioritise:
1. Windows Event Viewer + Sysmon
Learn how to identify what is happening on a Windows computer.
2. Wireshark
Learn how to understand network traffic and identify unusual communication.
3. Wazuh
Learn how professional security monitoring platforms collect and generate alerts.
These three areas will give you a solid foundation for entry-level SOC analyst skills.
One important thing: Your goal isn't to become an expert in Kali Linux. Your goal is to become someone who can investigate security events, understand what happened and explain why it matters.
That's what employers want to see.
Your first practical milestone
Get both VMs running, configure their networking, and successfully capture traffic from your lab using Wireshark.
Once you've done that, you'll have the foundation of your first SOC home lab!






From <https://chatgpt.com/c/6ae9ab85-d1b0-83e9-a13a-7875af5f633c> 
# notes
