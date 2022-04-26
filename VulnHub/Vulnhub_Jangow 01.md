# CTF-Write-up

## Vulnhub -  EvilBox: One

##### URL: https://www.vulnhub.com/entry/jangow-101,754/

##### Created by _https://www.vulnhub.com/author/jangow,823/_

At first we run ``nmap`` tool to find open ports.

![nmap](https://user-images.githubusercontent.com/20625004/165245616-c789d986-0577-426c-92ac-c79aebb7b265.PNG)

``FTP`` 21 and port 80 are open, lets access the web ports.

![web](https://user-images.githubusercontent.com/20625004/165245967-c18326be-036d-4409-8ba8-5edba65a83a3.PNG)

Lets use ``gobuster`` to find any interesting paths.

![gobuster](https://user-images.githubusercontent.com/20625004/165246229-5cda1737-e99f-4142-9ada-b95899b9af68.PNG)

Nothing intersting, now lets go back and access ``site`` path.

![site](https://user-images.githubusercontent.com/20625004/165246346-c191ce92-dced-4fad-8b94-16bce9c244e4.PNG)

Looking around, nothing seems to be anything of interest except for the ``Buscar`` page found.

![buscar](https://user-images.githubusercontent.com/20625004/165246526-91b83312-4cd2-46bb-92ff-931a8021b7ed.PNG)

We should check the parameter ``buscar`` for command injection.

![command_injection1](https://user-images.githubusercontent.com/20625004/165247526-608ab0a0-b679-4283-b5a4-3ef38bf07f03.PNG)

It seems it is working, i tried reverse shell but nothing worked, so lets look around with commands.

![command_injection2](https://user-images.githubusercontent.com/20625004/165247903-cc094986-7cd8-4820-8a83-e1c1abda6e3b.PNG)

We found users ``jangow01`` and ``desafio02``. lets access the home directory of user ``jangow01``.

![user_flag](https://user-images.githubusercontent.com/20625004/165248265-4e83f30a-b3e2-46ee-a951-8e44067e3f85.PNG)

We found the _user flag_, nice.





