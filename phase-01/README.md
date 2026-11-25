# DNS Analysis

## 1. Objective 

Using theory from coursework and practical application through Wireshark, investigate how DNS resolves domain names into IP addresses and analyzing DNS queries and responses

## 2. Environment

* Operating System: Windows
* Tool: Wireshark
* Network: Home Network
* Target domain: Github (github.com) 
* Main Protocols analyzing: UDP, DNS, IP

## 3. Methodology

* Select the network interface I'm using in Wireshark -- which is through ethernet
* Flushed DNS through ipconfig /flushdns
* Started packet capture 
* Visit the targeted website
* Applied DNS filter
* Inspected DNS queries and corresponding respones
* Examined DNS record types and returned IP addresses


Filters I used: \
| Filter  | Purpose
|:---|:---|
|dns| Display dns traffic|
|tcp.port == 53 <br> udp.port == 53| Check both UDP and TCP 
|dns.qry.type == 1 | Filter A record queries |
|dns.qry.type == 28 | Filter AAAA record queries |
|dns.qry.type == 65 | Filter HTTPS record queries
|dns.qry.type == 5| Filter CNAME | 
|dns.id == {target_id} | Filter specific request/response |

 



## 4. Observation

While accessing Github, I observed multiple DNS queries beyond the initial DNS lookup. 

1. Multiple DNS record types 

The capture showed A, AAAA, and HTTPS DNS queries for github.com. The A query returned an IP of 140.82.114.3 while the Type AAAA and HTTPS, responses contained SOA records in the authority sections rather than the requested records

2. Additional Hostname resolution

Additional DNS queries were observed for avatars.githubusercontent.com, github-cloud.s3.amazonaws.com


3. CNAME records

A CNAME record was observed for github-cloud.s3.amazonaws.com, demonstrating the use of DNS aliases to direct hostname resolution toward another hostname

4. Conclusion

Through my findings, I observed that accessing sites actually involve multiple hostnames and requesting different DNS record types. 

This capture also demonstrated that multiple infrastructure could be involved, and a single website doesn't necessarily rely on a single hostname






## 5. Evidence

**Type A Query**
![Type A DNS Query](phase-01\images\image-4.png)
![Detailed information on Type A DNS query](phase-01\images\image-5.png)


**Type AAAA Query**
![Type AAAA DNS Query](phase-01\images\image.png)
![Detailed Information on DNS Query](phase-01\images\image-1.png)

**Type A Query of avatars.githubusercontent.com**
![Type A Query of a different github domain](phase-01\images\image-2.png)

** Type A With CNAME **
github-cloud.s3.amazonaws.com
![DNS query of github-cloud.s3.amazonaws.com](phase-01\images\image-6.png)
![Detailed Information of github-cloud.s3.amazonaws.com DNS query](phase-01\images\image-7.png)




