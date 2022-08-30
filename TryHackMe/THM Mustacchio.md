# CTF-Write-up

## Try Hack Me - Mustacchio

##### URL: https://tryhackme.com/room/mustacchio

##### Created by _https://tryhackme.com/p/zyeinn_

![logo](https://user-images.githubusercontent.com/20625004/187385183-721c157c-5b71-4977-b5bc-d39375de5b57.PNG)

You should deploy the machine first.

Add the CTF ip to your host file.

``` echo "CTF ip" >> /etc/hosts```

Run nmap against the target machine.

```nmap -sC -A  <target IP>```

Ports 22 and 80.

Lets view port 80.

![80](https://user-images.githubusercontent.com/20625004/187385417-28e86e50-0cf3-4c4b-9c3a-842e34249e59.PNG)

With the use of ``ffuf`` tool we try to find intersing directories.

``fuf -u http://targgetIP/FUZZ -c -v -w /path/to/wordlist``

![custom](https://user-images.githubusercontent.com/20625004/187386233-5c381a8b-e78c-4770-98e5-28bcee8c3087.PNG)


Accessing the ``custom`` directory reveals another directory ``js`` beneath that, we’ find a ``users.bak`` file and download it.

![custom_js](https://user-images.githubusercontent.com/20625004/187386684-63eace75-a7f7-4ac9-9d33-4b8383209291.PNG)



![bak](https://user-images.githubusercontent.com/20625004/187387521-c38d8cd0-6ac9-42c1-a694-d1b42b441dee.PNG)


with command ``file`` we found that the file is an SQLite database, and we can view the content with ``cat`` command.

We have a user called "admin" and hash id. With ``hash-identifier`` tool we found that the hash is sha1.



![hash](https://user-images.githubusercontent.com/20625004/187388019-324effee-e859-44d4-bc46-e0c5f5b0c57a.PNG)



users.bak file which is a SQLite database.

We found nothing of use. Now lets run again ``nmap`` with all ports.

```nmap -sC -A  <target IP> -p- ```

We found a new port ``8765``.

Lets 
