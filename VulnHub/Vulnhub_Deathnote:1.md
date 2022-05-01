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
