##  Investigating Windows<br>

### 1. Whats the version and year of the windows machine?<br>

To check the system version and year, you can find it by entering the **system information** in the search box.<br><br>
<img width="687" alt="image" src="https://user-images.githubusercontent.com/117110034/199895121-1e04a646-81f8-4227-9807-488315793661.png"> <br><br>
Answer : `Windows Server 2016`<br><br>

### 2. Which user logged in last?<br>

1. Use the `net user` command to check the users.<br><br>
<img width="447" alt="image" src="https://user-images.githubusercontent.com/117110034/199898848-170049f3-c320-4fae-8555-f35255d73d4f.png"><br><br>
2. Let's check the last login time of **admin** and **Jenny**.<br><br>
<img width="589" alt="image" src="https://user-images.githubusercontent.com/117110034/199899404-ae2e54f2-58de-43cc-9b9d-734e4acf427f.png"><br><br>
User : `Administrator`, Last login : `11/04/2022 05:08:24 AM`<br><br>
<img width="589" alt="image" src="https://user-images.githubusercontent.com/117110034/199899887-deef068e-5e86-4cae-9601-c010261b7664.png"><br><br>
User : `Jenny`, Last login : `Never`<br>

Answer : `Administrator`<br><br>

### 3. When did John log onto the system last?<br>

Use the `net user John` to check the log onto the system.<br><br>
<img width="589" alt="image" src="https://user-images.githubusercontent.com/117110034/199902276-99e12e52-534e-417b-b62a-11a5e2880285.png"><br><br>

Answer : `03/02/2019 5:48:32 AM`<br><br>

### 4. What IP does the system connect to when it first starts?<br>

1. Go to `regedit` to check the IP that the system connects to when it first starts.<br>
(You can check in the registry about information when the system is started.)<br><br>
<img width="337" alt="image" src="https://user-images.githubusercontent.com/117110034/199904369-98a5b9ea-1261-40fb-a363-134d4a08e36c.png"><br><br>
2. `HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > Current Version > Run` <br><br>
<img width="730" alt="image" src="https://user-images.githubusercontent.com/117110034/199905791-59faba80-489d-4467-84a4-82ac0fd3d439.png"><br><br>

##### HKEY_LOCAL_MACHINE<br>
###### All system-wide settings are stored here, primarily using the HKLM\Software key to verify computer-wide settings. Simply put, many Windows settings, including installed programs and hardware information, can be done here.<br><br>
Answer : `03/02/2019 5:48:32 AM`<br><br>

### 5. What two accounts had administrative privileges (other than the Administrator user)?<br>

1. Go to `Computer Management > Local Users And Group > Users`<br><br>
<img width="784" alt="image" src="https://user-images.githubusercontent.com/117110034/199908462-c5186997-5863-4bf7-b86a-37ea826dca0e.png"><br><br>
2. Check the **Member of**<br><br>
`Guest`<br><br>
<img width="396" alt="image" src="https://user-images.githubusercontent.com/117110034/199909778-3677207b-3903-4c86-ba32-033b87bca19f.png"><br><br>
`Jenny`<br><br>
<img width="396" alt="image" src="https://user-images.githubusercontent.com/117110034/199909834-5d04373e-3463-413f-8919-588ce779b0eb.png"><br><br>

##### Local Users And Group<br>
###### You can protect and manage user accounts and groups that are designated locally on your computer.<br><br>

Now we know `Guest` and `Jenny` are Administator users.<br><br>

Answer : `Jenny`, `Guest`<br><br>

### 6. Whats the name of the scheduled task that is malicous.<br>

Go to `Computer Management > Task Scheduler`<br><br>
<img width="893" alt="image" src="https://user-images.githubusercontent.com/117110034/199910930-f624be88-8215-4df9-89a9-35ca1ce42ea3.png"><br><br>

##### Task Scheduler<br>
###### It is a built-in app for Windows versions earlier than Windows 10, and is a tool that runs a program set when an event occurs. It refers to the time, the user's login, when the computer enters the power saving mode, etc. You can think of it as a pre-scheduling so that the computer can handle the tasks that the user has to do repeatedly by connecting them to the occurrence of the event.<br><br>

Answer : `Clean file system`<br><br>

### 7. What file was the task trying to run daily?<br>

<img width="568" alt="image" src="https://user-images.githubusercontent.com/117110034/199911318-3614a2ea-8de0-47ef-8e0d-11ad9203e410.png"><br><br>

Answer : `nc.ps1`<br><br>

### 8. What port did this file listen locally for?<br>

<img width="753" alt="image" src="https://user-images.githubusercontent.com/117110034/199911717-ad10bed4-3baf-4481-81d1-f1d495e4bef1.png"><br><br>

Abswer : `1348`<br><br>

### 9. When did Jenny last logon?<br>

Let's use the following command in PS : `net user Jenny`<br><br>
<img width="417" alt="image" src="https://user-images.githubusercontent.com/117110034/199912603-f76bf833-ca9c-46bf-9f51-3bdb83216efd.png"><br><br>

Answer : `Never`<br><br>

### 10. At what date did the compromise take place?<br>

<img width="427" alt="image" src="https://user-images.githubusercontent.com/117110034/199913145-73e32ac4-ecbb-4908-be90-5c524d01998f.png"><br><br>

Answer : `03/02/2019`<br><br>

### 11. At what time did Windows first assign special privileges to a new logon? (Hint : 00/00/0000 0:00:49 PM)<br>

Go to `Event Viewer > Windows Log > check 00/00/0000 0:00:49 PM`<br><br>
<img width="791" alt="image" src="https://user-images.githubusercontent.com/117110034/199916396-33e41d0f-bac6-48e0-bfff-377271beefb6.png"><br><br>

##### Event Viewer<br>
###### It manages events and event logs, supports event recording, lookup, regular verification, log archiving, and metadata management. It is possible to grasp the execution history of the background program and the presence or absence of various services, and leaves various logs that occur in the system.<br><br>
Answer : `03/02/2019 04:04:49 PM`<br><br>

### 12. What tool was used to get Windows passwords?<br>

Go to `Task Scheduler > Task Scheduler Library > Gameover > action`<br><br>
<img width="527" alt="image" src="https://user-images.githubusercontent.com/117110034/199917660-efc24816-32db-4cc8-a62a-c84a0d992407.png"><br>
<img width="945" alt="image" src="https://user-images.githubusercontent.com/117110034/199918613-41b37a16-8e5d-4d4a-ab5a-7214d61c6a47.png"><br><br>
Looking at mim.exe, it is highly likely that it is `MimiKatz`. Let's serach about it.<br><br>
<img width="601" alt="image" src="https://user-images.githubusercontent.com/117110034/199918145-eb7b4a54-0f33-41c5-b8c9-7a93cde0aa05.png"><br><br>

Answer : `Mimikatz`<br><br>

### 13. What was the attackers external control and command servers IP?<br>

In Windows, a `host` file is a file that **stores an IP address** that corresponds to the host name, allowing the server to locate it without receiving address information from the Domain Name System (DNS).<br>
Go to `C: > windows > system32 > drivers > etc > hosts` <br><br>

<img width="611" alt="image" src="https://user-images.githubusercontent.com/117110034/199920425-f062cf3e-eb84-42c0-a9ff-f5105b5c87f4.png"><br><br>
It looks like Google's address is wrong.<br><br>

Answer : `76.32.97.132`<br><br>

### 14. What was the extension name of the shell uploaded via the servers website?<br>

Go to `C: > intetpub > wwwroot`<br><br>
<img width="640" alt="image" src="https://user-images.githubusercontent.com/117110034/199921107-1c5ea386-1ef4-42f2-bcaa-074156548b4b.png"><br><br>

##### intetpub<br>
###### It is a folder containing website content and web apps, and may provide multiple domains.<br>

##### wwwroot<br>
###### It includes all web pages and content to be published on the web, and is the default directory for publishing web pages.<br><br>
Answer : `.jsp`<br><br>

### 15. What was the last port the attacker opened? (Hint : Firewall)<br>

Go to `Windows Firewall with Advance Security > Inbound Rules`<br><br>

<img width="427" alt="image" src="https://user-images.githubusercontent.com/117110034/200103046-4c9deaf1-04f2-41b8-8a20-8b836193c7c6.png"><br><br>

##### Inbound Rules<br>
###### It refers to a rule that allows a client to enter its server data. It is a rule that allows users to access servers, read the data, and create, modify, and delete them depending on their permission. Since the client is authorized to access the server's data, the inbound rule basically presupposes closing all ports. That is, ports that are not set in the inbound rule are ports that cannot be used, and even if the port is used, the connection itself is prevented.<br><br>

Answer : `1337`<br><br>

### 16. Check for DNS poisoning, what site was targeted?<br>

Before checking DNS spoofing, I think we should think about how to DNS spoofing on Windows. Search found that temporarily adding rows to the `hosts` file, if you have a Windows system, is the easiest way to test DNS changes before they actually take effect.<br>
Let's go to `c:\windows\System32\drivers\etc\hosts`<br><br>

<img width="611" alt="image" src="https://user-images.githubusercontent.com/117110034/199920425-f062cf3e-eb84-42c0-a9ff-f5105b5c87f4.png"><br><br>

Answer : `google.com`<br><br>







