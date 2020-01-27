# Security Engineering

## Intro
This is going to be my brain dump of useful interview tips, articles, and papers that I come across that I have found useful in my studies for getting a security engineering job.

Security Engineering is one of the hardest paths in computing to break into on your own.  I hope this article is helpful to any that stumble upon it.

## General Interview Tips
+ Stay calm and dont take things personally
+ Dont be phased by interviews that dont go well
+ Focus on what you do know and what you are great at

## Systems Administration & DevOps

Cybersecurity requires top notch systems administration skills in order to be successful in implementing new protections on the end devices that need protecting.  DevOps knowledge is key if one is to fully understand the systems that they are working with and attempting to ingest logs from. The more stacks and technologies you know the more things you can secure.

### General Cloud
+ the cloud is just another way of saying "someone else is managing my hardware"
### Azure
+ This is microsofts cloud platform.  It is essentially a more windows enterprise friendly AWS and its admin console can be 
### AWS
+ lambda functions
    - javascripts that run when an endpoint is hit
    - They serverless backend functions essentially
    - publically accessable
### Ansible
+ system administration automation
+ its just a fancy python script that reads a yaml file
+
### Log Analysis
+ Windows
+ Linux

## Programming Tips
### Algos
+ Fastest sort
    - quick sort in most cases
### Python syntax specifics
+ decorators
    - function wrappers that are functions
    - allow for returning new data and running other functions inside of itself
    ```python
    @make_pretty
    def ordinary():
        print("I am ordinary")

    # is the same as
    def ordinary():
        print("I am ordinary")
    ordinary = make_pretty(ordinary)
    ```
## Networking Tips
+ How does traceroute work (different on windows and unix)
+ TCP Flags
    - Syn
        + Synchronize
    - Ack
        + Acknowledge successful receipt of a packet
    - Rst
        + Sent when a packet is received that the receiver was not expecting
    - Urg
        + The receiver will be notified to process the urgent packets before others and will be notified when urgent data has been received
    - Psh
        + Push flag is like the Urg flag but the packets are processed as soon as they are received
    - Fin
        + The finished flag which indicates that there is no more data to be sent after this from the current data stream
    - ECE
        + indicates that peer is ECN capable
+ TTL
    - A part of the IP section of a packet and indicates if the packet is too late to be considered valid
    - Commonly set manually for DNS Records in a resolvers cache
    - speeds up website lookup speed 
    - should be set to lower number for local lookups
+ CIDR
    - Classless Interdomain routing
    - No need for class based A, B, C IP worries
    - Define network address as prefix
    - /24 is 24 network bits 8 host bits

## Security Applications & What they do
### Firewall
+ Network edge device
+ Commonly hosts VPN server
+ Analyze traffic based upon rules and filter traffic coming from unsecured or suspicious sources
+ Next Gen firewalls use deep packet inspection which looks at the data within the packet itself

### IDS
+ Network Intrusion Detection System -> NIDS
    - Snort
    - surricata
+ Host Intrusion Detection Systesm -> HIDS
    - File integrity monitoring
    - windows reigstry monitoring
    - Monitoring the state of the system
    - OSSEC + Atomicorp
    - chkrootkit

### IPS
+ sits between the edge device of the network (usually firewall) and the devices on the inside
+ It can identify threats in a number of ways:
    - Packet analysis
        + looks at packets for binary patterns compared against a database of common signatures
    - Statistical anomaly detection 
        + takes samples of network traffic randomly and compares them to pre-calculated baseline performance level.
### SIEM
+ Splunk
+ ELK Stack

### SOAR tools
+ phantom
+ socless
+ 

## Crypto Basics

### Common Algorithms

### HTTPS
+ Hello
    - Contains SSL information about client include sipher suites and max SSL supported
    - Server hello contains the same information and the intended cipher suite and SSL version to be used
+ Cert exchange
    - Server sends over its SSL Cert
        + name of owner
        + the property (domain its attached to)
        + certificate pub key
        + digital signature
        + certificate validity dates
    - Client checks if it has the CA already trusted
    - Server may request that the client proves itself with the same process
+ key exchange
    - 

## Authentication methods
### LDAP
### LDAPS
### OAUTH
1. The first website connects to the second website on behalf of the user, using OAuth, providing the user’s verified identity.

2. The second site generates a one-time token and a one-time secret unique to the transaction and parties involved.

3. The first site gives this token and secret to the initiating user’s client software.

4. The client’s software presents the request token and secret to their authorization provider (which may or may not be the second site).

5. If not already authenticated to the authorization provider, the client may be asked to authenticate. After authentication, the client is asked to approve the authorization transaction to the second website.

6. The user approves (or their software silently approves) a particular transaction type at the first website.

7. The user is given an approved access token (notice it’s no longer a request token).

8. The user gives the approved access token to the first website.

9. The first website gives the access token to the second website as proof of authentication on behalf of the user.

10. The second website lets the first website access their site on behalf of the user.

11. The user sees a successfully completed transaction occurring.

12. OAuth is not the first authentication/authorization system to work this way on behalf of the end-user. In fact, many authentication systems, notably Kerberos, work similarly. What is special about OAuth is its ability to work across the web and its wide adoption. It succeeded with adoption rates where previous attempts failed (for various reasons).

## Web Attacks Tips
### Anatomy of SQLi and blind SQLi attacks
### Anatomy of XSS attack
### Anatomy of CSRF attack
+ How do you prevent a CSRF attack?
Make sure all XSS vulnerabilities have been patched.  An XSS can read any page on the site using an XMLHttpRequest and grab the CSRF token from the response and then include said token in its forged request.  Token based mitigation is the recommended way to prevent CSRF.  It can either be state based, (synchronizer token pattern) or stateless (encrypted/hash based token pattern).  

## Policy Compliance
### PCI-DSS
[from Forcepoint](https://www.forcepoint.com/cyber-edu/pci-dss-compliance)
1. Firewall to protect cardholder data

2. Update vender-supplied default passwords

3. protect stored cardholder data

4. Encrypt the transmission of cardholder data

5. Protect all systems from malware

6. Develop and maintain secure systems and applications

7. Limit cardholder data access to authorized personnel

8. Unique IDs for all users with cardholder data access

9. Restrict physical access to cardholder data

10. log and monitor all access to cardholder data and network resources

11. Regularly test security systems and processes

12. Enforce an information security policy for all personnel

PCI self-assessment questionnaire to determine compliance level (SAQ). Once you are in compliance and have completed a self-assessment of compliance you can file a formal Attestation of Compliance (AOC).  

## Triaging an attack
[Source from Rapid7](https://blog.rapid7.com/2016/12/13/the-three-steps-for-effective-information-security-event-triage/)

### Step 1: Identify
+ Find artifacts of the incident
+ Looking for the highest value targets involved in the attack
+ Network security monitoring, deeper investigations
+ Find how malware entered the network, what systems it infected, what endpoints it hit
+ Gather logs
+ Extract artifacts
+ look up reputations
+ detonate files in a sandbox

### Step 2: Map
+ Start investigation after gathering the key indicators of threat
+ Begin piecing the artifacts together
+ Draw a timeline of events
+ What was the entry point -> next place -> next place etc
+ Treat it almost like debugging a piece of code
+ focus on why the infected machine was infected
+ Review audit logs
+ playback monitoring recordings
+ draw a timeline

### Step 3: Eradicate
+ Prioritize response based upon the highest value targets
+ Swiftly remove malware from the identified systems
+ restore from backups where possible
+ Should be at step 3 as quickly as possible to catch the attack while in progress
+ Remove malware
+ Delete infected assets
+ Restore from backup

## Security Automation Best Practices
[Rapid 7 White Paper](https://www.rapid7.com/globalassets/_pdfs/whitepaperguide/rapid7-komand-automation-best-practices-whitepaper.pdf)

### What is Security Automation?
Taking a set of tasks and putting those into an automated system is less prone to human error and becomes more efficient.

With a more efficient (repeatable) process, better and faster decisions can be made.  

Having programming talent on the team is an asset for Security Automation as well as having what a well-defined process looks like in mind.  

