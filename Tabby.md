# CTF-Write-up

Hack The Box

Machine Tabby

//////////////////////////////////

First we fire up nmap.

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 45:3c:34:14:35:56:23:95:d6:83:4e:26:de:c6:5b:d9 (RSA)
|   256 89:79:3a:9c:88:b0:5c:ce:4b:79:b1:02:23:4b:44:a6 (ECDSA)
|_  256 1e:e7:b9:55:dd:25:8f:72:56:e8:8e:65:d5:19:b0:8d (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Mega Hosting
8080/tcp open  http    Apache Tomcat
|_http-title: Apache Tomcat
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=10/29%OT=22%CT=1%CU=36678%PV=Y%DS=2%DC=T%G=Y%TM=5F9AF6
OS:A7%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=108%TI=Z%CI=Z%II=I%TS=A)OP
OS:S(O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST
OS:11NW7%O6=M54DST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)EC
OS:N(R=Y%DF=Y%T=40%W=FAF0%O=M54DNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=
OS:AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(
OS:R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%
OS:F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N
OS:%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%C
OS:D=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 993/tcp)
HOP RTT      ADDRESS
1   59.31 ms 10.10.14.1
2   59.48 ms 10.10.10.194


I did some recon with ssh but nothing.


I browsed manually the web application on ports 80 and 8080.

On the background i had Dirb to brute force paths of the web ports 80 and 8080.

WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://10.10.10.194/ ----
==> DIRECTORY: http://10.10.10.194/assets/                                                                                                                                                                                                                                                                                
+ http://10.10.10.194/favicon.ico (CODE:200|SIZE:766)                                                                                                                                                                                                                                                                     
==> DIRECTORY: http://10.10.10.194/files/                                                                                                                                                                                                                                                                                 
+ http://10.10.10.194/index.php (CODE:200|SIZE:14175)                                                                                                                                                                                                                                                                     
+ http://10.10.10.194/server-status (CODE:403|SIZE:277)                                                                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                          
---- Entering directory: http://10.10.10.194/assets/ ----
==> DIRECTORY: http://10.10.10.194/assets/css/                                                                                                                                                                                                                                                                            
==> DIRECTORY: http://10.10.10.194/assets/fonts/                                                                                                                                                                                                                                                                          
==> DIRECTORY: http://10.10.10.194/assets/images/                                                                                                                                                                                                                                                                         
==> DIRECTORY: http://10.10.10.194/assets/js/                                                                                                                                                                                                                                                                             
                                                                                                                                                                                                                                                                                                                          
---- Entering directory: http://10.10.10.194/files/ ----
==> DIRECTORY: http://10.10.10.194/files/archive/                                                                                                                                                                                                                                                                         
+ http://10.10.10.194/files/statement (CODE:200|SIZE:6507)                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                                                          
---- Entering directory: http://10.10.10.194/assets/css/ ----
                                                                                                                                                                                                                                                                                                                          
---- Entering directory: http://10.10.10.194/assets/fonts/ ----
                                                                                                                                                                                                                                                                                                                          
---- Entering directory: http://10.10.10.194/assets/images/ ----
                                                                                                                                                                                                                                                                                                                          
---- Entering directory: http://10.10.10.194/assets/js/ ----


and port 8080 


home/kali# dirb http://10.10.10.194:8080 /usr/share/dirb/wordlists/vulns/tomcat.txt 

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

WORDLIST_FILES: /usr/share/dirb/wordlists/vulns/tomcat.txt

-----------------

GENERATED WORDS: 87                                                            

---- Scanning URL: http://10.10.10.194:8080/ ----
+ http://10.10.10.194:8080/examples (CODE:302|SIZE:0)                                                                                                                                                                                                                                                                     
+ http://10.10.10.194:8080/examples/jsp/index.html (CODE:200|SIZE:14245)                                                                                                                                                                                                                                                  
+ http://10.10.10.194:8080/examples/jsp/snp/snoop.jsp (CODE:200|SIZE:618)                                                                                                                                                                                                                                                 
+ http://10.10.10.194:8080/examples/servlets/index.html (CODE:200|SIZE:6596)                                                                                                                                                                                                                                              
+ http://10.10.10.194:8080/host-manager (CODE:302|SIZE:0)                                                                                                                                                                                                                                                                 
+ http://10.10.10.194:8080/manager (CODE:302|SIZE:0)                                                                                                                                                                                                                                                                      
+ http://10.10.10.194:8080/manager/html (CODE:401|SIZE:2499)                                                                                                                                                                                                                                                              
+ http://10.10.10.194:8080/manager/jmxproxy (CODE:401|SIZE:2499)                                                                                                                                                                                                                                                          
+ http://10.10.10.194:8080/manager/status.xsd (CODE:200|SIZE:4374)       

On port 8080 we observe an Apache Tomcat 9 Version 9.0.31.

And Login pages on the following links: http://10.10.10.194:8080/host-manager/html and http://10.10.10.194:8080/manager/html 



Smells like LFI lets check it out.


                                                                             
