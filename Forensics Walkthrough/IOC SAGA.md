# Let's dig into them and find some Indicator of Compromise (IOC).<br>

## 1. `'www.go****.ru'` (write full url without any quotation marks)<br>

Let's dump the memory of the previously found malicious process `PID 1860, 1820, 2464` to see what kind of malicious activity it did.
```
.\volatility_2.6_win64_standalone.exe -f victim.raw --profile Win7SP1x64 -p 1860,1820,2464 memdump -D . 
```
<img width="698" alt="image" src="https://user-images.githubusercontent.com/117110034/199660299-e05f6b06-658f-43cb-974e-aab2898ca841.png">

Now, let's replace the dump file with a text file extension and open it with Notepad++.<br>
```
Ex) strings 1860.dmp > 1860.txt
```
`PID 1860`
<br><br>
<img width="468" alt="image" src="https://user-images.githubusercontent.com/117110034/199663451-cba4a9fc-091a-44bc-8419-b9903eff0257.png">
<br>

`PID 1820` 
<br><br>
<img width="244" alt="image" src="https://user-images.githubusercontent.com/117110034/199663279-4c29f374-a0ed-40fa-9f51-54d78496396d.png">
<br>

`PID 2464`
<br><br>
<img width="468" alt="image" src="https://user-images.githubusercontent.com/117110034/199663451-cba4a9fc-091a-44bc-8419-b9903eff0257.png">
<br>

There was no information on `www.go****.ru` in the rest of the PID except PID **1820**.
<br>
|URL|Flag|
|:------:|:---:|
|www.google.ru|X|
|www.go4win.ru|X|
|www.gocaps.ru|X|
|www.goporn.ru|O|

###### Answer : www.goporn.ru

#

## 2. `'www.i****.com'` (write full url without any quotation marks)<br>

`PID 1820`
<br><br>
<img width="233" alt="image" src="https://user-images.githubusercontent.com/117110034/199667484-4c4ae194-1466-4491-a9ac-58578f07772b.png">
<br>

There was no information on `www.i****.com` in the rest of the PID except PID **1820**.<br>

###### Answer : www.ikaka.com

#

## 3. `'www.ic******.com'`<br>

`PID 1820`
<br><br>
<img width="349" alt="image" src="https://user-images.githubusercontent.com/117110034/199667977-3ca8442d-f1db-4675-9129-bfcd7ed8f8f0.png">
<br>

There was no information on `www.ic******.com` in the rest of the PID except PID **1820**.<br>

###### Answer : www.icsalabs.com

#

## 4. `202.***.233.***` (Write full IP)<br>


`PID 1820` 
<br><br>
<img width="189" alt="image" src="https://user-images.githubusercontent.com/117110034/199668768-1ab97662-908a-4234-82bf-34ada2bef5f6.png">
<br>

There was no information on `202.***.233.***` in the rest of the PID except PID **1820**.<br>

###### Answer : 202.107.233.211

#

## 5. `***.200.**.164` (Write full IP)<br>

`PID 1820` 
<br><br>
<img width="636" alt="image" src="https://user-images.githubusercontent.com/117110034/199669362-14ec486e-68a1-4df8-af1f-3b5602da094f.png">
<br>

There was no information on `***.200.**.164` in the rest of the PID except PID **1820**.<br>

###### Answer : 209.200.12.164

#

## 6. `209.190.***.***`<br>


`PID 1820` 
<br><br>
<img width="477" alt="image" src="https://user-images.githubusercontent.com/117110034/199669637-1cedd2e4-169d-4f7a-90b6-54ecafb602e8.png">
<br>

There was no information on `***.200.**.164` in the rest of the PID except PID **1820**.<br>

###### Answer : 209.190.122.186

#

## 7. What is the unique environmental variable of PID 2464?<br>

Let's use the ` envars` plugin  to check the environmental variables for PID 2464.
``` 
.\volatility_2.6_win64_standalone.exe -f victim.raw --profile Win7SP1x64 -p 2464 envars
```
<img width="1276" alt="image" src="https://user-images.githubusercontent.com/117110034/199675386-7d173a0d-7ea6-4d9d-aaf3-f93f77578f3b.png">
<br>

I don't know what `OANOCACHE` is even if I search it. If you know it, please let me know in the comments.<br>anyway, we found the unique environmental that "OANOCACHE".

###### Answer : OANOCACHE
