
# Cybersecurity Adversary Emulation & Detection Lab

# System Information

- CPU: Intel(R) Core(TM) i5-8350U CPU @ 1.70GHz (1.90 GHz)
- RAM: 16GB
- Storage: 256 GB SSD
- Motherboard: HP ZBook 14u G5
- Host Operating System: Microsoft Windows 11 Pro

# Network Diagram

<img width="660" height="371" alt="Network_diag" src="https://github.com/user-attachments/assets/eed4b65d-c3ad-4971-ad58-066f77c6cf0c" />

# VM Configuration

| VM | CPU (Core) | RAM (GB) | Network Type |
|---|---:|---:|---|
| Kali | 2 | 4 | NAT |
| Windows Server 2019 | 2 | 4 | NAT |

**Kali Machine**  


**Windows Machine**  

  
# Splunk Installation

**Downloading Splunk Version : splunk-10.2.2**

<img width="641" height="338" alt="LAB SS1" src="https://github.com/user-attachments/assets/eb9e1bbf-2848-4f9c-9935-7874e905e827" />


**Installing Splunk**

<img width="647" height="237" alt="LAB SS2" src="https://github.com/user-attachments/assets/94e15d96-8f2d-4c45-b602-dff8224d7aa5" />



**Starting Splunk**
<img width="634" height="479" alt="image" src="https://github.com/user-attachments/assets/263df457-6d5a-44eb-998a-f3c8e10dc23d" />
<img width="1708" height="741" alt="LAB SS SPLUNK MISSING" src="https://github.com/user-attachments/assets/34d24dce-836f-4c50-bb01-497276cd446d" />
<img width="1275" height="757" alt="LAB SS3" src="https://github.com/user-attachments/assets/67dd386e-2816-412a-9247-031f029434fd" />



-------------------------------------------------------------
**Download Universal Forwarder** [Link](https://www.splunk.com/en_us/download/universal-forwarder.html)

<img width="1330" height="606" alt="splunk_universal_down" src="https://github.com/user-attachments/assets/9755e42b-f555-4263-a994-8a28e0c8990d" />

**Installing Universal Forwarder**
<img width="501" height="390" alt="LAB SS4" src="https://github.com/user-attachments/assets/a4709e3c-df39-4aab-843c-9dc19d3c6b84" />
<img width="497" height="391" alt="LAB SS5" src="https://github.com/user-attachments/assets/df003aeb-1bba-4917-8af5-fe65c43daa30" />


Set Receiver Port on Kali Machine : **9997** 
<img width="1699" height="855" alt="LAB SS9" src="https://github.com/user-attachments/assets/98ab2fef-e504-46ab-8ae6-dabbd0caddf7" />


Get ip address of kali machine : **192.168.65.129**  
<img width="646" height="512" alt="LAB SS7" src="https://github.com/user-attachments/assets/bcca30da-6fb8-4064-b6dc-37c4d09078aa" />


Now set **Host: 192.168.65.129** and **Port: 8089** as **Deployment Server**  in Windows Machine  
<img width="496" height="389" alt="LAB SS6" src="https://github.com/user-attachments/assets/3d301281-5e3c-4c70-acae-7f078d6942f5" />
<img width="495" height="388" alt="LAB SS8" src="https://github.com/user-attachments/assets/6aea367c-4087-4e62-9a22-9c27c88e6ac4" />

Check if the forwarder is active   

<img width="981" height="512" alt="LAB SS10" src="https://github.com/user-attachments/assets/7d73f471-8ecd-4d58-83a6-ab1f2b87343a" />

Now, we will setup sysmon. First we will download and extract sysmon files to C:\Tools\Sysmon  
<img width="1155" height="597" alt="LAB SS11" src="https://github.com/user-attachments/assets/b1313ea9-40e9-4233-8ef0-7b55000465f5" />
 

Save the configuraion file to the same directory
<img width="1699" height="920" alt="LAB SS12" src="https://github.com/user-attachments/assets/e9bf9526-4886-47bc-8e6a-c05e50ac93df" />
 

Installing Sysmon  
<img width="1701" height="354" alt="LAB SS13" src="https://github.com/user-attachments/assets/8414d633-5458-4c4c-93ce-c788d200328f" />
  

Check if sysmon is running and logging  
<img width="1700" height="585" alt="LAb SS14" src="https://github.com/user-attachments/assets/ad68a7e7-d7ae-49a3-a1d5-6571b1336465" />
  

Now, Create a new index **win** from kali machine  
<img width="577" height="440" alt="LAB SS 17 " src="https://github.com/user-attachments/assets/af57652c-585f-46b9-a6ab-1dbae0d06411" />


Now create a local app for Sysmon input at : `**C:\Program Files\SplunkUniversalForwarder\etc\apps\TA-local-sysmon\local\inputs.conf**`  
<img width="1330" height="717" alt="LAB SS15" src="https://github.com/user-attachments/assets/2901d1eb-f3d3-44e7-a146-b4b86a55482d" />
 

Now restart the forwarder:  
<img width="1682" height="375" alt="LAB SS16" src="https://github.com/user-attachments/assets/3aae0a29-f056-4f62-8ea9-2220757b72bb" />


Checking in kali machine for logs on newly created index = win  

<img width="955" height="216" alt="index_win" src="https://github.com/user-attachments/assets/452efcf7-732f-4724-a93a-2e69ba024b88" />  

<img width="955" height="978" alt="splunk_home_data" src="https://github.com/user-attachments/assets/7dc6d6aa-3322-41be-ad94-11da21eeaffc" />  

Enable useful Windows logging with powershell:  

```
wevtutil sl "Microsoft-Windows-PowerShell/Operational" /e:true
wevtutil sl "Microsoft-Windows-TaskScheduler/Operational" /e:true
wevtutil sl "Microsoft-Windows-Windows Defender/Operational" /e:true
```


Install Splunk Add-on for Sysmon which will help us to check the logs properly.   
<img width="934" height="479" alt="Sysmon_addon" src="https://github.com/user-attachments/assets/4be5e802-e557-4a5d-ab1d-ebfc500ad8d1" />  


# Install Atomic RED Team  

```
[Net.ServicePointManager]::SecurityProtocol =[Net.SecurityProtocolType]::Tls12
Set-ExecutionPolicy Bypass -Scope Process -Force

Install-Module -Name invoke-atomicredteam,powershell-yaml -Scope CurrentUser -Force

IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing)
Install-AtomicRedTeam -getAtomics
Import-Module Invoke-AtomicRedTeam 
```

Sometime it will make error for directory, To solve this we need to set the environment path to fix the issue.  
 <img width="860" height="506" alt="LAB SS22" src="https://github.com/user-attachments/assets/414713c8-b64f-4e63-9b6c-096a05fddfb1" />


```
Set-ExecutionPolicy Bypass -Scope Process -Force

Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1" -Force
$PSDefaultParameterValues = @{
  "Invoke-AtomicTest:PathToAtomicsFolder" = "C:\AtomicRedTeam\atomics"
}

Get-Command Invoke-AtomicTest
````

<img width="1298" height="606" alt="LAB SS23" src="https://github.com/user-attachments/assets/328b2606-cb58-487c-8378-19874bee59ba" />

 

# T1053.005 (Persistence) | Scheduled Task: Create a task that runs a hidden script (every minute.)  

Check of for modules of **T1053.005**  
<img width="941" height="262" alt="LAB SS24" src="https://github.com/user-attachments/assets/84aedc5e-09b8-445a-8d29-c02d20757f74" />
 
 The built-in test 8 -  T1053.005-8 Import XML Schedule Task with Hidden Attribute does **hidden** has similarity to the task.  
 Execute and check if its ok  
<img width="1338" height="597" alt="LAB SS25" src="https://github.com/user-attachments/assets/984ec667-c059-469d-ab76-59e09800879e" />
  

# T1218.005 (Defense Evasion) | MSHTA: Execute a malicious remote .hta file to bypass app control.  

Check of modules of T1218.005  
<img width="1673" height="365" alt="LAB SS26" src="https://github.com/user-attachments/assets/05cd573d-9a4f-42fd-8747-383d3fa28c63" />

As 3 is matches our requirements, we will use **T1218.005-3**  
<img width="1703" height="489" alt="LAB SS27" src="https://github.com/user-attachments/assets/a26f3008-2ae6-4bf8-bffd-04bc8fe613f6" />
 

# T1003.001 (Credential Access) | LSASS Dumping: Use procdump to steal credentials from memory.  

Check the module of **T1003.001**  
<img width="975" height="260" alt="T1003 001" src="https://github.com/user-attachments/assets/f0d51ed5-ba0a-47dd-81ee-bf34ddfba5ea" />  
As 1 matches our requirement, we will use **T1003.001-1**  
For first run, windows defender blocked the process. So we had to disable the defender real-time protection then it worked and file has been written on **C:\Windows\Temp\lsass_dump.dmp**  
<img width="796" height="587" alt="T1003 001-1-done" src="https://github.com/user-attachments/assets/345e233e-7913-4036-936a-4aefa8d573fc" />  

# T1059.001 (Execution) | PowerShell Download:  Download and execute a script from the web.  

Check the module of **T1059.001**  
<img width="958" height="428" alt="T1059 001" src="https://github.com/user-attachments/assets/dcb72c26-c22c-4829-b4b1-f7db14a90d46" />  
As option 6 and 8 both are good choice but 6 is purely on powershell. So we are using option 6.  
<img width="741" height="162" alt="T1059 001-done" src="https://github.com/user-attachments/assets/1e7979e3-b065-47e2-8eac-bcdae6bcc6b9" />  

# T1112 (Defense Evasion) | Registry Modification: Disable Windows Defender via  

Check the modules of T1112   
<img width="811" height="908" alt="T1112" src="https://github.com/user-attachments/assets/3d1f171b-870c-4d1e-91ce-680938b63e28" />  
For this task, we will use three sperate module. **T1112-38 (Suppress Win Defender Notifications),  T1112-51 (Disable Win Defender Notification) and T1112-56 (Tamper Win Defender Protection)**  
<img width="829" height="423" alt="T1112-done" src="https://github.com/user-attachments/assets/0d9513e8-5cf5-4377-a73b-c31ec7b89519" />  
**T1112-38 and T1112-51 completed successfully but T1112-56 was blocked by windows security but no notification has been popped because of other two options.**  

# LOG Analysis

As we have installed **Splunk Add-on for Sysmon**, we need to do some changes to work with that addon.  
App -> Manage App -> **Splunk Add-on for Sysmon**  -> Edit -> Visible (Yes)  
<img width="1351" height="656" alt="sysmon_addon1" src="https://github.com/user-attachments/assets/9480f9b3-e3d7-4012-947d-755f51be37f9" />  
<img width="852" height="553" alt="sysmon_addon-2" src="https://github.com/user-attachments/assets/04a8a538-a5b2-41ec-882f-3e6ca02e7051" />  
Now a new menu will show in apps section  
<img width="942" height="585" alt="sysmon_addon3" src="https://github.com/user-attachments/assets/db0d45f4-592e-443d-a47e-5b14848edd61" />  

# The Detection (Blue Team)

**1. T1053.005 (Persistence) | Scheduled Task** : Sysmon Event ID 1 is most helpful because it can show `powershell.exe` being launched with scheduled-task registration behavior such as `Register-ScheduledTask`, `New-ScheduledTask`, or XML-based task import. This provides the required process name, command line, and time of execution.  

```
index="win" ("Sysmon" OR "Microsoft-Windows-Sysmon") (EventCode=1 OR EventID=1)
(Image="*\\powershell.exe" OR Image="*\\pwsh.exe")
(
    CommandLine="*Register-ScheduledTask*"
    OR CommandLine="*New-ScheduledTask*"
    OR CommandLine="*Set-ScheduledTask*"
    OR CommandLine="*-Xml*"
    OR CommandLine="*ScheduledTask*"
    OR CommandLine="*TaskScheduler*"
)
| eval Time=strftime(_time,"%Y-%m-%d %H:%M:%S")
| eval Process_Name=mvindex(split(Image,"\\"),-1)
| eval Command_Line=CommandLine
| table Time host User EventCode EventID Process_Name Image Command_Line ParentImage ParentCommandLine ProcessId ParentProcessId
```

**Proof:**  
<img width="1919" height="757" alt="blue_T1053 005" src="https://github.com/user-attachments/assets/3a64b07c-5931-4ef4-9c4a-c5254b82382e" />  


**2. T1218.005 (Defense Evasion) | MSHTA:** Sysmon Event ID 1 is most helpful because it shows `mshta.exe` being launched and captures the full command line, including the `.hta` payload.  

```
index=win ("Sysmon" OR "Microsoft-Windows-Sysmon") (EventCode=1 OR EventID=1)
(Image="*\\mshta.exe" OR OriginalFileName="MSHTA.EXE")
(
    CommandLine="*http://*"
    OR CommandLine="*https://*"
    OR CommandLine="*.hta*"
    OR CommandLine="*vbscript:*"
    OR CommandLine="*javascript:*"
)
| eval Time=strftime(_time,"%Y-%m-%d %H:%M:%S")
| eval Process_Name=mvindex(split(Image,"\\"),-1)
| eval Command_Line=CommandLine
| table Time host User EventCode EventID Process_Name Image Command_Line ParentImage ParentCommandLine ProcessId ParentProcessId
```
**Proof:**  
<img width="1755" height="755" alt="blue_T1218 005" src="https://github.com/user-attachments/assets/ded8c642-51f8-4d9b-9831-2007c62a54f3" />  

**3. T1003.001 (Credential Access) | LSASS Dumping:** Sysmon Event ID 10 is most helpful because it shows a process accessing lsass.exe. That is the key behavior for LSASS credential dumping. The join with Sysmon Event ID 1 adds the original process command line, which proves the process name, command line, and time.  


```
index=win ("Sysmon" OR "Microsoft-Windows-Sysmon") (EventCode=10 OR EventID=10)
TargetImage="*\\lsass.exe"
(
    SourceImage="*\\procdump.exe"
    OR SourceImage="*\\procdump64.exe"
    OR GrantedAccess="0x1fffff"
    OR GrantedAccess="0x1010"
    OR GrantedAccess="0x1410"
    OR GrantedAccess="0x143a"
)
| eval Access_Time=strftime(_time,"%Y-%m-%d %H:%M:%S")
| eval ProcessGuid=coalesce(SourceProcessGuid, SourceProcessGUID, source_process_guid)
| eval Event10_Process_Path=coalesce(SourceImage, source_image)
| eval Event10_Process_Name=mvindex(split(Event10_Process_Path,"\\"),-1)
| join type=left ProcessGuid [
    search index=win ("Sysmon" OR "Microsoft-Windows-Sysmon") (EventCode=1 OR EventID=1)
    | eval ProcessGuid=coalesce(ProcessGuid, process_guid)
    | eval Created_Time=strftime(_time,"%Y-%m-%d %H:%M:%S")
    | eval Created_Process_Name=mvindex(split(Image,"\\"),-1)
    | rename Image as Created_Image
    | rename CommandLine as Created_CommandLine
    | table ProcessGuid Created_Time Created_Process_Name Created_Image Created_CommandLine ParentImage ParentCommandLine ProcessId ParentProcessId
]
| eval Time=coalesce(Created_Time, Access_Time)
| eval Process_Name=coalesce(Created_Process_Name, Event10_Process_Name)
| eval Image=coalesce(Created_Image, Event10_Process_Path)
| eval Command_Line=coalesce(Created_CommandLine, CommandLine, "Command line not stored in Event ID 10; correlated with Event ID 1 if available")
| table Time host User EventCode EventID Process_Name Image Command_Line SourceImage TargetImage GrantedAccess CallTrace ParentImage ParentCommandLine ProcessId ParentProcessId ProcessGuid
```  
**Proof:**  
<img width="1917" height="770" alt="blue_T1003 001" src="https://github.com/user-attachments/assets/0121447b-590b-46e8-8f11-310a74822216" />  


**4. T1059.001 (Execution) | PowerShell Download:** Sysmon Event ID 1 is most helpful because it records `powershell.exe` execution and captures the command line showing web download behavior and execution behavior.  

```
index=win ("Sysmon" OR "Microsoft-Windows-Sysmon") (EventCode=1 OR EventID=1)
(Image="*\\powershell.exe" OR Image="*\\pwsh.exe")
(
    CommandLine="*http://*"
    OR CommandLine="*https://*"
    OR CommandLine="*Invoke-WebRequest*"
    OR CommandLine="*iwr*"
    OR CommandLine="*wget*"
    OR CommandLine="*curl*"
    OR CommandLine="*DownloadString*"
    OR CommandLine="*DownloadFile*"
    OR CommandLine="*Net.WebClient*"
    OR CommandLine="*System.Net.WebClient*"
)
(
    CommandLine="*iex*"
    OR CommandLine="*Invoke-Expression*"
    OR CommandLine="*-enc*"
    OR CommandLine="*-EncodedCommand*"
    OR CommandLine="*-ExecutionPolicy Bypass*"
    OR CommandLine="*-nop*"
    OR CommandLine="*-NoProfile*"
)
| eval Time=strftime(_time,"%Y-%m-%d %H:%M:%S")
| eval Process_Name=mvindex(split(Image,"\\"),-1)
| eval Command_Line=CommandLine
| table Time host User EventCode EventID Process_Name Image Command_Line ParentImage ParentCommandLine ProcessId ParentProcessId
```
**Proof:**  
<img width="1914" height="817" alt="blue_T1059 001" src="https://github.com/user-attachments/assets/cdc3b493-6198-4b31-87b0-2e436090389f" />  


**5. T1112 (Defense Evasion) | Registry Modification:** Sysmon Event ID 1 was the most helpful in this environment because it captured the process responsible for the Defender modification attempt, such as `reg.exe`. The command line showed Defender-related modification behavior, including values such as `TamperProtection`, `DisableNotifications`, `Set-MpPreference`, or related Defender settings. This provided the required proof of the process name, command line, and time of the attack.  


```
index=win ("Sysmon" OR "Microsoft-Windows-Sysmon") (EventCode=1 OR EventID=1)
(
    Image="*\\reg.exe"
    OR Image="*\\powershell.exe"
    OR Image="*\\pwsh.exe"
)
(
    CommandLine="*Windows Defender*"
    OR CommandLine="*DisableAntiSpyware*"
    OR CommandLine="*TamperProtection*"
    OR CommandLine="*DisableNotifications*" 
    OR CommandLine="*Notification_Suppress*" 
    OR CommandLine="*DisableRealtimeMonitoring*"
    OR CommandLine="*DisableBehaviorMonitoring*"
    OR CommandLine="*DisableOnAccessProtection*"
    OR CommandLine="*Set-MpPreference*"
    OR CommandLine="*Add-MpPreference*"
)
| eval Time=strftime(_time,"%Y-%m-%d %H:%M:%S")
| eval Process_Name=mvindex(split(Image,"\\"),-1)
| eval Command_Line=CommandLine
| table Time host User EventCode EventID Process_Name Image Command_Line ParentImage ParentCommandLine ProcessId ParentProcessId
```  
**Proof:**
<img width="1881" height="819" alt="blue_T1112" src="https://github.com/user-attachments/assets/ecd8782d-4dfa-459f-bb95-542cd46eb3b1" />
