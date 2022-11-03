# Volatility Forensics<br>
## 1. What is the Operating System of this Dump file? (OS name)<br>

When you unpack the `victim.zip`, the raw file comes out. Let's start the analysis using `volatility 2.6`.<br> First, we need information on the operating system. To do so, let's use the following plugin.<br><br> 
***Don't forget to move that raw file to volatility2.6 directory!***
```
.\volatility_2.6_win64_standalone.exe -f victim.raw imageinfo
```
<img width="1153" alt="image" src="https://user-images.githubusercontent.com/117110034/199409309-fcfbfdd4-147c-45a0-b932-506cffd71f10.png">
<br>
It seems that the victim was using Windows OS. (windows7)<br> 

###### Answer : Windows 
#

## 2. What is the PID of SearchIndexer? <br>

Use the following plugin to find the `PID`. I usually use `pstree` a lot.<br>pstree is **quickly identify** the parent and child processes of a specific process.<br><br>
***Don't forget `--profile` plug-in! The suggested profile(s) for this raw file was `Win7SP1x64`.***
```
.\volatility_2.6_win64_standalone.exe -f victim.raw --profile Win7SP1x64 pstree
```
<img width="1153" alt="image" src="https://user-images.githubusercontent.com/117110034/199412655-11641e61-8cfa-4970-a5a5-e4b3afb109e4.png">
<br>

We found that the PID of SearchIndexer was `2180` and the PPID was 504 and the **parent process** of SearchIndexer is `services.exe`.<br>

###### Answer : 2180
#
## 3. What is the last directory accessed by the user? (The last folder name as it is?)<br>

You must use the `Shellbags` plugin to gather information about directories.<br> Shellbags collect **all information about directory, such as size, location, and icon**.<br>
```
.\volatility_2.6_win64_standalone.exe -f victim.raw --profile Win7SP1x64 shellbags
```
<img width="1154" alt="image" src="https://user-images.githubusercontent.com/117110034/199420324-f5585f26-2b3c-4281-ae83-2faeab5a064d.png">
<br>

If you check the directory access list, you can see that the last directory accessed is `Z:\logs\deleted_files`. <br>

###### Answer : deleted_files




