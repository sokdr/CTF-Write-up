# CTF-Write-up

## Vulnhub -   bossplayersCTF: 1

##### URL: https://www.vulnhub.com/entry/bossplayersctf-1,375/

##### Created by _https://www.vulnhub.com/author/cuong-nguyen,649/_

![logo](https://user-images.githubusercontent.com/20625004/161815571-55e220df-8854-4ac1-8d5d-bd3ad6aa0339.PNG)

First run ``nmap`` to identify open ports.

![nmap](https://user-images.githubusercontent.com/20625004/164456576-e175cdb0-b5bb-42e5-94ed-2458c8a1e453.PNG)

Lets access port ``80``.

![80](https://user-images.githubusercontent.com/20625004/164456674-75417553-5d59-498a-b5c2-e0fdfe2fde02.PNG)

Nothing there, but lets check also ``view page source`` of the page, and we found a comment.

![comment](https://user-images.githubusercontent.com/20625004/164456938-5726a38f-2972-4193-8318-1894852238f5.PNG)

It seemed like Base64, so decode it using ``base64`` command. The output shows another encodeded text, it seems like Base64, so decoded it again, now
we found something interesting a path.

![base64](https://user-images.githubusercontent.com/20625004/164457930-258c0850-2322-4a66-b4f6-089e0820d2e5.PNG)

Access the new page.

![php](https://user-images.githubusercontent.com/20625004/164458185-1d8e0e27-d26f-4ef2-ae3e-c399dd7f73b9.PNG)

It seems to be a to-do list, from the list we understand that ``ping`` and ``privilege escalation`` are not fixed yet.

