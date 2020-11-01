## HTB /FreeLancer

**_created by IhsanSencan_**

**_https://app.hackthebox.eu/challenges/82_**

**_CTF Write up by: sokdr_**

![logo](https://user-images.githubusercontent.com/20625004/97815862-cc69ec80-1c99-11eb-9a3f-f7d93410b4f2.PNG)

### Information Gathering

We found a simple web site with a few clicks and a **_contact me form_**. With the help of a proxy tool like burp we found that the application is hosted on **_Apache/2.4.29 (Ubuntu)**_.

Then i i used **_dirb_** tool to find more paths of the web application.

```
