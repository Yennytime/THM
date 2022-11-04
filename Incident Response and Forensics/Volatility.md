# Volatility<br>

`volatility` is a free **"memory forensics tool"** developed and maintained by Volatility labs. - is an invaluable tool for any Blue Teamer.<br>

#

1. **Live machines** (turned on) can have their memory captured with one of the following tools:<br>

* FTK Imager
* Redline
* DumpIt.exe
* win32dd.exe / win64dd.exe
<br>

These tools will typically output a `.raw` file which contains an image of the system memory.<br>The `.raw` format is one of the most common **memory file types** and the original data that turned the evidence into an **image**.<br><br>


2. **Offline machines** can have their memory pulled relatively easily as long as their drives aren't encrypted. For example - Window system :
```
%SystemDrive%/hiberfil.sys
```
__Hiberfil.sys__, better known as the Windows hibernation file, contains a memory image compressed from a previous boot and is available for some memory forensics.<br><br>

3. **Virtual machines** - The following is a memory capture processes/files that contain memory images for various virtual machine hypervisors.<br>

* VMware - .vmem file
* Hyper-V - .bin file
* Parallels - .mem file
* VirtualBox - .sav file > This is only a partial memory file (memory dump needed) <br>

These files are often found simply in the **data store** on that hypervisor and can be copied simply without shutting down the associated virtual machines, thereby maintaining **integrity**. <br>

#

1) What memory format is the most common? <br>`.raw`<br>
2) The Window's system we're looking to perform memory forensics on was turned off by mistake. What file contains a compressed memory image?<br>`hiberfil.sys`<br>
3) How about if we wanted to perform memory forensics on a VMware-based virtual machine?<br>`.vmem`<br>

#

###  Examining Our Patient

1.  Let's see our options now with the command `volatility -f MEMORY_FILE.raw imageinfo`

<img width="852" alt="image" src="https://user-images.githubusercontent.com/117110034/199876611-ea30140d-4fe6-4cbc-9dc6-2a46e7144727.png">


2. What profile is correct for this memory image?<br>`WinXPSP2x86`<br>
<img width="767" alt="image" src="https://user-images.githubusercontent.com/117110034/199876882-559ad36b-52b3-4227-9b93-d0ed5a923f5a.png">

3. What is the process ID for the smss.exe process?<br>`368`<br>
<img width="509" alt="image" src="https://user-images.githubusercontent.com/117110034/199877070-bef4622e-c5fe-4098-9eb0-0c51031688d9.png">

4. What process has only one 'False' listed?<br>`csrss.exe`<br>
<img width="773" alt="image" src="https://user-images.githubusercontent.com/117110034/199883770-3a4c4e3a-d2c9-4e32-b393-1064666a9d62.png">
<img width="842" alt="image" src="https://user-images.githubusercontent.com/117110034/199877483-8b4eddbd-054a-4bbf-80be-507c2371834c.png">

###### It's fairly common for malware to attempt to hide itself and the process associated with it. `psxview` plugin is can view intentionally hidden processes.
5. Which process has all three columns listed as 'False' (other than System)?<br>`csrss.exe`<br>
<img width="790" alt="image" src="https://user-images.githubusercontent.com/117110034/199883479-729a6515-5d5e-4bca-af1e-906d609c15ad.png">
<img width="842" alt="image" src="https://user-images.githubusercontent.com/117110034/199878349-2a2c8e95-dac3-4602-9aab-2a07f210e478.png">

###### `ldrmodules` plugin is a greater focus then psxview. Three columns will appear here in the middle, InLoad, InInit, InMem. If any of these are false, that module has likely been injected which is a really bad thing.

6. `apihooks` plugin is can check unexpected patches in the standard system DLLs. If we see an instance where `Hooking module: <unknown>` that's really bad.
<img width="786" alt="image" src="https://user-images.githubusercontent.com/117110034/199883391-c3ad79e5-6fb5-4902-8b3d-e18cb1e27905.png">
<img width="685" alt="image" src="https://user-images.githubusercontent.com/117110034/199882384-67930ff1-d206-4f8e-b161-64865dbfc890.png">
<img width="685" alt="image" src="https://user-images.githubusercontent.com/117110034/199882298-00a81149-b40d-4ab5-bd7d-4ff346d65650.png">

###### I couldn't capture everything because there were many results. Anyway, if you check the function of the dll files of `explorer.exe` and `reader_sl.exe`, you can see that it is malicious code.
7. How many files does this generate?<br>`12`<br>
<img width="814" alt="image" src="https://user-images.githubusercontent.com/117110034/199882836-bda05cbb-103a-4ba7-961c-aeb6c4d2d76c.png">
<img width="251" alt="image" src="https://user-images.githubusercontent.com/117110034/199882896-f484d1b1-849a-49c9-8ccb-d022d1307f3b.png">

###### `malfind` plugin can check the injection code

8. DLLs are **shared system libraries utilized in system processes**. These are commonly subjected to hijacking and other side-loading attacks, making them a key target for forensics. `dlllist` plugin can check the list all of the DLLs in memory.  
<img width="857" alt="image" src="https://user-images.githubusercontent.com/117110034/199885895-cb638d4a-2b00-48f8-ab47-d9f260d0701a.png">
<br>

`PID 1640`<br><br>
<img width="1312" alt="image" src="https://user-images.githubusercontent.com/117110034/199886119-afefb3b1-3cca-404e-b757-039bdac25e24.png">

###### If you specify a PID, you can check the DLLs list of the specified PID.

9. How many DLLs does this end up pulling?<br>`12`<br>
<img width="1020" alt="image" src="https://user-images.githubusercontent.com/117110034/199886976-8c852ad3-7da3-4da0-9d64-c1055d5ba24f.png">

#

### Post Actions<br>

What malware has our sample been infected with? You can find this in the results of VirusTotal and Hybrid Anaylsis?<br>`Cridex`<br><br>
<img width="459" alt="image" src="https://user-images.githubusercontent.com/117110034/199888541-0669d6e4-9adc-4b4d-b297-d4f61dfdcdfe.png">

