# Capture-The-Flag1

## Objective:

This is a capture the flag project that I completed in my Cyber Infrastructure & Technology course. This project was designed to test the skills learned throughout the course. Two pre-configured VMs - one Windows 10 machine and one Ubuntu server machine - were given to conduct the investigation. The scenario is as follows: 

"An organization’s monitoring system identified suspicious download activities captured in a honeypot named Cowrie. The Splunk system recorded the event, but the system cannot be accessed because its operator, who was the head of the security investigation team, was recently released from the company. You were hired as a security analyst not long after.

Due to the recent events, there was not enough time to provide you with all the information required to freely access the system. However, the system administrator was able to provide you with access to the mail server and told you that all the data needed to access the system is stored on that server.

Your objective is to connect to the Splunk system, investigate the events, and identify a suspicious message to obtain the flag."

The Ubuntu server machine that was given contained the mail server. The Windows 10 machine was used to access the mail server for investigation. 


### Skills learned:
- Digital Forensics
- Basic knowledge and use of POP3
- Using telnet to connect to another endpoint in order to conduct an investigation 
- Experience with analyzing and interpreting logs generated from a honeypot
- Development of critical thinking and problem-solving skills in cybersecurity


### Tools used:
- VirtualBox
	- Windows 10
	- Ubuntu Server
- PowerShell
- Telnet
- POP3
- Splunk Enterprise
- Base64 Decoder

## Process:
*(NOTE: reference screenshots have been added where applicable with a description above each image. Specific areas have been outlined in red to draw attention to the particular action taken.)*
</br>
</br>

*Below are the tasks that were given for this project. Answers for each of the questions/tasks have been added as well.*

### Task 1: Connect to the mail server
#### "In this task, you will connect to the mail server and retrieve the important emails."
</br>

#### 1.) Inspect the Ubuntu VM and note the message about the POP3 protocol.
![CTF_T1_Step1](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/3d929f6e-2772-46f8-a01b-09bfd782f59b)
</br>
</br>

#### 2.) Which port does POP3 use? 
Port 110
</br>
</br>

#### 3.) Use Telnet to connect to the POP3 service via PowerShell. Were you successful? Why?
The Telnet cmdlet through PowerShell was not successful because it was not turned on on the machine.
![CTF_T1_Step3](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/91531332-9207-4f84-84a5-9ae9c5b76e91)
</br>
</br>

#### 4.) Install Telnet in the Windows 10 VM.
Telnet is a feature of Windows and is already installed. It can be turned on by activating it through the Control Panel.
  - Open Control Panel and navigate to "Programs"
![CTF_T1_Step4-1](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/b14dde42-b5b0-4c7b-a62f-5713c1fbec22)
  - Click "Turn Windows features on or off"
![CTF_T1_Step4-2](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/f6c6e04a-f7ab-452d-855d-42fc1eb08a3a)
  - Scroll down and select "Telnet Client" and click "OK" to apply
![CTF_T1_Step4-3](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/ec99f5ae-41c6-4873-a038-4f688a8c6556)
</br>
</br>
 
#### 5.) Try to establish the connection again and log in once connected.
Now that Telnet has been turned on, the following is typed into PowerShell to establish connection to the Ubuntu Server via Telnet: "telnet 192.168.1.5 110" 
</br>
</br>
In POP3, to login start with "User johnd" first and then "Pass toor" 
![CTF_T1_Step5](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/1aa9b03e-8d6f-41a3-9f54-f4250e8c8bf4)
</br>
</br>

#### 6.) List the existing emails and investigate them to search for interesting information.
The existing emails are listed using the "list" command. (I checked each of the emails listed using "retr [#]" but I only included a screenshot of the email containing the answer below)
![CTF_T1_Step6](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/1034f985-eaea-4f62-8160-bcc674e7492f)
</br>
</br>

#### 7.) Enter the provided URL and log into the system.
The URL led to the Splunk Enterprise login page where the given credentials were used to log in.
</br>
</br>
</br>

### Task 2: Search for suspicious activity
#### "In this task, you will search for recorded suspicious activity in the organization."
</br>

#### 1.) In the platform, search for records of the download attempt and investigate them to identify the potential sources.
- Click "Search & Reporting" </br>
![CTF_T2_Step1-1](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/2a031780-1361-4d4a-a300-57ee5e2c4bca)
- There wasn't much to go off of at this point, so it was time to start digging around. Selected "Alerts" to find clues
![CTF_T2_Step1-2](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/cb023a62-878b-4537-8edf-3dfc5894c85c)
- Found a list of alerts pertaining to the honeypot. Selected the one that had to do with file download attempts on the honeypot and opened it in the search feature
![CTF_T2_Step1-3](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/a32afb2d-4141-4e71-988d-f79a76dfa08f)
- Made sure the timeframe was set to "All Time" so there wouldn't be any missed events. Below are the results
![CTF_T2_Step1-4](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/13eb94f0-93fe-4830-a509-e331568934d8)
</br>
</br>

#### 2.) Access the located sources to search for interesting information in them.
- Investigated further by checking all of the URLs from each event
![CTF_T2_Step2-1](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/9d79bc48-3b08-4b7b-bfea-010a3d5a7980)
- Several of the URLs did not lead to the answer; such as the example below:
![CTF_T2_Step2-2](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/ded19c53-4fb6-4e51-9905-e5dec64b04bb)
- Excluded these URLs from the search to filter out the "incorrect" events
![CTF_T2_Step2-3](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/dea3abc0-9d4b-4ee0-a318-164b0691a8e8)
- Eventually came to a URL with a Base64 encode
![CTF_T2_Step2-4](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/50bdb189-74eb-47ee-820e-45416a1db1b5)
</br>

#### 3.) Decipher the messages located in the URLs and identify the flag.
- Copied this code into a Base64 decoder. The first one was not the answer, so the investigation continued
![CTF_T2_Step3-1](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/6401df31-dd8d-481c-a01e-b4a686ed41cc)
- Came across another one with Base64 notation, so I copied that and pasted it into the decoder
![CTF_T2_Step3-2](https://github.com/MitchV123/Capture-The-Flag1/assets/163186778/7300b0bc-f1f0-422b-a9db-fd20ba5dbe4c)

### Flag: "Congrats, you have finished CIT_FINAL successfully"
 
