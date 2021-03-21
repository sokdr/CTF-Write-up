# CTF-Write-up

## Try Hack Me - Lian_Yu

##### URL: https://tryhackme.com/room/lianyu

##### Created by _https://tryhackme.com/p/Deamon_

![logo](https://user-images.githubusercontent.com/20625004/111899596-51ca1f80-8a36-11eb-94ff-fd726fab3227.jpeg)

##### You should deploy the machine first.

##### Run nmap against the target machine.

```nmap -sC -A <target IP>```

Port 80 web access. 

![port80](https://user-images.githubusercontent.com/20625004/111899688-d452df00-8a36-11eb-86f7-69bcf2762d3b.PNG)

##### Then we use ```gobuster``` to seach for paths in the web application.

```gobuster dir <target IP> -w /path/to/wordlist```



##### ```===============================================================```
##### ```/.htaccess            (Status: 403) [Size: 199]```
##### ```/.htpasswd            (Status: 403) [Size: 199]```
##### ```/island               (Status: 301) [Size: 235]```
##### ```/server-status        (Status: 403) [Size: 199]```                             

##### Accessing the web app with the new path 

![code](https://user-images.githubusercontent.com/20625004/111899829-87233d00-8a37-11eb-8543-f85bcc1904ad.PNG)

##### Seems we have a code.

##### Again use ```gobuster``` with the new path.

##### After a lot enumeration we found a new path 

##### ```===============================================================```
##### ```/2100                 (Status: 301) [Size: 240] ```

![2100](https://user-images.githubusercontent.com/20625004/111900051-f188ad00-8a38-11eb-8ffa-74264719ad46.PNG)

#### View source of the page provide us with an extension.

![source_2100](https://user-images.githubusercontent.com/20625004/111900103-2d237700-8a39-11eb-8358-a3de1ea9db8b.PNG)

##### Again fire ```gobuster``` to search for the file extension

##### ```gobuster dir -u "<Target IP>/island/2100/" -w /path/to/wordlsit -x ticket``

##### ok we found it ```/green_arrow.ticket   (Status: 200) [Size: 71]```

##### Access the new path on the browser.

![file_](https://user-images.githubusercontent.com/20625004/111900357-d880fb80-8a3a-11eb-9c89-3f8722a96730.PNG)

##### We found a token and we should decrypt it. It is a Base58 and decode it provide us with a pass. And we have the FTP password.

#####   By using as username the code we found earlier "third pic" and the decoded pass we can access the FTP service.

##### ```220 (vsFTPd 3.0.2)```
##### ```Name (10.10.70.136): <code_word>```
##### ```331 Please specify the password.```
##### ```Password:```
##### ```230 Login successful.```
##### ```Remote system type is UNIX.```
##### ```Using binary mode to transfer files.```
##### ```ftp> ls```
##### ```200 PORT command successful. Consider using PASV.```
##### ```150 Here comes the directory listing.```
##### ```-rw-r--r--    1 0        0          511720 May 01  2020 Leave_me_alone.png```
##### ```-rw-r--r--    1 0        0          549924 May 05  2020 Queen's_Gambit.png```
##### ```-rw-r--r--    1 0        0          191026 May 01  2020 aa.jpg```
##### ```226 Directory send OK.```
##### ```ftp> ```

