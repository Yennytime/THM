# Dig a little more...<br>
## 1. There are many suspicious open ports; which one is it? (ANSWER format: protocol:port)<br>


The following plugin should be used to locate open ports that are suspicious:<br>
```
.\volatility_2.6_win64_standalone.exe -f victim.raw --profile Win7SP1x64 netscan
```
***We cannot use `sockets` and `connscan` plugins because the victim's OS is Windows 7.***

<img width="1154" alt="image" src="https://user-images.githubusercontent.com/117110034/199653452-8154390a-3da1-4724-9c5c-dee2eaad6b32.png">
<br>

UDP port 5005 uses the `Datagram Protocol`, a communications protocol for the Internet network layer, transport layer, and session layer.<br>
This protocol when used over PORT 5005 makes possible the transmission of a datagram message **from one computer to an application running in another computer.**
<br>
###### Answer : UDP:5005
#

## 2. Vads tag and execute protection are strong indicators of malicious processes; can you find which they are? (ANSWER format: Pid1;Pid2;Pid3)<br>

Let's use the `malfind` plugin to find the malicious processes.<br>malfind is the plugin that can be used to find out the **hidden and injected code**.<br>
```
.\volatility_2.6_win64_standalone.exe -f victim.raw --profile Win7SP1x64 malfind
```
<br>

`PID 1860`<br>
<img width="756" alt="image" src="https://user-images.githubusercontent.com/117110034/199657686-e9eeed39-5a5c-484f-92d9-5841a70d73b8.png">
<br>

`PID 1820`<br>
<img width="756" alt="image" src="https://user-images.githubusercontent.com/117110034/199657886-e10b1853-6bf7-435c-a8dc-ad21c7c1747f.png">
<br>

`PID 2464`<br>
<img width="756" alt="image" src="https://user-images.githubusercontent.com/117110034/199658002-731406a2-756f-43e8-9bd9-5f3a1edfa17c.png">
<br>

PIDs of three malicious processes were found.<br>
###### Answer : 1860;1820;2464


