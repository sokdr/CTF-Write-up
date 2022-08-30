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


![bak](https://user-images.githubusercontent.com/20625004/187388454-8ec4242d-fc82-40a4-a578-8436002b34cd.PNG)


with command ``file`` we found that the file is an SQLite database, and we can view the content with ``cat`` command.

We have a user called "admin" with a hash id. With ``hash-identifier`` tool we found that the hash is sha1.


![hash](https://user-images.githubusercontent.com/20625004/187388019-324effee-e859-44d4-bc46-e0c5f5b0c57a.PNG)

In order to find the password you can use online tools such as ``https://crackstation.net/`` or tools such as ``john``.

We will use ``john`` with the following command since we know the hash is of sha1.

``john --format=raw-sha1 sha.txt --wordlist=/path/to/wordlist/``

We finally found the password. Since ``SSH`` port is also open we try to access with username ``admin``.

``ssh admin@targetIP``

No success, after further enumaration we use again ``nmap`` now with all ports.

``nmap -sC -A  <target IP> -p- ``

We found a new port ``8765``.

Now we see a portal.

![admin_panel](https://user-images.githubusercontent.com/20625004/187389686-b8a0e787-68cd-4036-b699-58c3b7204989.PNG)

We use the ``admin`` username and the password that we found earlier and we access the web application.

![admin_panel_1](https://user-images.githubusercontent.com/20625004/187390006-ee1bd23f-f784-4543-b106-500cbe053e59.PNG)

It appears that we can add a comment to the website. Further by inspecting the source code of the page there is comment about another user and an ssh key.

![otheruser](https://user-images.githubusercontent.com/20625004/187390871-e02e78fd-4edb-4481-a9b7-f5e37edc0af5.PNG)

Back on the page we found we try to post something and error pops up that says: ``“Insert XML Code!”``.

Maybe the website is vulnerable to ``XML``, following the guideline ``https://owasp.org/www-community/vulnerabilities/XML_External_Entity_%28XXE%29_Processing`` we try to inject with the comment area the below code.

```<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE root [<!ENTITY test SYSTEM 'file:///etc/passwd'> ]>
<comment>
  <name>Joe Hamd</name>
  <author>Barry Clad</author>
  <com>&test;</com>
</comment>```


