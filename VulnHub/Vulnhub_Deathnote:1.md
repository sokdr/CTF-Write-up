# CTF-Write-up

## Vulnhub -  Deathnote: 1

##### URL: https://www.vulnhub.com/entry/deathnote-1,739/

##### Created by _https://www.vulnhub.com/author/hwkds,816/_

![logo](https://user-images.githubusercontent.com/20625004/166140788-8abce583-7943-45dc-b89d-8c4504d931e8.PNG)

Run ``nmap`` ta first to identify open ports.

![nmap](https://user-images.githubusercontent.com/20625004/166147772-58a273ea-c4e9-4949-bc16-e4b4aa202085.PNG)

Access port ``80``.

Nothing lets add it to our host file.

``echo " target ip deathnote.vuln" >> /etc/hosts``

Now access port ``80``.

![port80](https://user-images.githubusercontent.com/20625004/166147863-772ecc8f-5ae9-4a48-b316-ef162bdcc183.PNG)

Digging around we found various web pages.

![hint](https://user-images.githubusercontent.com/20625004/166147935-989400cd-c09e-48f2-85bd-8a6ebd52035b.PNG)

![comment](https://user-images.githubusercontent.com/20625004/166147940-fe26c54a-1d36-49c7-8307-4d0955b05740.PNG)

Lets fire up ``gobuster``.

``gobuster dir -u http://target site -w /path/to/wordlist ``

![gobuster](https://user-images.githubusercontent.com/20625004/166147993-5a3c0b29-e4ab-424b-8cdd-a9156634dc52.PNG)

lest view ``robots.txt``

![robots](https://user-images.githubusercontent.com/20625004/166148040-12e862c1-01f3-468b-b3b2-2b93c291ab8c.PNG)


We understand that the site is using ``wordpress``.

We found some names and hints by viewing the pages. (Users:L, Kira, ryuk) (Hint: notes.txt, iamjustic3)

Lets access the ``wp-login`` page.

![admin](https://user-images.githubusercontent.com/20625004/166148138-7c848bc5-279a-4636-a41f-3c11300a2b47.PNG)

User ``l`` not found lets try with ``kira`` and password ``iamjustic3``.

Success.

![kira](https://user-images.githubusercontent.com/20625004/166148171-0ed612a1-1d66-43eb-b97a-5705ceeabc6c.PNG)

Searching around we found hint ``notes.txt``.

![notes](https://user-images.githubusercontent.com/20625004/166148207-4729d7b9-cf4c-4cae-b0dd-22c51cf53b96.PNG)










