# Windows Registry<br>

The registry is a collection of **databases that contain the system's configuration data**.<br>
- Hardware
- Software
- User Information
- Used Files
- Programs Used
- Data for devices connected to the system <br>

**Key** (folder)<br>
**Value** (data stored in these registry keys)<br>
**Hives** (the "group" of keys, sub keys, and values stored in a single file on disk)<br>

#

|Name|Description|
|-------------|-----------------------|
|HKEY_CURRENT_USER (HKCU)|Contains the root of configuration information for the currently logged on user.<br>The user's folder, screen color, and control panel settings are stored, and this information is associated with the user's profile.|
|HKEY_HKEY_USERS (HKC)|Include profiles of all active logged users on the computer.<br>HKEY_CURRENT_USER is the subkey of HKEY_USERS|
|HKEY_LOCAL_MACHINE (HKLM)|Contains configuration information specific to your computer.|
|HKEY_CLASSES_ROOT (HKCR)|Make sure that the correct program opens when you open a file using Windows Explorer<br>Sub key in HKEY_LOCAL_MACHINE\Software<br>From Windows 2000, save under HKEY_LOCAL_MACHINE & HKEY_CURRENT_USERS key|
|HEKY_CURRENT_CONFIG|Contains information about the hardware profile used by the local computer at system startup.|

#

# How to access Registry Hive offline<br>
If you can only access the disk image, you need to know where the registry hive is located on the disk.<br>

`C:\Windows\System32\Config`<br>

|Name|Location|
|------|-----------|
|DEFAULT|HKEY_USERS\DEFAULT|
|SAM|HKEY_LOCAL_MACHINE\SAM|
|Security|HKEY_LOCAL_MACHINE\Security|
|Software|HKEY_LOCAL_MACHINE\Software|
|System|HKEY_LOCAL_MACHINE\System|

#

# Hives with user information<br>
For Windows 7 and later: `C:\Users\<username>\` (NTUSER.DAT, USRCLASS.DAT is a **hidden file.**)<br>

|Name|Location|
|------|-----------|
|NTUSER.DAT|HKEY_CURRENT_USER `C:\Users\<username>\`|
|USRCLASS.DAT|HKEY_CURRENT_USER\Software\CLASSES `C:\Users\AppData\Microsoft\Windows`|

#

# Transaction Logs and Backups<br>

- **Transaction Logs**<br>
It is considered a change log journal for Registry Hive, and Windows is often used to write data to Registry Hives.<br>
This means that **Transaction Logs can have the latest changes to the registry that have not reached the registry hives itself.**<br>
The name is the same as the registry hive, but the extension save as a `.LOG` file.<br>
ex) Transaction Logs for SAM Hives are stored in `C:\Windows\System32\Config`<br><br>
- **Backup**<br>
Opposite to Transactions Logs.<br>A backup of a registry hives, **copied to a directory every 10 days.**<br>
ex) Backup location for SAM Hives is located in `C:\Windows\System32\Config\RegBack`

#

