AWS Cloud History:
	- AWS Cloud launch in 2002 Internally
	- 2003 core strength idea abouth Amazon infrastruture.
	- 2004 Launched Publicly with SQS
	- 2006 Re-launched with SQS, S3 & EC2 in America only
	- 2007 Launched in Europe
	- Appilcations : Dropbox, Airbnb, Netflix, Nasa
	- AWS Cloud Number facts: 1)AWS 2) Microsoft 2) Google 4) allibaba cloud, Orecle, IBM 
	- AWS 74% of market, Microsoft 22%  according to 2019 survey
	- Using AWS build sophisticated, scalable Application 
	- Enterprise IT, Backup & Storage, Big Data analytics, Website, Mobile & Social app hosting, Gamming server etc
	- Uses : 21st century fox, Activision, McDonald etc
	
Structure: 
	- Region : Clustor of data centers based on geo-location e.g: us-west-1
	- Availability Zones: Each Region has Availability zone 3 to 6. 
	- Data-center:
		- Each Availability zone have 1 or more discrete data center. Data center have actual hardware basically.
	- Edge Locations
		- Amazon has 400+ point of persence, you can cache your website over their for low lantency.
	
How to choose an AWS Region:
	- Compliance : according to govt. legal requirement.
	- Proximity: reduce latency
	- Availability service: Service Available on that region
	- Pricing : price varies region to region
	
------------------------------------------------------------------------------------------------------------------

IAM: User & Groups
	- IAM : Identity and Access Management, Global service
	- Root account created by default, Don't share it with anyone.
	- Create User using IAM User and add permission using Group, Inline etc.

IAM: permission
	- Permission Assign by using the JSON document.
	- important parts in JSON : version, Statment : [ { effect, Action, Resource } ].
	- AWS recommend "LEAST PRIVILEGE PRINCIPLE"
	- Create Group --> Add Policy into group --> Assign group to user.
	- Alias: Globally unique, alias name or your account ID.
	
IAM Policies:
	- If user have multiple group policy and Union of that Policy apply for the user.
	- Parts: 
		- Version : required
		- Id: optional
		- Statment : required (defined your Policy here: [ {  } ])
			- sid: optional
			- Effect : required (allow/ deny)
			- Principal : optional ( {AWS : "*"} ), Account/user/role related info
			- Action: required, ( [add you permission e.g "S3:*"] )
			- Resource: required ( [whcih Resource you need declare here] )
			- condition : optional (when policy apply)
	- Three types of Policy
		- AWS managed 
		- Cutome managed (Create by the User)
		- Inline Policy

IAM - Password Policy:
	- Create policy for your password like 8 char, alfanumatic, upper case, lower case, Time need to change etc.
	
MFA - Multi Factor Authentication:
	- Protect account using MFA
	- MFA = password + security device you own (Authy)
	- Adv. if password hacked then hacker need the MFA also for login

MFA Devices:
	- virtual MFA device (authy, google authent	authenticator)
	- Universal 2nd Factor(U2F) pendrive key
	- Hardware key Fob MFA device  (same like app but in harware form)
	- Hardware key Fob MFA device for AWS GovCloud(US)
	- You can register up to 8 MFA device for Per user

How can user access AWS: (For all three need the access key + secret key)
	- AWS console
	- CMD : Created using python boto3 
	- SDK : multiple language optional available 

Cloudshell:
	- CMD functionality in AWS 
	- you can run all the CMD command over here
	
IAM Roles for Services:
	- When Some AWS Service will need to perform actions on your behalf (Service to Service communication Basically)
	- You need to assign Role to the Service in which, using that you are going to access some service. e.g. lambda to rds (give permission lambda for accessing rds)
	
IAM Security Tools: (Audit)
	- IAM Credentials Reports (Account-level) : list of all your account's users and thier credentials
	- IAM Access Advisor (User level) : which user have which permission and when those services were last used.
	

Shared Responsibility Model for IAM:
	- AWS:
		- infrastruture, configuration and vulnerability analysis, Compiance validation
	- User
		- User, Groups, Roles, Policies, and monitoring of app.
	
	- Aws is Responsible for infrastruture and user is for how to use.
	
------------------------------------------------------------------------------------------------------------------
	

EC2 Fundamentals:
	Extra for EC2:
	- EC2 : Elastic compute cloud
		- EC2 instance type : general, compute, memory, storage
		- Security options
		- Purchaging option : on-demand, reserved, savings Plan, spot instance, dedicated hosts, capacity Reservations 
	- EBS : Elastic block store  (virtual storage device)
		- EBS AZ, Snapshot, Deletion, recycle-bin (restore snapshot)
		- AMI, EC2 Instance store, AMI, EFS.
	- ELB : Elastic Load Balancer
		- Types of ELB
	- ASG : Auto-scaleing Group
	
AWS Buget Setup:
	- using root account give access to activate the billing innformation
	- My Account --> IAM User Role Billing information
	- using IAM user set/check the billing : Free tier
	- Budget --> add your email for message
	


Amazon EC2: (Elastic Compute Cloud)
	- most popular
	- infrastruture as a service
	- Consists using:
		- Renting VM (EC2 OS)
		- Renting Virtual Drive (EBS, EFS)
		- Distributing load across machine (ELB)
		- scaleing the service using : (ASG)
	- By defauls root volume deleted by the deleting the ec2 instance.
	
EC2 sizing & configuration options:
	- OS
	- CPU
	- RAM
	- Storage:
		- Network-attached (EBS & EFS)
		- Hardware (EC2 Instance Store)	: FASTER then n/w 
	- Network card: Speed of card, Public IP address
	- Firewall rules: Security Group
	- Bootstrap script: configure first launch
	
	
EC2 User Data:
	- During the fisrt time boot giving script. 
	- Only run once (during the first time create)
	
EC2 instance types:
	- e.g. t2.micro(free tier), m5.16xlarge 
		- t: instance class, 2: generation, micro/16xlarge: size in the instance class
		
	- General Purpose : diversity like: compute, memory, networking etc, --> M, t, a1
	
	- Compute Optimized : fast computing (high Performance), --> c
	
	- Memory Optimized : Process large data sets in memory, --> R, x, z1d, high
	
	- Storage Optimized : sequential read & write access for large local storage, --> I, d, h
	
	- Accelerted Computing : 
	- Instance Feature :
	- Measuing Instance Performance : 


Security Group:
	- Control traffic by allowing & denying the IP/connection
	- only allow rules need to add, by default all deny
	- Act like a firewall on the EC2 instance
	- one instance have multiple SG
	- SG based on region 
	- If you application showing the timeout error, then check te security group
	- by default: all inbound --> blocked, all outbound --> allow

Classic Ports to know:
	- 22   = ssh(secure shell) 
	- 21   = FTP (File transfer Protocal)
	- 22   = SFTP (Secure FTP)
	- 80   = HTTP sites
	- 443  = HTTPS
	- 3389 = RDP (Remote Desktop Protocal)

SSH connect to PC:
	- SSH configure in PC + inbound rule for ssh in instance
	- chmod 0400 pemfile.pem
	- ssh -i pemfile_without_space ec2-user@public-ip 
	
Instance IAM role:
	- Give the permission services using the IAM role 

EC2 Instances Purchaging Options:
	- On-demand Instances:
		- short workload, pay by second, price 
	- Reserved Instances: 72% discount (on-demand)
		- 1 & 3 years, long workload
	- Saving Plans: 72% discount (on-demand)
		- 1 & 3 years, commitment to an amount of usage, long workload e.g. 10/hr for 1ys
	- Spot Instance: 90% discount
		- short workload, chep, can lose instance(less reliable), not suitable to critical jobs
	- Dedicated Hosts: 
		- book entire Physical server
		- most expensive, (using this Purchaging ondemand + reserved one)
	- Dedicated Instances: 
		- your instance run on hardware that's dedicated to you.
		- other customers will share your hardware
	- Capacity Reservations: 
		- reserved Capacity in a specific AZ for any duration
		- no time commitment, no billing discount
	
------------------------------------------------------------------------------------------------------------------
EC2 Instance Storage:

EBS: (Elastic Block Store)
	- Network Drive, thing like USB stick
	- After removing the instance, Persist data inside the EBS
	- One EBS can have One Instance but not vise-versa
	- scope onlt in the specific Availability zone
	- Free tier : 30 GB, Gerneral Purpose SSD per month

EBS volume: (Network Drive, not Physical drive)
	- use Network to communicate the Instances, might be  latency bcoz using n/w.
	- Attach or detach possible
	- EBS belog to AZ so for changing AZ need to take snapshot and then move the AZ
	- Capacity by GBs size or IOPS

EBS- Delete on Termination attribute:
	- Option in creation time to delete, like checkbox
	- by default root volume enable, other EBS disable

EBS Snapshots:
	- Any time you can create snapshot of EBS
	- can copy snapshots across AZ or Region
	
EBS Snapshots Features:
	- EBS Snapshot Archive:
		- move to "Archive tier", 75% cheaper
		- takes 24 to 72 hr for restoring
	
	- Recycle Bin for EBS Shapshots:
		- set rule for deleting EBS, will store in the Recycle bin.
		- retention from 1day to 1yr
		
	- Fast snapshot restore(FSR)
		- no latency, when you recover EBS
		- costly


AMI Overview: (Amazon machine Image)
	- Customizable, You can use and modification, then create that as new AMI, 
    - Faster boot / configuration time reduce
    - we heve public AMI(free), your own AMI(you need to take care), or marketPlace AMI(purchaged)
    - using AMI you can create instance
	- region specific, for new region need to create new AMI(or you can make copy for new region)
	

EC2 Instances store: (Ephemeral)
	- EBS volume are Network drive so limited Performance
	- for high-Performance hardware disk, Use EC2 instance store
	- Better I/O
	- If terminate EC2 then instance store loss.
	- good for buffer / cache/ temporary content

EBS Volume Types:
	- 6 types:
		- gp2/gp3 (SSD) : normal price & Performance,
		- io1/io2 (SSD) : high Performance & low latency 
		- st1 (HDD) : low cost, frequently accessed
		- st2 (HDD) : lowest cost, less frequently accessed
	- For root volume only can use gp or ip type volume

gp type:
	- used for test, dev environment, 1 to 16 tb, (3000 IOPS).
	- gp2 throughput and IOPS connected, so increase the both
	- gp3, not linked IOPS ans throughput, so increase independly

EBS volume IOPS type:
	- io1/io2 have more throughput & IOPS (16000 IOPS), 4 to 16 TB
	- low latency, support multi-attach
	- io1 --> 32000 IOPS maximum
	- io2 --> 256000 IOPS maximum
	
Hard Disk Drives:
	- Cannot use as root vol. 125GB to 16TB
	- use for big data

EBS multi-Attch - io1/io2:
	- allow same EBS to multiple Instances in the same AZ
	- When you have TB data that time multi attch useful for accessing data for different-2 instance
	- up to 16 EC2 Instances at a time
	- File system not use (XFS, Ext4...etc), used by aws created.

Amazon EFS: (Elastic File System)
	- n/w used, support multi-AZ for EC2
	- Highly Available, scalable, expensive like (3 * Gp2)
	- used for webserving, data sharing
	- only support "linux AMI" not windows
	- KMS support
	- pay per use, like lambda

EFS - Performance & Storage Classes:
	- 10 GB+ throughput, NFS support, petabyte-scale handle
	- Performance Mode available on the creting Time like maxi/o or Gerneral Purpose

EFS - Storage Classes:
	- Storage Tier (Lifecycle Management feature move file after N days)
	- Standard --> Infrequent access(EFS-IA)
	- support multi-AZ for prod, for dev one AZ
	- 90% cost saving

EBS vs EFS vs Instances Store :
	- EBS volume:
		- One instance (except multi-attach io1/io2)
		- locaked at AZ
		- to migrate EBS need the Snapshot across AZ
		- by default root EBS volumes get terminate with Instances
	- EFS volume:
		- mount 100 of instance across AZ
		- Only for linux instance
		- EFS higher price then EBS
	- Instances Store
		- high-Performance hardware disk, physical attach to instance, max IOPS
		- If instance remove then data remove
	

------------------------------------------------------------------------------------------------------------------

AWS Fundamentals: ELB + ASG

scaleability & High Availability:
	- scaleability:
		- scaleability means can handle greater loads by adapting
		- 2 types: Vertical , Horizontal (Elasticity)
		- Vertical scaleability: Increase the size, scale up/Down
		- Horizontal scaleability: add more person/items/Instance Instances, scale in/out, ASG, load-balancer

	
	- High Availability:
		- It means running you app at least 2 data centers.
		- goal to service data-center loss
		- High Availability == multi AZ
		- ASG with multi-AZ, load-balancer with multi-az 
	
Load Balancing:
	- serve traffic to multiple server
	- e.g. ELB

Why Load Balancing:
	- spreading load across Instance
	- single point of access(DNS) for your APP.
	- for handle failures of Instance
	- available health check, SSL, enforce stickiness, High Availability, sent public traffic to private traffic
	
ELB (Elastic Load Balancer):
	- managed by aws, can integrate with EC2, ASG, ECS, ACM, CloudWatch, Route 53, WAF etc
	- Health check : if instance not healthy, then not sent the request on that Instance

Types of load Balancer:
	- CLB (Classic Load Balancer) : 2009, not used now, old generation
	- ALB (Application Load Balancer): 2016, for Http, Https, websocket -> layer 7
	- NLB (Network Load Balancer): 2017, for TCP, TLC(secure TCP), UDP -> layer 4
	- Gateway Load Balancer: 2020, GWLB, -> layer 3, IP protocal
	
Load Balancer SG:
	- user to load Balancer (role : allow internet -->  https/http)
	- load-balancer to instance (role : allow load-balancer --> instance )

ALB:
	- woorked on layer 7, load balancing to multiple Http app (target group)
	- support http,https, websocket
	- support routing based on "URL path", hostname, query string, header
	- great fit with Docker + ECS
	- support dynamic port mappint with ECS
	- get fixed hostname by load-balancer
	- true ip of the client in the header "X-Forward-For", and for true port "X-Forward-Port" and Proto "X-Forward-Proto"
	- Clint IP --> load-balancer --(use private LB ip)--> EC2 instance 

Target Group:
	- can be EC2 instance with ASG, ECS tasks, lambda function
	- Create target group along with Instances
	- Configuration of ALB like EC2 instance shouldnot access te internet directly by the public IP so for that only allow the security group to get http request from the ABL with 80/443 port, and ALB security group have the http internet access.
	
NLB:
	- layer 4, handle TCP & UDP traffic
	- handle million of request, low latency
	- NLP has one static IP per AZ, support Elastic IP
	- not free Tier
	- NBL --> ALB (goog combination)
	- health checks support TC, Http & Https
	
GLB:
	- layer 3, deploy, scale & manage a fleet of 3rd party n/w virtual appliances in aws
	- GBL is used for the checking the request and then redirect to the instance, checking with the help of 3rt party security app.
 	- GENEVE protocal on port 6081 --> GLB
	
Sticky Session (session Affinity):
	- same client redirect to same instance (sticky) using LB
	- works with CLB, ALB, NLB
	- cookie help to achive this
	- handle the user data session like login user info
	- type of cookie 
		- Application based cookie
			- Custom cookie
				- generated by the target, cookie name should be unique, don't used reseved words like AWSALB, AWSALBAPP, AWSALBTG
			- Application cookie
				- Generated by the load Balancer, reserved Name : AWSALBAPP
		- Duration based cookie
			- cookie generated by the load Balancer
			- reserved name: AWSALB, AWSELB

Cross-Zone Load Balancing:
	- Each load balancer distributes load evenly across the AZ, e.g. 50% us-east-1a, 50% us-east-1b, so each instance get same amount of traffic
	- without cross zone, based on AZ they are not getting same amount of traffic
	- ALB -> Enabled automatically, not chargable
	- NBL / GBL --> default disable, chargable
	
	
SSL/TLS - Basics:
	- SSL certificate allow traffic b/w your client and LB to be encrypted in transit.
	- SSL (secure sockets layers), TLS (transport layer security), TLS > SSL (more used)
	- public SSL certificates issed by GoDaddy, Symantec, GlobalSign, Comodo etc.
	- Users --(https encrypted)-> LB --(HTTP private VPC)-> EC2
	- ACM can have your certificates
	- Client can use SNI (Server name indication) to specify hostname

SSL- SNI (Server Name Indication):
	- SNI solve the problem of loading multiple SSL cerificates onto one web server (to serve multiple websites)
	- using SNI handle multiple SSL certificate for different-2 website
	- workes with ALB,NLB, CLoufront
	
Connection Draining:
	- connection Draining - for CLB
	- Deregistration Delay - for ALB & NLB
	- time to complete "in-flight request" until instance mark as un-healthy
	- set time b/w 1 sec to 3600 sec (default 300 sec), for disable set 0 sec
	- help to complete the request from the instance

ASG (Auto scaleing Group):
	- load can change any time so that we can use ASG for scale out and scale in, have power that if any instance unheathdy then terminate that and create new one.
	- minimum capacity, Desired capacity and maximum capacity
	- ASG is free
	- ASG works with LB like 
		- Users --> ELB --> ASG (good combination)
	- for ASG need to create launch template, in the template can use AMI, instance type, EBS volume, SG, IAM role, VPC, LB etc.
	- We can add the cloudwatch alarm for ASG
	
ASG- Scaling Policies:
	- base on CPI, request count, network in/out etc
	- Dynamic Scaling:
		- target Scaling:
			- if cpu > 40% set directly
		- simple scaling:
			- if cpu > 80% then cloudwatch alarm trigger 
	- Schedule Scaling:
		- scaling based on user patterns, e.g. friday 10 to 5 
	- Predictive Scaling:
		- schedule scaling ahead, based on history
	
Scaling cooldown:
	- after scaling activity your ASG have cooldown period (default 300 second)
	- during cooldown no scaling like up or down

ASG- Instance Refresh:
	- Goal: update launch template and then re-creating all EC2 Instance

------------------------------------------------------------------------------------------------------------------

Amazon RDS Overview:

RDS: (relational Database Service)
	- managed DB, use SQL
	- supports: postgres, MySQL, MeriaDB, Oracle, Microsoft SQL Server, Aurora

Advantage over using RDS: (vs ec2 personal database)
	- managed service, provisioning, OS patching
	- continuous backups & restore option
	- Monitoring DB, Read replicas for performance
	- Multi-AZ, scaleability option (Verical + Horizontal)
	
disadvantage RDS:
	- But you can't SSH through the instance to RDS

RDS- Storage Auto Scaling:
	- used for scaling the RDS storage
	- detect the rds that running out of storage, auto scale
	- support all DB in rds, need to Set Maximum Strorage Threshold
	- useful when unpredictable workload

RDS Read replicas vs Multi-AZ:

Read replicas:
	- upto 15 replicas, within and cross AZ & region, replicas in ASYNC,
	- any replica you can promoted as main DB, that time you need to update the connection string for read
	- best use case is all the analysis you can perform on the read replicas and main read replica not effected. (only Select perfomed)
	- no cost if the replica in same region, if different region then n/w cost for reading

RDS multi AZ: (Disaster Recovery)
	- Sync Replication, One DNS name - automatic app failover 
	- Increase Availability, if any failover occour then automatically change the master DB to standby RDS
	- no manual intervation, cannot access standby RDS

Note:Yes, We can set RDS read replicas as multi-AZ

RDS - From single-AZ to Multi-AZ:
	- Zero downtime operation
	- modify --> change to multi-AZ

Amazon Aurora:
	- not open sourced, menaged by AWS
	- postgres & MySQL supports aurora DB
	- 5x Performance MySQL, 3x Performance postgres
	- storage grow automatically 10GB to 128TB
	- can have 15 replicas, very fast, Aurora costly 20% more

Aurora High Availability & Read Scaling:
	- 6 copies across 3 AZ
	- very fast, Multi-AZ Support
	- automated failover for master in less then 30 sec
	
Aurora DB Cluster:
	- Writer Endpoint : Pointing to the mater 
	- Reader Endpoint (ASG): Connection Load Balancing

Feature of Aurora:
	- automatic failover, backup & recovery, Isolation and security
	- zero downtime, advanced monitoring etc

RDS & Aurora security:
	- For Encryption:
		- DB master & replicas can encrpt using KMS
		- If master is not encrypted, then read replicas cannot be encrypted.
		- To encrypt an un-encrypted DB, frist create DB Snapshot & restore as encrypted
	- "in-fight Encryption" supported, (default TLS ready)
	- using IAM user can connect the DB
	- support security Group
	- No SSH available
	- audit logs support, can check in CloudWatch
	
Amazon RDS Proxy:
	- RDS proxy is never publicly accessible (must use VPC)
	- using proxy enforce IAM authentication for DB
	- no code change required to use this
	- reduce RDS failover 66%
	- help in pooling the connections, minimize open connections

Amazon ElastiCache:
	- ElastiCache is managed by redis or Memcached
	- Using ElastiCache after query it will create the cache memory for that query.
	- high-Performance, low lantency, stateless
	- helps to reduce the load to the DB
	- aws take care of OS maintenance, optimization etc
	- For using this need to code change require in APP
	- worked like as cache memory
	- Stateless means session data store in cache so login user not need to login again like sticky
		
Redis VS Memcached:
Redis:
	- Multi-AZ with auto-failover
	- high-Availability, scale read replica
	- backup & restore Features
	- supports sets and sorted sets
	
Memcached:
	- Multi-node (sharding) for partitioning
	- No HA , no persistent
	- No backup & restore
	- multi-threaded architecture
	
Caching Implementation:
	- data maybe out dated
	- check the pattern for Caching
	- Lazy loading/Cache-Aside/Lazy Population:
		- first check in ElastiCache then check in the rds then write in the ElastiCache.
		- pros: only requested data cached
		- cons: data maybe outdated
	- write Through:
		- add or update cache when db is updated
		- pros: reads are quickly
		- cons: missing data until it is added
	
Cache Evictions and Time-to-live:
	- 3 ways can occur cache Evictions
		- delete item explicitly
		- memory full then
		- after set ttl
	- ttl can few second to hours or days
	
Amazon memoryDB for redis:
	- redis compatible, durable, in-memory etc
	- ultral-fast Performance 160 million/second
	- Support Multi-AZ, scalable
	- use cases: web & mobile apps, online gaming, streaming
------------------------------------------------------------------------------------------------------------------	
Route 53:

DNS: (Domain Name System)
	- change hostname to IP
	- backbone of the internet 
	- Domain Registrar: route 53, GoDaddy..
	- DNS Records: A, AAAA, CNAME, NS
	- Zone File: contains DNS Records
	- Name Server: resole DNS query
	- TLD(Top level domain): .com, .us, .in etc
	- SLD(Second level Domain): amazon.com, google.com


Route 53:
	- HA, scalable, Fully managed and authoritative DNS
	- authoritative = customer can update DNS Records
	- route 53 also a domain register
	- 100% Availability
	- 53 --> DNS Port number  

Route 53 - Records:
	- each records contains --> domain info(url link), record type(A, AAAA..), value(IP), routing policy(how route 53 responds query), TTL - amount of time cache
	- Route 53 records type: A, AAAA, CNAME, NS
	- A - ipv4, AAAA - ipv6, CNAME - hostname to another hostname, NS - Name Server for the hosted zone
	
Hosted zone:
	- container that define how the route traffic from domain to sub-domain
	- Public hosted zones: can talk to internet
	- private hosted zones: cann't talk to internet, use VPC (internal in the organization)
	- pay 0.5$ per month
	
Route 53 - Records TTL:
	- will Cache the url domain result till the ttl
	- High TTL(24 hr)
		- less traffic, possible outdated Records
	- Low TTL(60 sec)
		- more traffic on route 53(cost you), no outdated records
	- default 300 Second
	- TTL is not applyed for alias records

CNAME vs ALIAS:
	- AWS Resource(load-balancer & cloudfront) need to expose the AWS hostName(URL domain)
	
CNAME:
	- point hostname to other hostname, e.g. app.mydomain.com to bla.anything.com
	- only for non-root domain

Alias:
	- Point a hostname to an AWS Resource, e.g. app.mydomain.com to bla.amazon.com
	- works for root domain and non root domain
	- Free of charge
	- navitve health check
	
Alias Records:
	- it is extension of DNS functionality
	- Automatically recognize change in the resource's IP address
	- unlike CNAME, it can used as top node, like amazon.com (direct)
	- Alias Record is always of type A/AAAA for AWS resource
	- can not set TTL

Route53 - Routing Policies
	- responde to DNS query
	- routing means: not like load-balancer for traffic, it cann't route the traffic, it responds only the DNS quiers
	- Routing Policies:
		- Simple, Weighted, failover, Latency based, Geolocation, multi-valued ans, Geoproximity
	
Routing Policies - Simple:
	- route traffic to a single resource
	- can specify multiple values then server return all IP address the client randamly choose any one.
	- alias enabled, specify only one aws Resource
	- can't be do health check

Routing Policies - Weighted:
	- control the % of the request for each specfic Resource
	- assign weight our according
	- DNS must have same name and type
	- assign weight 0 means stop sending , 100 mean all sent to that
	- TTL available

Routing Policies - Latency based:
	- Redirect to the resource that has the least latency close
	- used when lantency was concern
	- latency based on traffic b/w users & AWS regions
	- can be associated with health check

Route 53 - Health checks:
	- Http Health checks are only for public resource
	- health check for automated DNS failover:
		- monitor endpoints
		- monitor Health check of other health check (calculated health checks)
		- based on CloudWatch alarms check (Private hosted zone)
	- health checks are integrated with CW metrics
	

Health checks - Monitor an Endpoint:
	- about 15 Global 15 health checker will check the Endpoint
	- intervel can set 10(costly) sec or 30 sec
	- if > 18% healty the its healthy
	- health checks can be pass and fail by first 5120 bytes (string health check)
	

Health checks - calculated health checks:
	- combine the health check result and then decide
	- connected as AND, OR and NOT ways
	- can monitor 256 child health checks
	- if any health check fail then don't effect anything
	

Health checks - Private hosted zone:
	- route 53 health checks are outside the VPC
	- can't have access the pricate endpoints
	- you can create cloudwatch metix then using this alarm for health checks 

Routing Policies - Failover(active passive):
	- check the mandatory health check (primary instance)
	- if failover, secondary instance work for this

Routing Policies - Geolocation:
	- different from latency policy, you can restrict the user IP based on location. e.g. US person can only go to the this IP like that.
	- default also can assign if location not match
	- can associated with health check

Geoproximity Routing Policy:
	- it is based on the geografic location of the users and Resource
	- ability to shift more traffic to perticular Resource by defining "BIAS"
	- bias from 1 to 99 +ve increment, -1 to -99 -ve decrement.
	- Resource based on region, latitude & longitude
	- must use route 53 traffic flow advance option to use this
	- visual editor have in route 53 
	
Routing policy - IP-based:
	- routing based on client IP address
	- you need to provide the list of CIDR for client IP (USER-IP-to-endpoint mapping)
	- use for Optimize Performance, reduce network cost
	userA(203.0.3.0) --> CIDR (location1 : 200.0.3.0/24) --> base on location1 go to IP address
	
	
Routing Policies - Multi-value:
	- same as simple by it have the health check functionality
	- so only send the healthy IP address to client so can can redirect to any IP address, bcoz all are healthy
	
	
3rd party Domain Registrar vs DNS Service:
	- domain can by from any Registrar like go-daddy, amazon.. etc, you need to pay annual changes..
	- Domain Registrar usually Provide the DNS service to manage your Records
	- you can use another DNS Service to manage your DNS Records. e.g. purchase domain from GoDaddy and use route 53 to manage your DNS Records
	- Change the NameServer name of Amazon DNS with the GoDaddy NameServer Names.. (it will redirect godday to amazon)
	- Domain Registrar != DNS service
	- Steps:
		- Create Hosted zone in route 53
		- Update NS records of 3rd party website to use Route53 NameServer
	
------------------------------------------------------------------------------------------------------------------

VPC - Crash Course: (2-3 ques in exam)
	- VPC topics:
		- VPC, Subnets, Internet Gateways & NAT Gateways
		- Security Groups, Network ACL (NACL), VPC flow logs
		- VPC Peering, VPC endpoints
		- Site to Site VPN & Direct connect
		
VPC & Subnets Primer:
	- VPC: Private network inside your region Resource
	- Subnets: Allow you to partition your network inside your VPC (private & public subnet)
	- Public Subnet: have accessible from the internet
	- Private Subnet: don't have accessible from internet
	- Route Table: Use to define the internet b/w subnets
	
Internet Gateway & NAT Gateways:

internet Gateways:
	- helps our VPC instance connect to internet
	- Public subnet have a route to the internet Gateway

Nat Gateways(AWS managed) & NAT instance (self managed):
	- allow the instance in your private subnets to access the internet, while remaining private

Network ACL & Security Groups:

NACL:
	- it is a firewall which controls the traffic at subnet level
	- allow/deny rules, rule includes only IP addresses
	
Security Groups:
	- A firewall that controls traffic from an ENI/an instance level
	- only allow rules, rule includes only IP addresses
	
VPC Flow Logs:
	- Using logs capture information about IP traffic 
		- VPC flow logs
		- Subnet Flow logs
		- Elastic Network Interface flow logs
	- Helps to monitor & trableshoot connectivity issues
		- Subnet to internet, subnet to subnet, internet to subnet etc
	- capture n/w information form ELB, ElastiCache, RDS etc.
	- we can send the logs data to S3, cloudwatch etc
	
VPC Peering:
	- Connecting two VPC, Privately using AWS n/w
	- must not have overlapping CIDR (IP range)
	- VPC peering not transitive (a-b, b-c so not a-c directly)
	
VPC Endpoint:
	- Endpoint allow you to connect to AWS services using private network instead of public n/w
	- enhanced security, lower latency
	- VPC Endpoint Gateways: S3 & DynamoDB
	- VPC Endpoint Interface: the rest
	
Site to Site VPN & direct connect:

Site to Site VPN:
	- connect VPN to AWS
	- the connection is automatically encrypted
	- working using the public internet

Direct Connect:
	- Establish a physical connection b/w onpremis to AWS
	- to connection is private, secure, Fast
	- use private n/w, take mount to setup

VPC Closing comments:
	- VPC: Virtual Private Cloud
	- Subnets: Tied to an AZ, network partition of the VPC
	- Internet Gateway: at the VPC level, provide Internet Access
	- NAT Gateway / Instances: give internet access to private subnets
	- NACL: Stateless, subnet rules for inbound and outbound
	- Security Groups: Stateful, operate at the EC2 instance level or ENI
	- VPC Peering: Connect two VPC with non overlapping IP ranges, non transitive
	- VPC Endpoints: Provide private access to AWS Services within VPC
	- VPC Flow Logs: network traffic logs
	- Site to Site VPN:	VPN over public internet between on-premises DC and AWS
	- Direct Connect: direct private connection to a AWS

------------------------------------------------------------------------------------------------------------------
Date: 25/1/2024

Amazon S3 Introduction:
	- Amazon S3 workes as backborn of AWS
	- Amazon S3 Use Cases:
		- Backup & storage, Disaster Recovery, Archive,
		- Hybrid cloud storage, Application hosting, 
		- Big Data analytics
		- Software Delivery
		- Static website hosting
	- Store data in object
	- Globally unique name
	- Bucket is define as region level
	- Object file has a key (which is a full path to access the object)
	- key = Prefix + object name

Amazon S3 - Object(cont.):
	- max object size 5TB (5000GB)
	- if more then 5GB, must use multi-part upload
	- Metadata (file + user meta info)
	- version also supported

Amazon S3 - security:
	- User Based:
		- IAM policies: allow to user for API
	- Resource-based:
		- Bucket Policy: add rule to allow accounts
		- Object Access Control list(ACL): on apply object (finer grain)
		- Bucket Access Control list(ACL): on apply Bucket all object (less common)
	
Note: IAM vs S3 object policy policies, IAM user can access if it is allow or resource policy allow, but there's no explicit deny (always DENY is more powerful)

	- Encryption: object default encrypted using amazon S3

Bucket Setting for block Public Access:
	- used for prevent company data leaks
	- always deny to access object if it is enable

Amazon S3 - Static Website Hosting:
	- S3 can host the static Website
	- If you get 403 Forbidden (then check the bucket policy - should allow)

Amazon S3 - versioning:
	- supported Object versions in Amazon S3
	- enabled on bucket level
	- same key will like v1, v2....
	- best pratice to enabled Bucket
	- prior file treat as version null


Amazon S3 - Replication (CRR & SRR): Cross/same region replicas
	- must Enabled version first
	- copying is asyncronously
	- should have IAM permissions
	- Use Cases:
		- CRR - Compliance, lower Latency, replicas across account
		- SRR - log aggregation etc
	
Amazon S3 - Replication:
	- after enable replication, only new object replicates
	- For replication existing object used S3 batch replication
	- For Delete operation can replicate delete markers, deletion with version ID are not replicates (to avoid malicious deletes)
	- not support chaining of replication:
		- like 1 bucket to 2, and 2 to 3 then if we upload 1 then not come into the 3.

S3 Storage Classes:
	- Standard - General Purpose
	- Standard - Infrequent Access(IA)
	- One Zone - Infrequent Access
	- Glacier Instant Retrieval
	- Glacier Flexible Retrieval
	- Glacier Deep Archive
	- Intelligent Tiering
	
Note: S3 have lifecycle configuration using that you can move Automatically higher class to lower class

S3 Durability & Availability:
	- Durability:
		- high durability 99.9^11's using multi-AZ
		- Same for all the Classes
	- Availability:
		- varies depending on the class
		- for Retrieval take time in lower class


S3 Standard - General Purpose:
	- 99.99% Availability, used for frequently access, low latency, high throughput
	- use cases: Big Data analytics, mobile & gaming apps...

S3 Standard - Infrequent Access(IA):
	- less frequently, but rapid access when needed
	- Lower cost then Standard
	- 99.9% Availability, used as the backups
	
S3 One Zone - Infrequent Access:
	- 99.5% Availability, 99.9^11 durability in single-AZ, data loss if AZ is destroyed
	- Use cases: storing secondary backups

S3 Glacier storage:
	- Low-cost in archiving/Backup
	- Pricing : storage + Retrieval cost
	
	- S3 Glacier instant Retrieval:
		- milisecond Retrieval, great for data accessed once a quarter
		- minimum storage duration 90 days
	- S3 Glacier Flexible Retrieval:
		- Expedited (1-5 minutes), Standard(3-5 hr), Bulk(5-12 hr) - free
		- minimum storage duration 90 days
	- S3 Glacier Deep Archive:
		- Standard(12 hr), Bulk(48 hr)
		- minimum storage duration 180 days

S3 Intelligent Tiering:
	- Small monthly monitoring + auto-tiering free
	- moves objects one class to another Automatically
	- no Retrieval charge
	- ex: Standard to Infrequent (30 days) then archive (90 days) then deep archive (180 days) etc..
	
------------------------------------------------------------------------------------------------------------------
Date: 29/1/2024    ---> AWS CLI, SDK, IAM Roles & Policies <---

EC2 instance Metadata(IMDS):
	- AWS EC2 instance metadata(IMDS) very powerful
	- Using this you can get the Metadata of EC2 instance, without using IAM role
	- URL http://169.254.169.254/latest/meta-data, Retrieve IAM role name not Policies
	- Metadata = info EC2 instance, Userdata = launch script in EC2

IMDSv2 vs IMDSv1:
	- IMDSv1 : directly you can access the meta data by link
	- IMDSv2 : first get session token then in harders (-H) you need to pass the token then you can access the Metadata
	

AWS CLI Profile:
	- Used for handling the multiple aws profiles
	- aws configure --profile profile_name
	
AWS MFA with CLI:
	- MFA should enabled for your Account
	- you need the temporary credentials, So use STS GetSessionToken
	- aws sts get-session-token --serial-number arn-iam-user --token-code authy-code-here (give temp credentials)
	- Use these token and set in the configure file then used for access the aws (valid for 1hr or 1 day etc)

AWS SDK Overview:
	- SDK is used for performing aws task using your application directly
	- language supports: java, .NET, NodeJs, PHP, Python etc...

AWS Limits(Quotas):
	- API Rate Limits:
		- DescribeInstance : API EC2 has 100 call per second limited
		- GetObject : API S3 has 5500 GET per second per prefix
		- For Intermittent Errors: important Exponential Backoff, Or go for AWS support request to increase the limit
	
	- Service Quotas:
		- on-demand instance: 1152 vCPU max
		- for increase Service Quotas limit go for AWS support request to increase the limit 

Exponential Backoff (any AWS Service):
	- If ThrottlingException then mostly go for Exponential Backoff
	- In SDK already implemented but for other you need to manualy added
	- must implement when you use AWS API, and for only for 5xx type(server error) of error
	
AWS CLI Credential Provider Chain:
	- The CLI Credential Chain order:
		- command line options: --region, --profile etc
		- Environment variable: AWS_ACCESS_KEY, AWS_SECRET_ACCESS_KEY.. etc
		- CLI credential file : aws configure
		- CLI configuration file: aws configure
		- container credentials: for ECS tasks
		- Intance Profile credentials: for EC2 instance
	
	- The SDK Credential Chain order:
		- System Properties : aws.accesskeyId, secretKey
		- environment variable:	AWS_ACCESS_KEY, AWS_SECRET_ACCESS_KEY... etc
		- default credential profiles files: .aws/Credential etc
		- ECS container credentials: for ECS containers
		- Intance profile credentials: EC2 instance
	
AWS Credentials Best Practices:
	- never store credential in the code
	- best prectice to get from the credential chain
	- If possible use IAM Roles
	- outside aws use profile Credential


Signing AWS API Request:
	- When you call the AWS HTTP API, you sign the request so aws can verify its you, using AWS Credentials
	- If you used CLI or SDK, HTTPS requests are signed for you
	- Sign through signature v4 (SigV4)
	- sign request examples:
		- HTTP header option: (signature in authorization header)
		- Query string option: (S3 pre-sign url)

------------------------------------------------------------------------------------------------------------------
Date: 29/1/2024   ---> Advance AWS S3 <---

Amazon S3 - Moving b/w Storage classes:
	- Standard --> Standard IA --> Intelligent tiering --> One-Zone IA --> Glacier Intant Retrieval --> Flexible Retrieval--> Deep Archive
	- automated by life cycle rule
	
S3 life cycle Rules:
	- Transition Actions:
		- move one class to anoter base on time
	- Expiration actions:
		- configure action based on the expiration Data
		- e.g after 365 days, old versions, incomplted multi-part uploads etc
	- rule can be based on certain prefix, based on tags also

Amazon S3 analytics - Storage class analytsis:
	- Helps you when need to change the class
	- Create a report for recommendation, update daily by aws
	- does not work for one-zone IA and Glacier
	- after 24 to 48 hr you can start analysis
	- good to used with life cycle rule

S3 Event Notification:
	- for every action S3 have emmit a Event
	- Use case: generate thumbnails after every upload
	- take sec or minutes for action sometime
	- You can create as many event as you need
	- S3 to lambda, SNS, SQS and EventBridge etc, using event bridge can add multiple functionality
	- For sqs need to add the permission for get the notification
	
S3 - Baseline Performance:
	- latency 100-200 ms, very high request automatically
	- 3500 CRUD or 5500 GET/HEAD request per prefix etc..
	- not limit for prefix in S3
	- best Practice to use Prefix

S3 Performance:
	- Multi-Part Upload:
		- if more the 5GB used multi part Upload
		- used parallelize approach (speed up)
		- divide big file into part then upload

S3 transfer Acceleration:
	- Upload though the edge location, It will increse the upload Speed
	- compatible with multi part Upload
	
S3 Performance- for reading (S3 Byte-Range Fetches):
	- get file in parallelize using the Byte-Range (download all paralle same time)
	- download only partial data (only some xx byte data) for get perticular data

S3 Select & Glacier Select:
	- used for server side filtering directly though S3 for less Data
	- can filter row & col, (simple sqk statements)
	- help client site, less CPU used in client side
	
S3 User-defined Object Metadata & S3 Object Tags:
	- S3 User-defined Object Metadata:
		- upload time you can define the Metadata
		- Name-value (Key-value pair)
		- user-define data must start with "x-amz-meta-"
		- metadata Retrieve when Object Retrieve
		
	- S3 Object Tags:
		- Key-value for objects in S3
		- useful for grained permission time (tag based permission give)
	
	- You can not search object metadata or object Tags

------------------------------------------------------------------------------------------------------------------
Date: 30/1/2024   ---> Amazon S3 Security <---

Amazon S3 - Object Encryption:
	- 4 method of Encryption
	- Server Side Encryption(SSE)
		- SSE-S3 (Managed by AWS, Default): AES-256, x-amz-server-side-encryption : "AES-256"
		- SSE-KMS (Managed key by you) :  x-amz-server-side-encryption : "aws-kms"
			- limit 5500 per sec, limit varies based on region, (request to aws for increse)
		- SSE-C	(You can add your own key): CLI supported only
	- Client Side Encryption(SSE) (encrypt and upload)

Amazon S3 - Encryption in transit (SSL/TLS):
	- ssl/tls supported, used https for endpoint (encryped flight), http for vice-versa

Amazon S3 - force Encryption in transit:
	- used policy condition boot type, aws:SecureTransport: false

Amazon S3 - Default Encryption vs Bucket policies:
	- SSE-S3 default, Automatically etc..
	- through policy you can force encryption and refuse any api call to S3 if they don't have the kms in bucket

S3 Cors: (Cross-origin Resource Sharing)
	- Origion = Scheme (Protocol) + host (domain) + port
	- allow different origion to access or request any service

Amazon S3 - MFA Delete:
	- Version must Enabled
	- Only Root owner can Enabled/Disabled MFA Delete

S3 Access Logs:
	- For create log of bucket, any operation
	- always logged in another Bucket
	- data can analysis using anthena etc
	- target bucket must be in same region
	- Do not log target same bucket other-wise recusion (Exponential increse)

Amazon S3 - Pre-signed URL:
	- Generate presigned URLs through S3, sdk, CLI etc
	- set time 1 min to 12 hr, CLI limit more
	- Only allow logged-in user can download 
	
Amazon S3 - Access Points:
	- create complex bucket policy based on folder in S3.
	- Each access point have policy, DNS name
	- Also define through the VPC for more secure access

Amazon S3 Object lambda:
	- Using lambda function we can modify the object data before Retrieveing the client/caller app.
	- e.g. S3 bucket ---> S3 access point ---> Lambda function ---> S3 Access point --> client/caller

	- Use case:
		- redacting person info from te S3 data
		- converting XML to JSON
		- resizing & watermarking on img
	

------------------------------------------------------------------------------------------------------------------
Date: 31/1/2024   ---> Amazon Cloudfront <---

AWS Cloufront:
	- Content Delivery Network (CDN)
	- Improve read performance, content cache in edge location
	- improve user experience
	- 400+ edge location
	- DDoS protection, shield + aws web application firewall

Cloudfornt - Origins:
	- S3 Bucket:
		- for distribution + caching in edge location
		- Supported OAC (new & more secure, bucket private) and OAI
		- Cloudfront can used for S3 uplaod(multi part uplaod)
	
	- Custom Origion(HTTP):
		- ALB, EC2 instance, S3 website (must first enable the bucket as staic S3 web)
	
Cloudfront vs S3 Cross Region Replication:
	- Cloufront:
		- Global Edge location
		- cached for TTL (maybe Day)
		- Great for staic content
	- S3 Cross region Replication:
		- must setup for each Region for Replication
		- file upload very fast (near real time)
		- Read only
		- Great for dynamic content, low latency

Cloufront Caching:
	- cache available each cloudfront edge location
	- cache identify by using the "Cache Key"
	- want to cache more data so latency very low

Cache Key:
	- A unique Identifier
	- default consists using hostname + resource url
	- in cache key you can add headers, query, cookies etc (in Cloufront cache policy)
	
Cache Policy:
	- cache based on:
		- HTTP headers, cookies, query string --> allow or DENY
	- TTL 0 sec to 1 yr
	- cache key automatically included in origin request
	
Cloudfront Policies - Origin Request Policy:
	- you can add values in the origin request directly
	- through cloudfront to origin you can add any values in the http headers, cookies, quiers etc

Cache Policy vs origin Request Policy:
	- Cache key is used for caching the data for client based on cache key
	- origin request Policies are used for add values for whitelisting things

Cloudfornt - Cache Invalidations:
	- use /* for informed the edge location that we have updated something 
	- Invalidation used to update the cache edge location

Cloudfront - cache Behaviors:
	- Configure different settings for URL pattern
	- e.g. /img/*, /api/*
	- route to different kind of origin based on path pattern

Cloudfront - ALB or EC2 as an origin:
	- Client --> Edge location --> allow public IP --> Security group --> EC2 instances(must be public)
	
	- Client --> Edge location -(allow public IP)-> security group(ALB) --> security Group --> EC2 instance(can be provate)
	
Cloudfront Geo Restriction:
	- allow/deny based on geo location (country)
	- contry determined using a 3rd party Geo-IP Database
	
Cloudfront Signed URL / Signed cookies:
	- used for distribute paid content to user
	- valid for TTL Time
	- Signed URL: access to individual file
	- Signed cookies: access to multiple files

Cloudfront Signed URL vs S3 Per-signed URL:
	- Cloudfront Signed URL:
		- allow access to any origin (ALB, S3.. etc)
		- have group for encryped the transfer the file
		- have cache feature
	- S3 Per-signed URL:
		- Uses the IAM key of the signing IAM Principal
		- TTL Available

CloudFront Signed URL Process:
	- Two types of signers:
		- using Trusted Group (REcommanded)	
		- Using AWS root account cloud front key pair
			- not REcommanded, managed key by root
	- You can create multiple trusted key Groups
	- you can generate your own pulic / private key
	- RSA - 2048 bit (private - public key)
	- public key in Cloudfront key group

Cloudfront - pricing:
	- Cloufront edge location are all around the world
	- cost veries based on edge Locations
	- cost reduction based on the class:
		- for class all: best Performance
		- class 200: most region, removed the expensive Region
		- class 100: only least expensive region

CloudFront - multiple Origin:
	- To route different origi based on content type
	- bsed on path, /img/*, /api/* etc, based on cache Behavior

CloudFront - origin Groups:
	- To increse high-Availability
	- set origin group, Primary origin, secondary origin
	- If primary failed the go for second origin, (S3 bucket or EC2 instance as origin)

CloudFront - Field Level Encryption:
	- Protect user sensitive information
	- add aditional layer of security with HTTPS
	- sensitive info encryped, asymmetric worked
	- on the edge location we encryped the sensitive info like credit card number etc, then origion decrtpt and used for response
	
Cloudfront - real time:
	- cloudfront sent data in real time to Kinesis data streams
	- monitor, analyze and take actions based on CDN

------------------------------------------------------------------------------------------------------------------
Date: 1/2/2024  --> ECS, ECR & fargate: Docker in AWS <--

Docker introduction: What is Docker
	- It is Software Development platfrom to deploy apps
	- apps are packages in containers that can run any OS
	- any machine, no compatibility issue, less work, predictable behavior, easier to maintain & deploy etc
	- Use case: microService architecture, lift & shift apps in aws cloud..
	
Docker On an OS:
	- Server(EC2) inside run containers like java container, node container etc
	- Docker images can store in docker repositories
	- Docker Hub, Amazon ECR (private, public)

Docker versus virtual Machines:
	- Docker is sort of VM, but not exactly
	- Worked on the docker demaon on EC2 instance 

Docker Container Management on AWS:
	- Amazon ECS (elstic container service): aws's own container platfrom
	- Amazon EKS (Eastic Kubernetes Service): aws managed, oper source
	- AWS Fargate: aws's own, Serverless containers
	- Amazon ECR (Elastic container Registry): store imgs

Amazon ECS - EC2 lunch type:
	- aws docker conatiner = launch ECS tasks on ECS clusters
	- EC2 launch type: must provision & maintain by you
	- Each EC2 intance must have ECS againt to add/registor the ECS Cluster
	- AWS take care of starting & stopping container

Amazon ECS - Fargate Lunch Type:
	- managed by AWS, need to define the infrastruture (EC2 instant not needed)
	- You need to create task defination
	- automatically allcated CPU/RAM
	
Amazon ECS - IAM Roles for ECS:
	- EC2 instance Profile:
		- Used by the ECS agent
		- Makes calls by ECS, send logs to CloudWatch, Pull docker image from ECR
		- get data from SM or SSM parameter Store
		
	- ECS task Role:
		- each task have specific role
		- use different roles for different ECS service run
		- Task role is define in task defination

Amazon ECS - Load Balancer Integrations:
	- ALB most used
	- NLB only recommanded for high Performance and aws private link
	- Classic Load Balancer supported but not recommend


Amazon ECS - Data Volumes (EFS):
	- Mount EFS with ECS tasks
	- Worked with both EC2 & forgate launch type
	- tasks running any AZ will share the same data in EFS
	- Fargate + EFS = Serverless
	- Use Cases: supported Multi-AZ share storage for container
	- S3 cannot worked with file system

ECS Service Auto Scaling:
	- automatically increase/decrease the ECS tasks
	- ECS auto scaling uses AWS application auto scaling
		- based on CPU utilization
		- based on Memory utilization
		- based on ALB request count per target
	- Target Tracking: scale based on target value, cloudwatch help in this
	- step scaling : scale based on CloudWatch alarm
	- Schedule scaling: scale based on time range
	- ECS service scaling != EC2 auto scaling
	- Fargate auto scaling is much easier to setup


EC2 Launch Type - auto Scaling EC2 Intance:
	- auto scaling group scaling:
		- ASG based on CPU
		- add EC2 
	- ECS Cluster capacity Provider:
		- used to scale ECS tasks
		- used Auto Scaling group
		- add EC2 based on CPU, RAM

ECS Rolling updates:
	- When updating v1 to v2, control any task and order also
	- min 50%, max 100%, so task min 2 and max 4 at a time

Amazon ECS - Task Definations:
	- JSON form for ECS to run container
	- it containers info like:
		- Image name, memory & CPU size, environment variable
		- networking info, IAM role, logs etc
	- we can define 10 container as per task defination

Amazon ECS - Load Balancing (EC2 Launch type):
	- Dynamic host port mapping supported ALB if you only define the task defination 
	- ALB managed automatically
	- Must allow EC2 instance's security any port from ALB SG.
	
Amazon ECS - Load Balancing (Fargate):
	- unique Private IP for task
	- Used ECS ENI SG for port 80 ALB

Amazon ECS - One IAM role per task defination:
	- Task defination + ECS task Role
	- define task role in your task defination so any new service create with that role

Amazon ECS - Env Valirable:
	- Hardcoded, SSM Paramerte stpre, secrets Manager
	- Env files (bulk) - Amazon S3
	
Amazon ECS - Data Volumes (Bind Mounts):
	- share data b/w the containers
	- works for both EC2 & fargate tasks
	- EC2 used instance storage 
	- fargate use 20GB to 200GB of Ephemeral Storage
	- use cases:
		- share data b/w container 
		- sidecar container pattern, sidecar use for log sending

ECS Tasks Placement:
	- It is only for EC2 not for fargate
	- It determine wher to place it in the container, CPU, Memory & available port etc
	- Also figureout which task need to terminate
	- have Task placement strategy & task placement containers
	
ECS task Placement Process:
	- ECS places task for that container process:
		- check CPU, memory, port requirement etc
		- check containers, check able to satisfy the task etc.


ECS Task Placement Strategies:
	- Binpack : cost saving, based on CPU uses (Try to fill first container then go for next)
	- Random : randamly
	- Spread : evenly spread, based on Availability zones
	- You can use the mix also using these 3
	
ECS Task Placement Constraints:
	- DistrintInstance: place each task in different container 
	- memberOf: place task using expression
		- used cluster query Language

Amazon ECR:
	- store docker image, public & private
	- integrated with ECS, backed by S3
	- Login Command : AWS cli v2
	- Docker commands: Push and Pull
	- For all command you need IAM permission

AWS Copilot:
	- CLI tool to build, release & production ready containerized apps
	- using this run apps on AppRunner, ECS & Fargate
	- helps for focus on code not on the infrastruture
	- have pipelines Also, deploy multiple env Also
	- help in troubleshooting, logs, health check etc


AWS EKS:
	- launch managed Kubernetes clusters on AWS
	- open source, scaling & management of containerized (using docker) app
	- alternative of ECS
	- EKS supports EC2 & Fargate to deploy etc
	- Use case: easily migrate the kubernetes to aws EKS
	- Kubernetes is cloud-agnostic (use any cloud)

Amazon EKS - Node Types:
	- Managed Node Groups:
		- Create & managed nodes(EC2) for you
		- Nodes are part of ASG managed by EKS
		- Supported on-demand or spot Instances
	- Self-Managed Nodes:
		- Node created by you and registerd to EKS Cluster & managed by ASG
		- prebuild AMI can use
		- Supported on-demand or spot Instances
	- AWS Fargate:
		- No maintenance, no nodes managed

Amazon EKS - Data volumes:
	- need to specify Storage EKS Cluster
	- Container Storage Interface (CSI) compliant driver
	- supported for: EBS, EFS, FSx for Lustre, NetApp etc


------------------------------------------------------------------------------------------------------------------
Date : 2/2/2024   ---> AWS Elastic Beanstalk <---

Developer Problem on AWS:
	- Managing infrastruture
	- Deploy code
	- Configure all the databases, loadbalancer etc.
	- scaling concerns
	- Most web apps have same architecture (ALB+ASG)
	- all Developer want their to code run with every env etc

Elastic Beanstalk - Overview:
	- Beanstalk solve mostly all problems
	- it uses all components like EC2, ASG, ELB RDS etc
	- Managed by aws: all + monitoring intance configuration etc
	- also give the full control over Configuration
	- Beanstalk is free but for underuse service need to pay
	
Elastic Beanstalk - components:
	- Application: env, version, configuration
	- Application version: Application code
	- Environment: multiple env supported, web server + worker env supported
	- flow:
		- Create application --> upload version --> Launch env --> Manager env --> then step 2 (upload)
	- Lang: all lang + docker container, multi docker etc


Web Server tier vs Worker Tier:
	- web env are same like ELB to ASG and then instance
	- Worker env first SQS queue to ASG then instance

BeanStalk Deployment Oprions for Updates:
	- All at once: fastest, downtime, no additional cost
	- Rolling: half-half update, half update then next half, sometime under Capacity, no additional cost, long time take
	- Rolling with additional batches: like rolling but extra intsance, Good for prod, longer deployment, additional cost
	- Immutable: New instance with new ASG, Then used swap, 0 downtime, High cost, longest time, quick roleback great for prod
	- Blue Green: Create a new environment and switch, not direct to beanstalk bcoz through the Route53, 0 downtime, setup the weight through route 53 for test	
	- traffic splitting: canary testing - first 5% then 100%, automatically rollback(very quick) 


Elastic Beanstalk CLI:
	- Install CLI called "EB CLI"
	- Basic commands: 
		- eb create, status, health, events, Logs
		- eb open, Deploy, config, terminate etc

Beanstalk lifecycle policy:
	- store more then 1000 app version
	- for new version deploy need to remove old version
	- you can use lifecycle policy for old version also send S3 for prevent 

Elastic Beanstalk Extensions:
	- zip file need deploy on Elastic Beanstalk
	- .ebextensions/  should be in root directry
	- YAML / JSON format
	- .config prefix file inside the .ebextensions/ folder
	- once .ebextensions/ deleted you all env deleted
	
Elastic Beanstalk Under the hood:
	- Elastic Beanstalk relies on cloudformation
	- use case: You can define cloudformation resource in you .ebextensions/ files for any resource like S3, ElastiCache etc


Elastic Beanstalk Cloning:
	- clone an env with extra configuration
	- useful for deploy test Env
	- all resource & configuration are preserved
	
Elastic Beanstalk Migration - Load Balancer:
	- During the first creation Beanstalk you need to select the load Balancer after that you can only change the setting not the LB
	- So for that You can use Migrate option:
		- Create new env without load Balancer (can't use clone bcoz LB also copy)
		- deploy you app onto new env 
	
RDS with Elastic Beanstalk:
	- RDS can be provisioned with Beanstalk, great for dev/test
	- not for prod, for prod seperate the RDS from EB app and add by connection string (Decuple functionality)
	
------------------------------------------------------------------------------------------------------------------
Date : 2/3/2024   ---> AWS cloudformation <---

Amazon Cloudformation - infrastruture as Code:
	- need to do all manual work
	- if anything delete or need to change the region or aws account etc. So that is very nightmare 
	- For solving this issue we used cloudformation

What is cloudformation:
	- Using cloudformation you need to just declare all the resource, then all thing created by CF
	- Using CF:
		- declare security Group
		- EC2 machine with SG
		- S3 Bucket etc..
	- Cloudformation create for you, in right order with same declared configuration
	
Benifits of Cloudformation:
	- infrastruture as code:
		- no manual worked needed
		- code can be version using GIT
		- Changes can reviewed through the code
		
	- Cost
		- Each resource declare in template so easy to estimate
		- saving strategy:
			- In Dev, just delete after 5PM and create 8AM safely etc..
			
	- Productivity:
		- ability to create & delete infrastruture
		- automated generation templates
		- Declartive programming (no need to check order etc..)
		
	- Separation of Concern: (many stack supported)
		- VPC Stack
		- Network stacks
		- App stacks
	
	- Don't re-invent the wheel
		- Leverage templates
		- have documentation 

How cloudformation Works:
	- templates need to upload in S3 then referenced in cloudformation
	- you need to upload every time template
	- stack are identified by Name
	- when delete stack, all Resource also deleted

Deploying CloudFormation templates:
	- Manual way:
		- edit template in the cloformation design, then deploy using console
	- Automated way:
		- edit templetes in YMAL file
		- using CLI deploye the templates
		- recommanded way 

CloudFormation Building Blocks:
	- Templates Components:
		- Resources: services declated (Mandatroy only)
		- Parameters: dynamic inputs for Templates
		- Mapping: static variables for your Templates
		- Outputs: references what you Created
		- Conditions: List of condition for Resource creation
		- metadata
	
	- Templates helpers:
		- Refereces
		- Functions
		
YAML Crash Course:
	- YAML & JSON use for write templates
	- JSON is horrible for CF
	- YAML is greate for CF
	- key valve (:), array (-), multi-line support (|)

What are resources:
	- It is Mandatroy
	- using this you can declare the resouces/Service
	- 224 types of Resources
	- AWS::aws-product-name::data-type-Name

Node: 
	- You can not create dynamic amount of resource, you need to declare first in templates
	- almost all services supported 

Parameters:
	- if configuration parameter change then in parameter
	- not need to redeply for changing the content

Reference a Parameter:
	- through fn::ref you can get the Refereces id of parameter
	- Parameters can use any where using the ref
	- shorthand YAML !Ref

Concept: Pseudo Parameters	
	- aws offers some reserve keywords
	- e.g: AWS::AccountId, NotificationARNs, Region, StackId, StackName etc
	
Mapping: 
	- fixed valirale in templates, hard coded in template
	- used for differentiante b/w env dev, prod etc
	
mapping vs Parameters:
	- Mappings are great when you know the values that can use in resource like region, AZ, AWS account, ENV etc, allow to control template
	- Use parameters When the values are really user specific

Fn::FindInMap accessing mapping values:
	- Fn::FindInMap return value of specific key
	- !FindInMap [ MapName, TopLevelKey, SecondLevelKey ]

Output:
	- output values can import into other stacks
	- can view the output in CLI & console
	- very useful if you use different stacks like network, VPC IC, etc
	- using perform cross stack collaboration
	- you can't delete CF if outputs are being referanced by another CF stack
	
Cross Stack Reference:
	- First need to Export 
	- For import use !ImportValue Export_key_name
	
Conditions:
	- use for control the cretion of resources or output
	- any condition like: 
		- based on Env, AWS region, any values etc

How to Define condition:
	- Condition:
		- CreateProdResource: !Equals [ !Ref EvntType, prod ] 
	- !And, !Equals, !If, !Not, !Or etc.

CloudFormation Most Know Intrisic Functions:
	- !Ref: return parameter value, resource ID
	- !GetAtt: get any attribute from resource
	- !FindInMap: return the matched value from the template
	- !ImportValue: export value can import
	- !Join: Can join the values, !join[":", [a,b]]
	- !Sub: used for substitute variables from text, or ${variableName}
	- condition(!And) ones: for checking the conditions
	
CloudFormation Rollback:
	- Stack Creation Fails
		- default rolls back (get deleted all)
		- option to disabled also
	- Stack Update Fails:
		- The stack Automatically rollback
		- log Available 

Cloudformation Stack notification:
	- Send stack event to SNS topic (Fail/pass etc)
	- Enable SNS using stack options
	
ChangeSets:
	- When update a stack, that time you can check before the change what are the changes.
	- It just show the in info about the changes
	- not success or failer info

Nested Stacks:
	- you can create parts of stacks
	- e.g. LB configuration stack can use etc
	- Nested stack are considered best Practice
	- root stack update always, when part update
	
Cross vs Nested Stack:
	- Cross stack :
		- when stack are different Lifecycle
		- Export and InportValue Used
		- When values need in many stack
	
	- Nested Stack:
		- used when components must re-used
		- e.g. re-use ALB 
		- nested stack only used in higher level stack

StackSets:
	- Multiple account & region stack can perform CRUD with single Option
	- Administrator account can Create
	- all stack update using this
	
CF Drift:
	- cloudformation allow you to create infrastruture
	- but not protect you from manual changes
	- for detecting those you can used Drift
	
CF Stack policies:
	- Usig stack policies you can allow or deny the specific resource update
	- Protect resource from unintentional Updates

------------------------------------------------------------------------------------------------------------------
Date : 2/4/2024   ---> AWS Integration & Messaging: SQS, SNS & Kinesis <---
	
AWS Integration & Messaging - Sestion Introduction:
	- Application need to communicate to each other
	- 2 pattern we use in communication
		- Synchronous communications (App to App)
		- Asynchronous / Event based (App to Queue to App)
	- Synchronous may be problematic if suddenly get so much traffic then, e.g. 1000 video's usually 10
	- For solving use "Decouple" app functionality
		- SQS: Queue model
		- SNS: pub/sub model
		- Kinesis: real-time streaming model
	- These service can scale automatically/independently
	
Amazon SQS:
	- Producer --(send message)--> SQS Queue --(pull message)--> Consumer
	- Oldest more 10 then yrs
	- fully managed, used decuple applications
	- Attributes:
		- Unlimited throughput, unlimited message in queue
		- defalt 4 days, max 14 days
		- low Latency
		- Limitation 256KB
	- duplicates possible, Work on at least once Delivery
	- out of ordering (best effort ordering)

SQS - Producing messages:
	- produced to sqs using SDK (sendMsgAPI)
	- Persisted message in sqs until a consumer deletes It
	- defalt 4 days, max 14 days
	- e.g. processed : order id, Customer id any attributes etc
	- SQS standard unlimited throughput
	
SQS - Consuming Messages:
	- Consumers (EC2, servers, AWS lambda etc)
	- Poll SQS for messages (recieve upto 10 msg at a time)
	- process message (e.g. interst the msg into rds DB)
	- Delete msg using Delete API
	
SQS - multiple EC2 Intance consumers:
	- consumers recieve & process msg in paralle
	- at least once Delivery
	- best-effort message ordering
	- scale consumers horizontally 

SQS with Auto Scaling Group (ASG):
	- From SQS poll msg to ASG which is connected to EC2 instances
	- We can scale Instances through cloudwatch alarm for that need to set cloudwatch matrix on sqs so if max load then it trigger CloudWatch alarm and alarm increse intances using ASG. 

SQS to Decuples b/w application tiers: (Flow)
	- request --> ASG(frontend web app) --> send messages --> SQS queue --> Receive Message --> ASG(Backend processing) --> Insert DB etc

SQS - Security:
	- Encryption:
		- in-flight using HTTPS API
		- At-rest using KMS
		- Client side
	- Access Controls:	IAM policies for access SQS API
	- SQS Access points: (similar to S3 bucket Policies)
		- Cross-account access to SQS 
		- allowing other services (SNS, S3) to write 

SQS queue access policy:
	- Cross Account Access
	- Publish S3 Event Notifications to SQS Queue

SQS - Message Visibility Timeout:
	- When one user polled by consumer, it becomes invisible to other consumers
	- Default time 30 second "msg Visibility timeout", max 12 hr
	- So if one user pull msg then other use can not get the msg till 30 sec or user don't deleted the msg
	- ChangeMessageVisibility API for increse time
	
SQS - Dead Letter Queue:
	- If user not process msg with in MVT then goes into sqs queue
	- set a Threshold for recieving msg again and again
	- after maximum Receives Threshold, msg goes into DLQ
	- usful for debugging
	
SQS DLQ - redrive to source:
	- Help users to understand DLQ message, 
	- when code fixed, you can redrive the msg from DLQ to queue
	
SQS - Delay Queue:
	- Delay a msg (don't immediately get msg) within 15 minuter
	- default 0 sec
	- SelaySec you need to set
	
SQS - Long Polling:
	- when poll the msg that time the wait for gettin msg is knows as long Polling
	- LongPolling decreses the no of API calls made to SQS, it incresing the effciency and decreasing the latency of application
	- wait b/w 1 to 20 sec
	- RecieveMessageWaitTimeSeconds API call for increse second

SQS extended Client:
	- msg size limit 256kb, for sending 1GB Data
	- using SQS Extended Client (JAVA Library)
	
SQS - Must know API:
	- CreateQueue (MessageRetentionPeriod), DeleteQueue
	- PurgeQueue : delete all msgs
	- SendMessage (DelaySeconds), RecieveMessage, DeleteMessage
	- MazNumberOfMessages: default 1, max 10
	- RecieveMessageWaitTimeSeconds: Long polling
	- changeMessageVisibility: change msg time out
	- batch APIs sendMessage, DeleteMessage, ChangeMessageVisibility
	
SQS - Fifo Queue:
	- FIFO: First in First Out(ordering of msgs in the queue)
	- Limited throughput : 300 msg/s without batch, 3000 msg/s with
	- Exactly-once send capability (removing duplicates)
	- Message processed in order

SQS Fifo - Deduplication:
	- De-duplication interval 5 min
	- Two De-duplication methods:
		- sha-256 hash
		- provide a Deduplication id
		
SQS FIFO - Message Grouping:
	- You can sent group data in using the MessageGroupID in Fifo 


Amazon SNS:
	- For sending msg to mutiple user same Time
	- Pub/sub model
	- for direct integration service you need to manage the ASG etc
	
	- event producer sends msg to one SNS topic
	- event Receiver are SNS subscriber
	- Each subscriber get all the msg (you can apply filter)
	- up to 12,500,000 subscriber per topic
	- 100,000 topics limit
	
SNS - How to Publish
	- Topic Publish (Using SDK)
		- Create Topic
		- create subscription
		- publish to the Topic
	- Direct Publish (for Mobile Apps SDK)
		- create app
		- create Endpoint
		- publish Endpoint
		- works wit GCM, Apple, ADM
		
SNS - Security:
	- Encryption:
		- in-flight using HTTPS API
		- At-rest using KMS
		- Client side
	- Access Controls:	IAM policies for access SNS API
	- SNS Access points: (similar to S3 bucket Policies)
		- Cross-account access to SNS 
		- allowing other services (SNS, S3) to write

SNS + SQS - Fan out:
	- Push one SNS, recieve all SQS queue as subscriber
	- Make sure sqs queue policy all sns msg
	- fully decoupled, no data loss
	- Cross-Region Delivery: works
	
Application: S3 Event to multiple queues
	- for S3 event we can utilize this Fan out Model
	- send S3 event Notification to SNS to sqs or lammbda etc
	
Application: SNS to Amazon S3 through Kinesis Data Firehose
	- SNS can send to Kinesis
	- sns to Kinesis Firehose to S3 or any KDF destination
	
SNS - FIFO Topic:
	- ordering msgs in the Topic
	- similar to SQS FIFO, Ordering MessageGroupID, De-duplication ID supported
	- Limited ThroughPut (Same as SQS FIFO)
	
SNS - Message Filtering:
	- JSON Policy used to filter msgs for SNS topics
	- if subscription not apply filter policy then recieve every msg

Kinesis Overview:
	- Makes it easy to collect, Process, analyze streaming data in real time
	- real-time Data like: Application logs, Metircs, website click streams etc
	- 4 types:
		- Kinesis Data Streams: capture, process, store data stream
		- Kinesis Data Firehose: load data streams into AWS data store 
		- Kinesis Data Analytics: analyze data streams using SQL, Apache Flink
		- Kinesis Video Streams: capture, process, store video streams
	
	
Kinesis Data Streams:
	- Shards : it is process the data, speed 2 MB/Sec per shard for all Consumers, enhance to per Consumers
	- retention b/w 1 to 365 days
	- ability to reprocess Data
	- once inserted in kinesis can't deleted
	- data partition goes into same shard
	- Ptoducers: AWS SDK,Kinesis agent etc
	- Consumers: AWS SDK, lambda, KDF, KDA
	
Kinesis Data Streams - Capacity Modes:
	- Provisioned Mode: 
		- choose no of shard, scale manually using API
		- Each shard get 1MB/s (1000 records per second)
		- Each shard gets 2MB/s out
		- pay per shard provisioned per hr
	
	- On-demand Mode:
		- No need to provision or manage the capacity
		- Default capacity (4MB/s or 4000 records per second)
		- Scales automatically
		- pay per stream per hr & data i/out per GB
	
Kinesis Data Streams Security:
	- Control Access using IAM
	- Encryption:
		- in-flight using HTTPS API
		- At-rest using KMS
		- Client side 
	- VPC Endpoint available
	- monitor API calls using CloudTrail

Kinesis Producers:
	- puts data into data Streams
	- data consists of:
		- Sequence number (Unique per partition-key shard)
		- partition key
		- Data blob
	- Producers:
		- AWS SDK
		- Kinesis Producer Library(KPL): C++, java, compersion etc
		- Kinesis agent
	
	- write throughput 1MB/s or 1000 records/sec shard
	- PutRecord API
	- Using batching with PutRecords API reduce costs & increse throughput
	
Kinesis Producers:
	- Using Hash Function it will send the partition key into the same shard 
	- DeviceId == partitionKey should be unique, It help to hash funciton to send data in different-2 shard, also reduce the load on shard
	- If you common partition key then get error, "ProvisionThroughPutExceeded", so for this use Exponential Backoff

Kinesis Data Streams Consumers:
	- get data from data streams and process them:
		- AWS lambda
		- KDA
		- KDF
		- Custom Consumer (AWS SDK) - classic or Enhanced Fan-out
		- KCL (client library)
	
Kinesis Consumers - Custom Consumer:
	- Shared(Classic) Fan-out consumers
		- Pull Model, every shard can give only 2MB/s
		- If more consumer for that shard then speed devided
		- Max 5 getRecords API calls, less costly, till 10 MB data get
		- latency ~200ms
	Enhanced Fan-out Consumer:
		- Each consumer get same amount of speed 2MB/s
		- Push Model, every shard can give only 2MB/s per consumer
		- latency ~70ms, Higher cost, soft limit 5 consumer (default, you can increse by request to aws)

Kinesis Client Library (KCL):
	- A java library that helps read record from a kinesis Data Stream with distributed applications sharing the read workload
	- Each shard have only one KCL, e.g 4 shard = 4 KCL instance
	- Progress is checkpointed into DynamoDB (Need IAM access)
	- KCL can run on EC2, Elastic Beanstalk & on-Premises
	- version:
		- KCL 1.x shared consumer
		- KCL 2.x Enhanced Fan-out consumer
	- Shard >= KCL always

Kinesis Operation - Shard Splitting:
	- Used to increse the stream capacity (1MB/s data per shard)
	- divide a "hot shard"
	- old shard deleted once it expired
	- No automatic scaling, Manually
	- can't split more then 1 at a time
	
Kinesis Operation - Merging Shards :
	- Decrease the Stream Capacity & save cost
	- used to group two shards, based on clod shards(low traffic)
	- old shard deleted once it expired
	- can't merge more than two shard at a time
	
	
Kinesis Data Firehose:
	- get records data from many source then use in kinesis data firehose then batch write in aws destination
	- Fully managed service, no Administrator, automatic scaling, Serverless
	- Destination:	
		- AWS: Readshift, S3, opensearch
		- 3rd party: Splunk, MongoDB, DataDog, etc
		- Custom: send to any HTTP endpoint
	- pay per use
	- near real time
		- 60 sec delay or 1 MB of data send
	- supported mand data formates, conversions, transformatio, etc.
	- supported custom data transformation using Lambda
	- can send faild/all data to backup S3

Kinesis Data Stream vs Firehose:
	- Kinesis Data Stream:
		- stream service, real time(~200ms)
		- Write custom code (Producer/consumer)
		- managed scaling (shard splitting/merging)
		- Data storage for 1 to 365 days
		- supported reply capability
	- Firehose:
		- Full managed, Near real-time(buffer 60 sec or 1MB delay)
		- automatically scaling, no data storage
		- load streaming data into S3, redshift,3rd party etc
		- doesn't supported replay capability 

Kinesis Data Analytics for SQL appliaction:
	- Using KDS & KDF used as source then process KDA for SQL applicatios then for destination you can use new KDS & KDF through other services like lambda, S3 etc.
	- Real Time analytics on KDS & KDF using SQL
	- Add reference data from S3 to stream Data
	- fully manaaged, no servers to provision
	- Automatic scaling, pay per use
	- Output: 
		- KDS: create streams out of the real-time analytics
		- KDF: send analytics query results to destinations
	- Use cases: 
		- Time-series analytics
		- Real-time dashboards
		- real-time metrics
		
Kinesis Data Analytics for Apache Flink:
	- Use Flink(java, sql) to process & analyze streaming Data
	- Run Apache Flink app to managed cluster
		- Automatic Scaling, parallel computation
		- application backups
		- Flink does not read from Firehose

SQS vs SNS vs Kinesis:
	- SQS
		- pull Data
		- data delete after being consumed
		- can have many workers
		- no need to provision throughput
		- Ordering in FIFO
		- individual message delay
	- SNS
		- pub/sub model
		- Push data to many subscribers
		- up to 12.5 million subscriber per Topic
		- Data is not Persisted
		- upto 1 lac topics
		- no need to provision throughput
		- can combine with SQS
	- Kinesis
		- Standard: Pull data, 2MB per Shard
		- Enhanced fan out: push Data, 2MB per shard per Consumer
		- possibility to reply Data
		- real time Analytics
		- ordering at the shard level
		- data expire after X days(1 to 365)
		- both mode provisioned & on-demand



------------------------------------------------------------------------------------------------------------------
Date : 2/10/2024   ---> AWS Monitoring & Audit: CloudWatch, X-Ray, CloudTrail <---

Why Monitoring is important:
	- For checking application latency
	- for application outages: experience should be Good
	- troubleshooting & remediation
	- Bassically before the customer we want to find the issue so we can resolve and give good user experience
	
Monitoring in AWS:
	- AWS Cloudwatch:
		- Metrics: collect & track key metrics
		- Logs: collect, monitor, analyze & store logs Data
		- Event: sent Notifications based on event
		- Alarms: React in real-time to matrics/events
	
	- AWS X-Ray:	
		- troubleshooting appliaction performance & errors
		- distributed tracing of microService
	
	- AWS CloudTrail:
		- Internal monitoring of API calls
		- Audit change of AWS resources by your users


AWS Cloudwatch Metrics:
	- for every service, belong to namespace
	- matric monitor CPU utilization, Network etc.
	- Dimension are attribute (intance id, environment etc), 30 Dimension per Metircs supported
	- metrics have timestams

EC2 Details monitoring:
	- EC2 metrics have default "every 5 minutes"
	- with details monitoring (with cost), get every 1 minutes max
	- for faster ASG used detail monitoring
	- upto 10 Metrics free tier

Cloudwatch Custom Metircs:
	- possible to define your own Metrics, e.g. RAM, disk space, no of users logs
	- PutMetricData API call for store Data
	- StorageResolution API parameter - two possible value
		- Standard: 1 min
		- High Resolution: 1/5/10/30 second
	- make sure to cofigure your time correctly to the instance

CloudWatch Logs:
	- log groups: arbitrary name, usually represent app.
	- log stream: perticular instance logs/container etc
	- define your log expiration (never to 1 days..)
	- logs can send logs data to aws services like:
		- S3, kinesis data streams, KDF, lambda, opensearch etc
	- logs encryped by default
	- can Supported KMS-based Encryption also


CloudWatch Logs - Sources:
	- SDK, CloudWatch logs Agent, CloudWatch Unified Agent 
	- Beanstalk, ECS, Lambda, VPC, API Gateway, Cloudtrails, route 53 etc

CloudWatch Logs Insights:
	- for logs insights you can use Query command for gettting the query data
	- you can search & analyze logs Data
	- also give many example for help
	
CloudWatch Logs - S3 Exports:
	- take upto 12 hr, API call CreateExportTask
	- not near-real time or real-time... for realtime used subscription

CloudWatch Logs Subscriptions:
	- get Real-time logs event data
	- send to KDS, KDF, or lambda in realtime
	- also supported "Subscription Filter" for getting useful Data
	- cloudwatch logs arrgregation Support multi-account & multi region
	
Cloudwatch Agent & Cloudwatch logs Agent:
	- Cloudwatch logs for EC2:
		- by default, no logs for EC2 machine in Cloudwatch
		- you need to run cloudwatch agent on EC2 to push logs files
		- IAM permission needed 
		- cloudwatch log agent can be on-premises
	
CloudWatch Logs Agent & Unified Agent: 
	- both used for virtual services (EC2, on-premises...)
	
	- CloudWatch Logs Agent:
		- Old version, can send data to Cloudwatch
	- Cloudwatch Unified Agant:	
		- collect addtional info like RAM, Process, Disk, CPU, netstat etc
		- Collect logs & send cloudwatch
		- certralized Configuration using SSM Parameter store

CloudWatch Logs Metric Filter:
	- Cloudwatch logs can filter expressions
	- filter work after its creation, not filter previous data 

Cloudwatch Alarms:
	- alarm used to trigger Notification for any Metrics
	- various option (%, max, min etc)
	- Alarm states: OK, INSUFFICIENT_DATA, Alarm
	- Period: time in sec, 10 sec to 60 multiple

Cloudwatch Alarm Targets:
	- Stop, Termiante, Reboot, or Recover an EC2 Intance
	- Trigger Auto Scalling action
	- send notification to SNS, ASG etc

Cloudwatch Alarms - Composite Alarms:
	- CloudWatch Alarm for on a single metirc
	- Composite alarm are monitoring multiple other alarms using AND and Or Conditions
	- helpful to reduce alarm noise by creating complex composite alarms

Cloudwatch Alarm: Good to know
	- Alarm can be created based on Cloudwatch logs metics Filter
	- you can test the alarm using CLI
		- AWS cloudwatch set-alarm-state --alarm-name "" --state-value "" --state-reason ""

Cloudwatch Synthetics Canary:
	- configurable script that monitor your APIs, URLs, Websites...
	- try to reproduce what customer do programmatically, to find any issue
	- integrate with alarm, script can write in nodejs, python
	- can run once or regular schedule based

Cloudwatch Synthetics Canary Blueprints:
	- Heartbeat Monitor: load URL
	- API canary: test APIs
	- Broken Link Checker: check all links
	- Visual monitoring: compare SS during the run
	- Canary Recorder: recode you actions also
	- GUI workflow Builder: verifies the action can be taken on your webpages

Amazon EventBridge:
	- Schedule: Cron jobs, e.g. trigger lambda
	- Event Pattern: Event rules to react on service, e.g. root login sent event to SNS for email
	- trigger lambda function, send SQS/SNS etc

Amazon EventBridge Rules:
	- like a event bus, also can connect with 3rd party event bus like Zendesk, DataDog etc

Amazon EventBridge - Schema Registry:
	- EventBridge can analyze the events and infer the Schema
	- Schema Registry allows you to generate code for application, to know in advance how data is Structured
	- Schema can versioned
	- Also supported multi-account aggregation
	
 
AWS X-Ray:
	Why we need:
		- debugging in Production, the good old way:
			- test locally, add logs everywhere, re-deploy in prod
		- through logs get solution hard
		- distribution service getting errot hard
		- no common view of your entire archicture
	- For all the problem we have solution AWS X-Ray
	
AWS X-Ray - Visual analysis of our App:
	- you can check visully ini which service you are getting error
	
AWS X-Ray advantages:
	- troubleshooting Performance (bottlenecks)
	- understand the dependencies in microservice architecture
	- Pinpoint service issues
	- review request behavior
	- identify user that are impackted etc


AWS X-Ray compatibility:
	- lambda, Beanstalk, ECS, ELB, API Gateway
	- EC2 intances or any application server (on-premise)

AWS X-Ray Leverages Tracing:
	- tracing is an end to end way to following reqest
	- each component dealing with the request adds its own trace
	- tracing made sub segments etc
	- X-ray security: supported IAM & KMS 


AWS X-Ray - How to enable:
	- You code (any language) must import AWS X-ray SDK
		- need little code modification, then application can calls aws services, HTTP/HTTPS requests, DB calls etc
	- Install the X-ray Deamon or enable x-ray Aws integrtion
		- X-ray deamon need to install in EC2 or SDK but in the lambda Automatically just need to enable
		- Need IAM Permission

AWS X-Ray troubleshooting:
	- If x-ray is not working on EC2:
		- check EC2 IAM permission role
		- check EC2 intance have X-ray daemon installed
	
	- If enable in AWS Lambda:
		- Check IAM permissions
		- should import X-ray imported in the code
		- enable lambda x-ray active tracing

X-Ray Instrumentation in you code:
	- Instrumentation means measure of product's Performance, diagnose errors and write trace info
	- many SDK require only configuration changes
	- you can modify your application, customize & annotation in the SDK using Interceptors, filters, handlers, middleware etc

X-Ray concepts:
	- Segments : send details
	- Subsegments: for more details
	- trace : for end to end trace
	- sampling : reduce cost, decrese requests sents to X-Ray, each 1 second send request
	- annotation key-value pair used for index trace
	- metadata : key-value pair not for indexed, not for searching
	- supported cross account with IAM permission
	- You can create your own rules for x-ray sampling


X-Ray Write APIs:
	- PutTraceSegments: uploads segments AWS X-Ray
	- PutTelemetryRecordes: to upload telemetry (segmentsReceivedCount, segmentsRejectedCounts etc)
	- GetSamplingRoles: Retrieve sampling Rules
	- GetSamplingTargets & GetSamplingStatisticSummaries
	- IAM polices required for APIs

X-Ray Write APIs:
	- GetServiceGraph: main graph
	- BatchGetTraces: Retrieve list of traces
	- GetTraceSummaries: get annotations for traces 
	- GetTraceGraph: service graph get one or more specific trace IDs


X-Ray with Elastic Beanstalk:
	- included the x-ray daemon
	- you need to enable option or set in the configuration file (.ebextensions/xray-daemon.config)
	- Need IAM permission 
	- application code is instrumented with X-Ray
	
Node: X-Ray not provided the multicontainer docker

X-Ray with ECS:
	- ECS cluster 
		- X-ray container as a daemon
		- X-ray container as a side Car
	
	- Fargate cluster
		- X-ray container as a side Car

AWS Distro for Open Telemetry:
	- Secure, open source, same like X-Ray
	- provides a single set APIs, libraries, agents & collector Services
	- collects distributed traces & metrics from your Apps
	- collects metadata from aws Resouces/Service
	- Auto-Instrumentation agents, without changing code
	- send traces to aws services and 3rd party like zendesk etc
	- Migrate form X-ray to AWS distro for temeletry if you want to stanardize with open-source APIs from telemetry or send traces to multiple destinations


AWS CloudTrail:
	- Provide governance, compliance & audit for your AWS account
	- Cloudtrail is enabled by default
	- Get history of events/API calls in aws account by:
		- Console, SDK, CLI, AWS services etc
	- can put logs cloudtrail to CloudWatch logs or S3

CloudTrail Events:
	- Management Events:
		- operations that are performed on Resources
		- By default, trail are configured to log management events
		- can seperate Read events from write events
		
	- Data Events:
		- by defaults, data events are not logged(bcoz high volume)
		- S3 object delete, get, put operations, lambda invoke etc
		
	- CloudTrail Insights Events:
		- enable cloudtails insights to detect unusal activity
			- hitting limit, bursts AWS IAM Actions etc
		- analyze normal management events to create basline
		- and then continuously analyze write events to detect unusual patterns
	
CloudTrail Events Retention:
	- stored for 90 days in Cloudtrail 
	- for more time store in S3 then use athena for getting that record 

Amazon EventBridge - Intercept API Calls:
	- User --> delete API call --> DynamoDB --> logs api call --> Cloudtrail --> event --> EventBridge --> alery --> SNS
	
	- User --> asumeRole --> IAM Role --> API call logs --> Cloudtrail --> event --> EventBridge --> alery --> SNS
	
	- User --> edit SG inbound rule --> SG EC2 --> API calls --> Cloudtrail --> event --> EventBridge --> alery --> SNS


Cloudtrail vs Cloudwatch vs X-ray:
	- Cloudtrail:
		- Audit API calls made by users/services/accounts
		- useful to detect unauthorized calls or root cause
	- CloudWatch:
		- CloudWatch metices for monitoring CPU etc
		- CloudWatch Logs for stroing Application logs
		- CloudWatch alarms to send Notifications
	- X-Ray: 
		- Automated trace analysis & controle services map visualizations
		- Latency, Errors, fault analysis
		- Request tracing across distributed etc

Note: CloudWatch is just for overall metrices, X-ray is more trace oriented type of service, and CloudTrail is more auditing API calls related 

------------------------------------------------------------------------------------------------------------------
Date : 2/10/2024   ---> AWS Serverless: Lambda <---

Serverless:
	- Don't need to manage server
	- Serverless == Faas (Function as a service)
	- Just need to deploy the code

Serverless in AWS:
	- AWS lambda, DynamoDB, Cognito, API Gateway,
	- AWS S3, SNS & SQS, Kinesis Data Firehose
	- Aurora Serverless, step Function Fargate etc

Why AWS lambda:
	- Amazon EC2: 
		- Virtual Servers in the Cloud
		- limited RAM & CPU
		- Continously running
		- Scaling means intervention to add/remove Servers
	- Amazon lambda: 
		- Virtual functions - no servers to manage
		- limiteted by time - Short executions
		- run on-demand
		- automated scaling


Benefits of AWS lambda:
	- Easy pricing: pay per request, free 1M request & 4 lac GBs of compute time,
	- Integrated with all AWS services
	- Integrated wit many programming lang
	- easy monitoring through AWS cloudwatch
	- increse RAM will also improve CPU & network Automatically
	- lang:
		- Node.js, Python, Java, C#, Golang, Ruby, Custome runtime etc
	- Lambda Container Images:
		- container imag must implement the lambda runtime API
		- ECS/Fargate is preferred for running arbitrary Docker imgs

AWS Lambda Pricing: Examples
	- pay per calls, first 1M request free, then $0.20 per million request 
	- Pay per duration: (increment 1ms)
		- 4 lac GB/sec of compute are free
	- very cheap, very popular


Lambda - Synchronous Invocations:
	- Synchronous: CLI, SDK, API Gateway, Application Load Balancer
		- Results is returned right away
		- Error handling must happen client side (retries, exponential backoff etc)
	
Lambda - Synchronous Invocations - Services:
	- User Invoked:
		- ELB (ALB)
		- API Gateway
		- CloudFront(lambda@Edge)
		- S3 batch
	- Service Invoked:
		- Cognito
		- AWS step funcitons
	- Other Services:
		- AWS lex
		- AWS Alexa
		- AWS KDF

Lambda Integration with ALB:
	- To expose lambda as an https Endpoint
	- you can use ALB (or API gateway)
	- Lambda must be registered in an target group

ALB to lambda: Http to JSON
	- pass all the nessecery info to lambda in json format to lambda can invoke the request

Lambda to ALB conversions: JSON to http
	- response from the lambda you need to pass the result as json format so ALB can understand result 


ALB Multi-Header Values:
	- ALB can support multi header values (ALB setting)
	- When you enable multi-value headers, then you can send the query string parameters multiple valuesin array format etc.
	- queryStringParameters: {name:["abc","cde"...]}


Lambda - Asynchronous Invocations:
	- Asynchronous: S3, SNS, cloudwatch events.. etc.
	- Event are placed in "Event queue"
	- Lambda attempts 3 retry on error:
		- 1 min wait after 1st, then 2 min wait
	- make sure processing is idempotent (in every case same result)
	- when retries then duplicates logs entries in CW logs
	- Can define DLQ (dead letter queue), SNS or SQS for failed processing (IAM permission needed)
	- Asynchronous incovation allow you to speed up
	
Lambda - Asynchronous Invocations - Services:
	- AWS S3
	- AWS SNS
	- AWS Cloudwatch Events/EventBridge
	- AWS CodeCommit, aws codePipeline
	- AWS cloudwatch logs
	- AWS SES 
	- AWS cloudfromation
	- AWS config, IOT, IOT events etc

Cloudwatch Event / EventBridge:
	- using corn expression invoke lambda function 

S3 Event Notifications:
	- S3 object create, update, read, delete, repication etc using these event can create trigger which is asynchonous
	- event can sec to minutes to invoke 
	- If you are using Asynchronous then Used DLQ, It is recommanded on Doc.
	
Lambda - Event Source Mapping(poll methed):
	- Kinesis Data streams
	- SQS & SQS FIFO queue
	- DynamoDB streams
	
	- Model: 
		- Common denominator: record need to be polled from the source
		- Your Lambda Function is invoked Synchronously

Streams & lambda (Kinesis & DynamoDB):
	- process item in order, event source mapping creates an iterator for each Shard
	- start with new item, from the begining or form timestamp
	- Processed items aren't removed form the stream (other can read, can create connections)
	- low traffic: use batch window processing
	- you can process multiple batches in parallel
		- upto 10 batches per Shard
	
Streams & Lambda - Error Handling:
	- By default, if function return an error, the entire batch is reprocessed until the function succeeds, or items in the batch expire
	- to ensure in-order processing, affected processing shard paused until the error is resolved
	- can configure event source mapping to:
		- Discrad old Event
		- restrict no of retries
		- split the batch on error
	- discarded event can go to a Destination

Lambda - Event Source Mapping SQS & SQS FIFO:
	- Event Source Mapping will poll SQS (Long polling)
	- specify batch size (1-10 msg)
	- REcommanded: Set the queue Visibility timeout to 6x timeout of lambda
	- to use DLQ:
		- set-up on SQS queue not lambda (DLQ only work for Asynchronous operation in lambda)
		- use lambda destination for failures

Queue & Lambda:
	- Lambda support in-order processing for FIFO, scaling up to the no of active msg Groups
	- For standard queue, items aren't necessarily processed in order
	- When Error occurs, batches are returned to the queue as individual items, and process in diff. grouping than origial batch
	- lambda deletes items after processed in queue
	- configure soruce queue to send items to a dead-letter queue if any error came.

Lambda Event Mapper Scaling:
	- KDS & DynamoDB streams:
		- one lambda invocaiton per stream shard 
		- if parallelize, upto 10 batches per shard
	
	- SQS Standard:
		- lambda adds 60 more instances per min to scale
		- upto 1000 batches of msgs
	
	- SQS FIFO:
		- Msgs with the same GroupID will be precessed in-order
		- lambda scales to the no of active msg groups

Lambda - Event & contet Objects:
	- Event Object:
		- JSON-formatted document for process 
		- contains information from the invoking service (e.g. EventBridge, custom etc)
		- Lambda runtime convert event json to object
		- Examples: imputes arguments, invokeing service arguments
	
	- Context Object:
		- provides methods & properties that provide info about te invocation, runtime env etc
		- passed at the run Time
		- example AWS reuest ID, function_name, memory limit etc


Lambda - Destinations:
	- Nov 2019: can configure to send result 
	- Asynchronous invocations: worked for both success and failed
		- SQS, SNS, lambda, EventBridge etc
	- AWS recommandeds you to use destinations instead of DLQ 
	- Event Source mapping: for discarded event batches
		- SQS, SNS
	- Note: you can send events to DLQ directly from sqs

lambda Execution Role:
	- Grants lambda function permission to use Services
	- When use event source mapping to invoke your function, Lambda uses the execution role to read event data
	- Best Pratice: Create one lambda execution role per function 

Lambda Resource Based Policies:
	- Use resource-based policies to give other accounts & AWS services permission to use your lambda resources 
	- Basically it is used for giving the lambda access to other services.
	- Similar to S3 bucket policies for S3 Bucket
	- IAM permission can access lambda:
		- IAM policies user
		- resource-based Policy
	- when S3 calls your lambda function, then resource-based policy gives it access

Lambda Environment variable:
	- support env variables
	- lambda service adds its own system enviroment variables as well
	- you can encrypt also the env using KMS or SMK

Lambda Logging & Monitoring:
	- Cloudwatch Logs:
		- lambda logs stored in AWS cloudwatch logs
		- make sure aws lambda functions has an execution role with an IAM policy
	- CloudWatch Metrics:
		- lambda metrics are displated in AWS cloudwatch metrics
		- invocations, Durations, Concurrent executions
		- Async Delivery failures

Lambda Tracing with X-Ray:
	- option to enable
	- runs the X-Ray daemon for you
	- use AWS X-Ray sdk in code
	- IAM permission needed (AWSXRAYDaemonWritesAccess)
	- env variables communicate with X-Ray
		- _X_AMZN_TRACE_ID: Contains the tracing header
		- AWS_XRAY_CONTEXT_MISSING: by deafult, LOG_ERROR
		- AWS_XRAY_DAEMON_ADDRESS: the X-Ray daemon IP_ADDRESS:PORT etc

Customization At the Edge:
	- many modern application execute some logic at the Edge
	- Edge Function:
		- A code can attach to cloudfront distributions
		- runs close to uses so minimize latency
	- cloudfront provides two types: Cloudfront Function & Lambda@Edge
	- full serverless, pay per use, deployed Globally
	- use case : customize CDN content

Cloudfront Function & Lambda@Edge Use Cases:
	- Website Security & privacy
	- Dynamic Web Application at the Edge
	- Search Engine Optimization (SEO)
	- Intelligently Route across Origins
	- Real-time imge Transformation
	- A/B testing
	- User Authentication & authorization
	- User tracking & analytics etc

Cloudfront Function:
	- Flow:
		- Client --> Viewer Request --> Cloudfront --> origin Request --> Origin Response --> Cloudfront --> Viewer response

	- lightweight Functions written in js
	- high-scale, latency-sensitive CDN customizations
	- million req/sec
	- used to change viewer req & res:
		- viewer request: after CF receives a request from Viewer
		- Viewer Response: before CF forwards the response to the viewer
	- Native feature of CF (manage code entierly within CF)

Lambda@Edge:
	- Lambda funcitons supports nodejs & python
	- scales to 1000s of req/sec
	- used to change CF req & res
	- one AWS region (us-east-1), then CF replicates to its locations


Cloudfront Function vs Lambda@Edge:
	- Cloudfront Function:
		- cache key normalization
		- header manipulation 
		- URL rewrites or redirects
		- Request authentication & authorization etc
	
	- Lambda@Edge:
		- Longer execution time
		- Adjustable CPU or memory
		- code depends on 3rd libraries
		- Network access to use external Services
		- File system access or access to the body of HTTPS
		- for creating signin credential using AWS signv4

Lambda by Default:
	- by default, lambda is outside of VPC (AWS-owned VPC)
	- therefore cannot access resources in your VPC (RDS, Elasticache, ELB etc)
	
Lambda in VPC:	
	- for solvinf need to add in the VPC
	- must define VPC ID, Subnets, SG 
	- lambda will create ENI in your Subnets
	- AWSLambdaVPCAccessExecutionRole Permission
	
Lambda in VPC - Internet Access:
	- Lambda function in VPC does not have internet Access
	- Deploying lambda function in a public subnet does not give it internet access or public IP
	- Deploying a Lambda Function in a Private subnet gives it internet access if you have a NAT Gateway/instance
	- You can use VPC endpoints to privately access AWS services without a NAT
	

Lambda Function Configuration:
	- RAM:
		- from 128MB to 10 GB in 1MB increment
		- more RAM Automatic More CPU
		- At 1,792 MB, a function have equivalent one full CPU
		- after 1792 MB, for more CPU, need to use multi-threading in your code 
		- IF your application is CPU-bound, increse RAM
		- Timeout: default 3 sec, maximum 900 sec(15min) for more time use Fargate, ECS, EC2 etc
	
Lambda Execution Context:
	- execution context is a temporary runtime enviroment that initialize any external dependencies of your code
	- execution context is maintained for some time in anicipation of another lambda Function
	- re-use the next function invocation same context, for saving the time and space
	- the execution context includes the /tmp directory
	
Lambda Function /tmp space:
	- if lambda function need to download big files
	- If Lambda function need to disk space to perform operations
	- you can use /tmp directory, max size is 10 GB
	- for permanent persistence of object (non-temporary), use S3
	- to encrypt content on /tmp, use KMS data keys

Lambda Layers:
	- Custom Runtimes:
		- Ex: C++, Rust
	- Externalize Dependencies to re-use them
	
Lambda - file systems Mounting:
	- Lambda functions can access EFS file systems if they are running in a VPC
	- Configure Lambda to mount EFS file systems to local directory during initialize
	- Must leverage EFS access Points
	
Lambda Concurrency & Throttling:
	- Concurrency limit: Upto 1000 concurrent executions
	- can set reserved concurrency at the function level
	- each invocation over the Concurrency limit will trigger a throttle
	- throttle behavior:
		- if Synchronous invocation => return throttle Error - 429
		- if Asynchonous invocaiton => retry then DLQ
	- for more limit, open a support ticket

Lambda Concurrency Issue:	
	- If you don't reserve (=limit) Concurrency, then folling issue can occour:
		- IF all application using lambda like ALB, API gateway and CLI
		- Then if ALB used 1000 concurrent execution then API and CLI for one request give the throttle error bcoz total 1000 you need to handle carefully
	- Same for Asynchonous also but for this Exponential backoff can handle this with DLQ
	
Clod Starts & Provisioned Concurrency:
	- Clod Starts:
		- First request take time for all the code load + env setup + layer load etc, So take time to execute for first time (called cold start)
	
	- Provisioned Concurrency:
		- Concurrency is allocated before the function invoked
		- handle cold start also low latency
		- ASG can manage concurrency (schedule ot target)
	- Note : Clod start detected in oct 2019


Lambda External Dependencies:
	- Lambda Function Dependencies:
		- you can add external libraries also using layer or direct upload in zip file, e.g. AWS X-Ray SDK, DB Clint etc
	
	- Upload zip if it is less then 50MB if more then use S3 and give the link
	- Native libraries work: need to be compiled on Amazon linux
	- AWS SDK comes by default with every lambda function 

Lambda & cloudfromation - inline:
	- Inline funciton are simple
	- use the Code.ZipFile property
	- you can not include function dependencies with inline Functions
	
Lambda & cloudfromation - through S3:
	- you must store in lambda zip in S3
	- must refer the S3 zip location in cloudformation Code:
		- S3Bucket
		- S3Key: full path to zip
		- S3ObjectVersion: if versioned bucket
	- If you update the code in S3, But don't update S3Bucket, S3Key or S3ObjectVersion, Cloudformation won't updated your function
	

Lambda & Cloudformation - through S3 multiple acounts:
	- you need to create cloudformation for all account and bucket policy for first S3 bucket so it can allow you to get data from this account to other account & replicate the data


Lambda Container Images:
	- Deploy Lambda function as container images, upto 10GB from ECR
	- Pack complex & large dependencies in a container
	- Base imgs Available for python, Nodejs, java, Go etc
	- Can create your own image as long as it implements the lambda Runtime api
	- Test container locally using the lambda runtime interface Emulator
	- Unified workflow to build apps

Lambda conatiner Imgs - Best Practices:
	- Stategies for optimizing conatiner imgs:
		- Use AWS-provided Base images
			- stable, run linux 2, cache by lambda services
		- Use Multi-Stage Builds:
			- build code in larger preliminary imgs
		- Build from stable to Frequently Changing
		- Use a Single Repository for Function with large layers
	
	- Use them to upload large Lambda functions (upto 10 GB)
	
AWS Lambda Versions:
	- when you work it is $latest version
	- When you ready to publish lambda function, we create new version
	- version are Immutable
	- version can incrase version no
	- version get their own ARN 
	- version = code + configuration (nothing can change - Immutable)
	- Each version can accessable
	
Aws Lambda Aliases:
	- Aliases are pointers to lambda functions versions
	- define dev, prod, test as pointer for different-2 lambda version (only version change after the Alias)
	- Alias are mutable
	- Aliases enable Canary deployment by assigning weight to lambda Function
	- Aliases enable stable configuration of our event Trigger
	- Aliases have their own ARNs
	- Aliases connot reference aliases
	
Lambda & codeDeploy:	
	- codeDeploy can help you automate traffic shift for lambda Aliases
	- codeDeploy is the SAM feature
	- Linear : grow traffic eveny N minutes until 100%, e.g. 10% - 3min, 20% - 10 min,  30% - 15 min
	- Canary: Try X persent then 100%
	- AllAtOnce: immediate, dangerous (not testes)
	- Can create pre & post traffic hooks to check health of lambda
		
Lambda & CodeDeploy - AppSec.yml:
	- Name (Required)
	- Alias (Required)
	- CurrentVersion (Required)
	- TargetVersion (Required)
	
	
Lambda - Function URL:
	- Dedicted HTTPS endpoint for your lambda
	- A unique URL endpoint 
	- invoke via web browser, CURL, Postman etc
	- Access your function URL through Public internet Only
	- Support resource based policies & cors Configuration
	- Can applied to any function or $latest
	- Create & Configure using AWS console or AWS API
	- Throttle your function by reserved Concurrency
	
	
Lmabda - Function URL Security:
	- Resource-based Policy:
		- Authorize other account / CIDR/ IAM principals
	
	- Cross-origin Resource Sharing(CORS):
		- If you call your lambda function URL from a different domain
	
	- AuthType None:
		- allow public & unauthenticated Access
		- Resource-based policy is always in effect (must grant public access)
	
	- AuthType AWS_IAM:
		- IAM used authenticate & authorize Request
		- both identity-based & resource based policy are evaluated
		- must principal must have lambda:InvokeFunction URL
		- same account - identity based or resource based allow
		- Cross account - identity based AND resource based allow


Lambda & CodeGuru Profiling:
	- Gain insight into runtime performance of your lambda functions
	- codeGuru creates a profiler group for your lambda
	- supported java & python
	- IAM policy: AmazonCodeGuruProfilerAgentAccess
	- Activate from AWS lambda Console

AWS lambda Limit to know - per region:
	- Execution:
		- Memory allocation: 128MB - 10GB (1MB increments)
		- maximum execution time 900 sec (15 min)
		- enviroment variable (4kb) max
		- Disk capacity in the function continer: 512 MB to 10 GB
		- concurrency execution : 1000 (can be incresed by support ticket)
	
	- Deployment:
		- Lambda fun size (compressed): 50MB 
		- Size of uncompressed (code + dependencies): 250MB
		- Can use the /tmp directory to load other files
		- size of env variables: 4KB

AWS Lambda Best Practices:
	- Perform heavy-duty work outside of your function handler:
		- connect DB
		- initialize aws SDK.. libraries
		- pull dependencies or Datasets
	
	- Use enviroment variables for:
		- DB connection string, s3 bucket... (don't put in the code)
		- password, sensitive value ... encrypt using KMS
	
	- Minimize your deployment package size to its runtime necessites:
		- break down function if needed
		- remember aws lambda Limit
		- use layers where necessary
	
	- Avoid using recursice code, never have lambda function call itself

------------------------------------------------------------------------------------------------------------------
Date : 2/11/2024   ---> AWS Serverless: DynamoDB <---

Traditional Architecture:
	- Client ---> Application layer (elb + ASG(instances)) ---> Database layer (RDS)
	- Traditional application laverage RDBMS databases
	- use SQL query lang, strong requirements abouth the data modeled
	- ability to do query, joins, aggregations, complex computations
	- vertical scaling (get more CPU, RAM, IO)
	- Horizontal Scaling (incresing reading capability EC2, RDS read replics)
	
NoSQL Database:
	- non-relational database & distributed
	- db like MongoDB, DynamoDB
	- do not support query joins
	- does not Support aggregation, SUM, AVG etc
	- NoSQL DB scale Horizontal
	
Note: Both database are good any one can use based on your use case

Amazon DynamoDB:
	- Fully managed, high available with replication also multiple AZs
	- NoSQL DB - not a relational db
	- Scales to massive workloads, distributed db
	- handle millions requests per sec, trillion of row, 100s of TB of Storage
	- Fast, consistent in performance (low latency)
	- integrated with IAM, Autorization & Administration
	- Enables event driven programming with DynamoDB streams
	- Low cost, auto-scaling capability
	- Standard & Infrequent Access(IA) table class

DynamoDB - Basic:
	- dynamoDB is made of tables
	- each table has PK (decided at creation time)
	- each table can have infinity no of items
	- Each item has attributs
	- maximum size per item 400 KB
	- Data type supported: 
		- Scalar types - strings, number, bool,null etc
		- Document types - list, map
		- set types - string set, number set, binary set etc

DynamoDB - Primary Keys:
	- option 1: Partition Key (HASH)
		- unique, diverse, distributed e.g user_id
	- option 2: Partition key + sort key (HASH + RANGE)
		- using both create unique key

DynamoDB - Read/Write Capacity Modes:
	- control using capacity (read/write throughput)
	
	- Provisioned Mode (Default):
		- need to specify the no of read/write per second
		- need to plan capacity beforehand
		- pay for provisioned read & write Mode
	
	- On-demand Mode:
		- read/write automatically scale up/down(vertical scaling) with workloads	
		- no capacity planning needed
		- pay per use, more expensive
	
	- you can switch b/w Mode after every 24 hours


R/W Capacity Modes - Provisioned:
	- provisioned read & write capacity units
	- Read Capacity Units(RCU) - ThroughPut reads
	- Write Capacity Units(WCU) - ThroughPut Writes
	- Option to setup auto-Scaling throughput to meet demand
	- In Burst Capacity, ThroughPut can be exceeded temporarily
	- If Burst Capacity consumed, then get a "ProvisionedThroughPutExceededException"
	- Then use exponential Backoff


DynamoDB - Write Capacity Units (WCU):
	- 1 WCU = write per second for 1KB item
	- if items are larger than 1KB, more WCU need
	- e.g. if write 10 items per second, with item size 2KB
	- solution: 10 * (2KB/1KB) = 20 WCUs


Strongly Consistent Read vs Eventully Consistent Read:
	- Eventully Consistent Read:
		- default
		- take 100 milisecond to change in DB
	- Strongly Consistent Read:
		- if you need just write, read functionality
		- set "ConsistentRead" Paramerte true in API Calls (GatItem, BatchGetItem, Query, Scan)
		- Consumes twice the RCU 
		- so ratio   2(eventully):1(strongly)
	- For both the item is 4kb, always round fingure in 4
	- e.g. 10 Strong consistent per sec, item 4kb
	- solution: 10 * (4KB/4KB) = 10RCU
	- e.g2. 16 Eventully per sec, item 12 KB
	- solution: 16 * 1/2 * (12KB/4KB) = 24 RCUs  
	
	
DynamoDB - Partitions Internal:
	- Data is stored in Partitions
	- partition keys go through a hashing algo
	- WCUs & RCUs are spread evenly across partitions

DynamoDB - Throttling:
	- if we exceed provisioned RCU or WCUs, then ProvisionedThroughPutExceededException
	- Reasons:
		- Hot Keys: 1 partition key have too many items
		- Hot Partition
		- Very large items: RCU & WCU depends on size of items
	
	- Solutions:
		- Exponential Backoff (alread in SDK)
		- Distribute partition key as much as possible
		- If RCU issue, use DynamoDB Accelerator(DAX)
	
R/W Capacity Modes - On-demand:
	- read/write Automatically scale up/down with workload
	- No capacity planning needed (WCU/RCU)
	- Unlimited WCU & RCU, no throttle, more expensive
	- 2.5x more expensive
	- used RRU (read req Units), WRU (write req units) for throughput
	- use case: unknown workload, etc

dynamoDB - Writing Data:
	- PutItem:
		- create new item or fully replace old item(same PK)
		- use WCUs
	
	- UpdateItem:
		- edits items or create new item if not exist 
		- used for Atomic counters
		
	- Conditional Writes:
		- Accept write/update/delete only if condition met, otherwise error return
		- Helps with concurrent access items

dynamoDB - Reading Data:
	- GetItem:
		- read using PK
		- PK can use HASH or HASH + RANGE
		- Eventually Consistent Read (deafult), optional to use strongly consistent read (more RCU, longer time)
		- ProjectionExpression specfied only certain attributes
		
dynamoDB - Reading Data(Query):
	- Query return items based on:
		- KeyConditionExpression
			- PK requred, sort key optional
		- FliterExpression
			- additional filtering after query 
			- not use hash or range attribute

	- Returns:
		- items specfied in limit
		- upto 1MB data
	- Pagination ability
	- can query table, local secondary index, Global secondary index
	

dynamoDB - Reading Data(Scan):
	- Scan run on entire tabel data then Filter your data
	- return upto 1MB - use Pagination
	- consumes lot RCU
	- for faster performance, use parallel Scan
	- can use ProjectionExpression & FilterExpression

dynamoDB - Delete Data:
	- DeleteItem
		- delete individual item using PK
		- ability to delete using condition 
	
	- DeleteTable
		- Delete whole table and all its items
		- much quicker then delete of all items

dynamoDB - Batch Operations:
	- reduce the API calls, latency Improve
	- operation done in parallel, give better efficiency
	- if batch fail, then try again on only fail item
	
	- BatchWriteItem:
		- upto 25 putitem & deleteitem in one call
		- upto 16MB of data wittern, upto 400KB data per item
		- can't update item
		- if failed then unprocessedItems use Exponential backoff
	
	- BatchGetItem:
		- get from one to more tables
		- upto 100 items, upto 16MB
		- item retrieved in parallel, fast
		- if failed then unprocessedKeys item use Exponential backoff

DynamoDB - PartiQL:
	- SQL compatiblity query language for DynamoDB
	- allow you to select, insert, update & delete data in DynamoDB using SQL (simple query can perform)
	- run query across multiple dynamoDB
	- run partiQL:
		- AWS consoles
		- NoSQL workbench
		- DynamoDB APIs
		- AWS CLI
		- AWS SDK

DynamoDB - Conditional Writes:
	- For PutIem, UpdateItem, DeleteItem, BatchWriteItem
	- you can specify condition expression:
		- attribute_exists
		- attribute_not_exists
		- attribute_type
		- contain (for string) : check if string is contained in another string
		- begins_with (for string) : check prefix match
		- ProductCategory IN (:cat1, :cat2), AND price BETWEEN :low AND :high
		- size
	- Note: Filter Expression filters results of read query, condition expression are write operation

Conditional Writes - Do Not Overwrite Elements:
	- attribute_not_exists(partition_key)
		- make sure item isn't overwritten
	- attribute_not_exists(partition_key) & attribute_not_exists(sort_key)
		- Make sure the partition / sort key combination is not overwritten
	
DynamoDB - Local secondary Index (LSI):
	- Alternative Sort Key for table (same partition key as base table)
	- sort key consists of our scalar attribute (string, Number, binary)
	- upto 5 LSI per Table
	- Must defined at table creation Time
	- attribute Projections - can conatin some or all attributes of base Table (KEY_ONLY, INCLUDE, ALL)

DynamoDB - Global secondary Index (GSI):
	- Alternative Primary Key(HASH & HASH+RANGE) from table
	- Speed up queries on non-key attribute
	- Index key consists of our scalar attribute (string, Number, binary)
	- attribute Projections - can conatin some or all attributes of base Table (KEY_ONLY, INCLUDE, ALL)
	- Must provision RCUs & WCUs for index
	- Can be added/modified after table creation 
	- can defined at table creation Time & after time also
 	
	
DynamoDB - Indexes & Throttling:
	- Global secondary Index:
		- if the writes are throttled on GSI, then mail table will Throttled
		- Even If the WCU on main table fine
		- Choose your GSI partition key carefully
		- Assign your WCU capacity carefully
	
	- Local Secondary Index:
		- Uses the WCU & RCUs of the main table
		- No Special throttling considerrations
	
	
DynamoDB - PartiQL:
	- use sql query
	- support statments: Insert, Update, Select, delete
	- It support Batch operation 

DynamoDB - Optimistic Locking:
	- DynamoDB has a feature called "Conditional Writes"
	- A strategy to ensure an item hasn't changed before you update/delete it
	- Each item have version attribute
	- based on version attribute you can add some condition for update or delete it will help to write the Atomic queries
	
DynamoDB Accelerator (DAX):
	- Fully-managed, highly Available, seamless in-memory cache for DynamoDB
	- Microseconds latency for cached reads & queries
	- Doesn't require application logic modification (Compatible with existing DynamoDB APIs)
	- Solve "Hot Key" problem (too many reads)
	- 4 min TTL for cache(deafult)
	- upto 10 nodes in Cluster
	- Supported multi-AZ
	- secure (KMS, VPC, IAM, Cloudtrail.. all supported)
	
	
DynamoDB Accelerator (DAX) vs ElasiCache:
	- application --> store Aggregation Result --> Amazon Elastic cache
	- application ---> (individual object cache, Query, scan cache) --> DAX --> dynamoDB
	
DynamoDB Stream:
	- Ordered stream on these modification (create/update/delete) in table
	- Stream records :	
		- KDS
		- lambda
		- KCL applications
	- data retention upto 24 hr
	- Use case:
		- react to change in real time
		- analytics
		- insert into derivative tables
		- insert into opensearch service
		- implements cross-region Replication
	
	- Ability to choose info:
		- KEYS_ONLY - only key attribute modified item
		- NEW_IMAGE - modified item get
		- OLD_IMAGE - before modified Image get
		- NEW_AND_OLD_IAMGE - both item get 
	
	- DynamoDB streams are made of shards, same like KDS
	- don't need to provision shards, handle by aws
	- Records are not retroactively populated in stream after enable, after enable one any changes happend then populated 


dynamoDB Stream & AWS Lambda:
	- need to define Event Source Mapping to read from dynamoDB Streams
	- need lambda permission 
	- your lambda function invoked Synchronously


DynamoDB - Time to Live (TTL):
	- Automatically delete items after an expiry timestamp
	- doesn't consume any WCUs
	- The TTL attribute must be a number data type with Unix Epoch timestamp
	- Expired items deleted within 24 to 48 hr
	- Expire items, that haven't deleted, appears in read/queries/scans (if you don't want them, filter them)
	- For deleting expire item first scan then findout expired item then delete the expire item
	- Use Cases: Reduce stored data by keeping only current items etc


DynamoDB CLI - Good to know:
	- --projection-expression : One or more attributes to Retrieve (filter columns)
	- --filter-expression : filter items before returned 
	
	- General AWS CLI Pagination options (DynamoDB, S3):
		- --page-size: specify that AWS CLI retrieve full items using parallel call which you are declare, If you don't declare then it will try to get all data in one API call (Default 1000 items)
		- --max-items: max. number of items to show on CLI (return nextToken)
		- --Starting-Token: specify last nextToken to retrieve next set of items 


DynamoDB Transactions:
	- Coordinated, All-or-nothing operations (add/update/delete) to multiple items across one or more table
	- Provided ACID (atomicity, Consistency, Isolation, Durability)
	- Read Modes - Eventual Consistency, Strong Consistency, Transactional
	- Write Modes - Standard, Transactional
	- Consumes 2(WCU & RCU): perform 2 items for each operation (prepare, commit)
	- Two Operations:
		- TransactGetItems - One or more GetItem Operation
		- TransactWriteItems - one or more PutItem, UpdateItem, deleteItem Operation
	- use case: financial Transactions, managing ordersm multiple games
	- you can change both table at once, if any failed then both failed


DynamoDB Transactions - capacity computation: (Important)
	- e.g.: 3 transactional write per second, item size 5KB
	- solution: 3 * (5KB/1KB) * 2 (Transactional cost) = 30WCU
	
	- e.g2.: 5 transactional read per second, item size 5KB
	- solution: 5 * (8KB/4KB) * 2 (Transactional read cost) = 20WCU

DynamoDB as Session State Cache:
	- It's common to use DynamoDB to store session state-reason
	- vs ElasiCache:
		- ElastiCache is in-memory, but dynamoDB is serverless (suport autoscaling)
		- Both key/value stores
		
	- vs EFS:
		- EFS must attached to EC2 instances as a n/w Drive
		
	- vs EBS & Instance Store:
		- EBS & Instance store can only used for local caching, not for shared caching
	
	- vs S3:
		- s3 is higher latency, not meant for small objects


DynamoDB Write Sharding:
	- if you choose common partition Key then Hot Partition issue came
	- A Startegy that allow better distribution of items evenly across partitions
	- Add a suffix to partition key Value
	- Two methods:
		- Random suffix
		- Calculated Suffix


dynamoDB - write Types: optimistic locking
	- Concurrent Writes: when 2 person update same value then second overwrite the first value
	- Conditional Writes: when 2 person update based on condition of value, then first accepted & second failed  (also called optimistic locking )
	- Atomic Writes: when 2 person write for increment value then both accepted and first increment then second
	- Batch Writes: many items at a time Update

DynamoDB - Large Object Pattern:
	- For storing large Object like Video file & Images
	- Applicaiton upload file in s3 bucket and store the metadata link in DynamoDB, so for Retrieval time get link form DynamoDB and download from S3.

DynamoDB - Indexing S3 Objects Metadata:
	- Application --> upload --> S3 bucket --> invoke --> lambda function --> store object's metadata --> DynamoDB table
	- then data can get using the application using dynamoDB
	
Note: Both Stategies help for:
		- search by data, list the object, all object uploaded successfully, total storage used by consumers

dynamoDB Operations:
	- Table Cleanup
		- option 1: scan + deleteItem : very slow, expensice, consumes RCU & WCU
		- option 2: drop table + recreate same table: fast, efficiency, cheap
	
	- Coping a DynamoDB table:
		- option 1: using aws Data pipelines
		- option 2: backup & restore into new table : take time to store
		- Option 3: Scan + PutItem or batch writeItem : write your own code

DynamoDB - Security & Other Features:
	- Security: 
		- VPC supported, IAM , KMS + SSL/TLS in-transit supported
	
	- backup & Restore feature Available:
		- point to time Recovery(PITR) like rds
		- No Performance impact
		
	- Global tables:
		- Multi-region, multi-active, fully replicated, High Performance
		
	- DynamoDB Local:
		- develope & test locally without accessing dynamoDB
	
	- AWS DB migration service (AWS DMS) can used to migrate to DynamoDB (From MongoDB, Oracle, MySQL etc)


DynamoDB - Users Interact with DynamoDB directly:
	- client + users login through aws temp credential using Identity provider then can directly interact to table


DynamoDB - Fine-Grained Access Control:
	- Web Identity Federation or Congnito Identity Pools can get Credential
	- You can assign IAM role with conditions
	- Leading Keys - limit can apply for user to access
	- attributes - Limit specific attributes the user can see


------------------------------------------------------------------------------------------------------------------
Date : 2/11/2024   ---> AWS Serverless: API Gateway <---

Building Serverless API:	
	- Client ---> Rest API ---> API Gateway ---> Proxy Requests ---> Lambda ---> CRUD ---> dynamoDB
	
AWS API Gateway:
	- AWS Lambda + API Gateway: No infrastruture to manage
	- support websocket Protocal
	- Handle API versioning (v1, v2..)
	- Handle different environments (dev, test, prod)
	- Handle security (Authentication & Authorization)
	- Create API Keys, Handle request Throttling
	- Swagger/Open API import quickly
	- Transform & Validate requests and responses
	- Generate SDK and API specifications
	- Cache API responses


API Gateway - Integrations High Level:
	- Lambda Function:
		- Invoke Lambda function
		- expose REST API connected to Lambda
	
	- HTTP:
		- Expose http endpoints in Backend
		- e.g.: internal http API, ALB...
		- Add rate limiting, caching, user authentications, API keys etc
	
	- AWS Service:
		- expose any service through API Gateway
		- e.g. start AWS Step Function workflow, post message to SQS
		- Add authentication, deploy publicly, rate control etc


API Gateway - AWS Service Integration Kinesis Data Streams example:
	- Client --> request --> API Gateway --> send --> KDS --> Records --> KDF --> store json files --> S3

API Gateway - Endpoint Types:
	- Edge-Optimized(default): For Global client
		- Request are routed through the CF edge locations (improves latency)
		- API Gateway only one region
	
	- Regional:
		- for client within same region
		- cloud manually combine with CF (more control over cache & distribution)
	
	- Private:
		- Can only be accessed from your VPC using interface VPC endpoint(ENI)
		- use resource policy to define access
	
API Gateway - Security:
	- User Authentication through:
		- IAM Roles (useful for internal applications)
		- Cognito (Identity for external users - example mobile users)
		- Custom Authorizer (your own logic)
	
	- Custom Domain Name HTTPS security through intergration with AWS certificate manager (ACM) :
		- if using Edge-Optimized endpoint, then certificate must be in us-east-1
		- if regional endpoint, then certificate must be in API Gateway region
		- Must setup CNAME ot A-alias record in Route 53
		
API Gateway - Deployment Stages:
	- if you and anything in API gate or code then you need to deply te stage, other wise it will not reflect.
	- changes are deployed to Stages (as many as you want or same also)
	- use any naming you like for stage(dev, test, prod etc)
	- Each stage has its own configuration parameters
	- stages can be rolled back as history of deployments is kept

API Gateway - Stage Variables:
	- Stage variable == Enviroment varible for API Gateway
	- Use them to change configuration values 
	- They can used like:
		- Lambda function ARN
		- HTTP Endpoint
		- Parameter mapping templates
	- Use cases:
		- Configure HTTP endpoints for stage to talk to (dev, test, prod)
		- pass configuration parameters to AWS Lambda through mapping templates
		- Stage variable passed in to lambda using the context object
		- Format : ${stageVariable.variableName}


API Gateway Stage Variable & Lambda Aliases:
	- we create stage variable to indicate the corresponding Lambda ALIAS
	- Our API gateway Automatically invoke right lambda
	- Flow:
		- Dev stage API gateway --> DEV alias lambda --> $(Latest) 
		- Test stage API gateway --> Test alias lambda --> v2 (5% traffic canary)
		- Prod stage API gateway --> Prod alias lambda --> v1 (95% traffic canary)

API Gateway - Canary Deployment:
	- Possibity to enable canary deployments for any stage(usually prod)
	- Choose the % traffic first to recieves, then 100%
	- Metrics & logs are seperate (for better monitoring)
	- override stage variable for canary
	- support blue/green deployment with lambda & API gateway


API Gateway - Integration Types:
	- Integration Type MOCK:
		- API gateway return response without sending Request
	
	- Integration type HTTP/AWS(LAMBDA & AWS services):
		- must configure both integration request & integration response
		- setup data mapping using mapping templates for req & res
		- Client --> rest API --> gateway + mapping templates --> aws services integration --> SQS

	- Integration type AWS_PROXY(lambda proxy):
		- incoming req from the client as input for lambda
		- function is responsible for logic of req/res
		- No Mapping template, headers, query string parameters... are passed as arguments
		
	- Integration Type HTTP_PROXY:
		- No mapping template
		- Http req is passed to Backend
		- http res from backend to API gateway
		- Possible to add HTTP Headers if need (e.g. API key)


Mapping Templates(AWS & HTTP Integration):
	- used to modify the req & res
	- rename/modify query string Parameters
	- modify body Content
	- add Headers
	- User velocity Template Language(VTL): for loop if etc..
	- Filter output result (remove unnecessary data)
	- content type can be set to application/json or application/xml


Mapping Example: JSON to XML with SOAP
	- SOAP API are XML based, whereas REST API are JSON based
	- client ---> restful, json payload ---> API gateway + mapping Template --> XML payload ---> SOAP api
	- API gateway should:
		- Extract data from request: either path, payload or Header
		- Build SOAP msg based on req data (mapping template)
		- Call SOAP service & recieve XML response
		- transform XML res to desired format(JSON)
	
Mapping Example: Query String Parameters
	- though mapping template you can convert query string in to JSON format (which we do in helios)
	

API Gateway - Open API Spec:
	- Common way to defining REST APIs, using API defining as code
	- Import existing OpenAPI 3.0 spec to Gateway
		- method
		- method req
		- integration Request
		- Method response
		- + AWS extensions for API gateway & setup every single option
	- Can export current API as OpenAPI spec
	- OpenAPI specs can written in YMAL or JSON
	- Using OpenAPI we can generate SDK for Our Application


REST API - Request Validation:
	- can configure to do basic validation of an API request before proceeding with integration Request
	- validation fail, API Gateway immediately Fails
		- returns a 400-error response to the caller
	- reduce unnecessary calls to Backend
	- checks:
		- required req parameters in URL, Query string & headers of an incoming req are included & non-blank
		- application req payload adheres to configured JSON Schema req model of the method


REST API - Request Validation - OpenAPI:
	- Setup request validation by importing OpenAPI definitions file


Caching API responses:
	- Caching reduces the number of calls made to Backend
	- Default TTL is 300 sec (min:0s, max 3600s)
	- Caches are defined per Stage
	- Possible to override cache setting per method
	- cache encryption option
	- cache capacity b/w 0.5GB to 237GB
	- cache is expensive, so use in prod, don't use in test/dev env


API Gateway Cache Invalidation:
	- able to flush the entire cache (invalidate it) immediately
	- clients can invalidate the cache with header: CacheControl: max-age=0
	- if you don't impose an invalidateCache policy, any client can invalidate API cache

API Gateway - Usege Plan & API Keys:
	- you can make API available to your cusotmer but you need to pay some amount.
	- Usage Plan:	
		- can access one or more deployed API stages & methods
		- how much & how fast they can Access
		- API key can identify API clients & meter Access
		- congifure throuttling limits & guota limit for individual Client
	
	- API Keys:
		- alphanumertic string value, distribte to your Customer
		- can use with usage Plans
		- Throttling limits are applied to API keys
		- Quotas limit is overall no of maximum Requests
		
API Gateway - Correct Order for API keys:
	- To configure usage plan
		- Crate one or more APIs, configure methods to required an API key, and deploy the APIs to Stage
		- Generate or import API keys to distribute application developers who will using Your API 
		- create the usage plan with throttle & quata Limits
		- Associate API stage & API keys with the plan
		
	- Callers of the API must supply as assigned API key "x-api-key" in headers
		

API Gateway - Logging & tracing:
	- Cloudwatch logs:
		- Log contains information about req/res body
		- enable cloudwatch log in any stage for (ERROR, DEBUG, INFO etc)
		- can override settings on a per API basis
		
	- X-Ray:	
		- enable tracing to get extra info about requests in API gateway
		- X-ray API Gateway + AWS Lambda gives you full picture

API Gateway - CloudWatch Metircs:
	- Metrics are by stage, enable for details metrics
	- CacheHitCount & CacheMissCount: efficiency of cache
	- Count : total no of API Request
	- IntegrationLatency: time b/w api request to backend to till received response from Backend
	- Latency: time b/w receives request from client to return response to the client. Latency inculdes integration latency + other API gateway overhead(authenticate + authorization)
	- 4xx error (client-side), 5xx(server side)


API Gateway Throttling:
	- Account Limit:	
		- API throttles request 10K (soft limit)
	- throttling error: 429 too many request (use exponential Backoff)
	- can set limit on stage or method & improve performance
	- can define Usage plans to throttle per costomer
	
	- just like lambda Concurrency, one API that is overloaded, if not limited, can cause the other APIs to b throttled


API Gateway - Error:
	- 4xx means Client errors:
		- 400: bad Request
		- 403: access denied, WAF filtered
		- 429: Quata exceeded, Throttle
	- 5xx means Server errors:
		- 502: bad gateway exception, for haavy load
		- 503: service Unavailable exception
		- 504: integration Failure - timeout 29 sec
		
	
AWS API gateway - CORS:
	- CORS must be enabled when you receive API calls another Domain
	- The OPTIONS pre-flight request headers:
		- Access-Control-Allow-Methods
		- Access-Control-Allow-Headers
		- Access-Control-Allow-Origin
	- CORS can enable through console


API Gateway - Security IAM permission:
	- Create an IAM policy authorization & attach to user/role
	- Authentication = IAM / Authorization = IAM policy
	- Good to provide access within AWS (EC2, lambda, Iam users..)
	- sigv4 capability == IAM credential are in Headers
	

API Gateway - Resource Policies:
	- Resource Policies (similar to lambda resource policy)
	- Allow for cross account Access
	- allow specific source
	- allow VPC endpoints


API Gateway - Security Cognito User Pools:
	- Cognito User Pools:
		- Cognito Fully manages user lifecycle, token expires automatically
		- API gateway verifies identity automatically from Cognito
		- no custom implementation Required
		- Authentication = cognito User Pools / authrization = API gateway methods

API Gateway - Security Lambda Authorizer (formerly custom Authorizers):
	- Token based authorizer (bearer token) - ex JWT (JSON Web token) or oauth
	- A req parameter-based lambda Authorizer
	- lambda must return IAM policy for the user, result policy is cached
	- Authentication = External / Authorization = Lambda Function

API Gateway - Security - Summary:	
	- IAM:
		- Greate for users / roles already within your aws account + reqource policy for cross account
		- Handle authentication + authorization
		- Leverages signature v4

	- Custom Authorizer:
		- Great for 3rd party Tokens
		- very Flexible in terms of IAM policy is returned
		- handle Authentication + Authorization in lambda function
		- pay per lambda function invocation, results are cached 
		
	- Cognito User pool:
		- You manahed your own user pool (use facebook, google login.. etc)
		- No need to write custom code
		- Must implement authorization in the backend


API Gateway - HTTP API vs REST API:
	- HTTP APIs:
		- Low-latency, cost-effective AWS lambda proxy, HTTP proxy APIs & private integration
		- Support OIDC & OAuth 2.0 Authentication, buit-in support for cors
		- No usage plan & API keys
	
	- Rest APIs:
		- All feature (except native OpenId connect/OAuth 2.0)

API Gateway - websocket API - Overview:
	- websocket:
		- Two way interactive communication b/w user's brpwser & server
		- server can send msg to client
		- enables stateful application 
	- WebSocket APIs are often used in real time application like chat app, game, trading etc
	- Works with AWS service (lambda,DynamoDB) or HTTP endpoints


Connection to the API:
	- websocket URL:
		- wss://[some-uniqueId].execute-api.[region].amazonaws.co/[stage-name]
		
	- Connection URL callback
		- wss://[same-uniqueId].execute-api.[same-region].amazonaws.co/[same-stage-name]/@connections/connectionId


Connection URL Operations:
	- Post : for send msg
	- Get : for GET msg
	- Delete: for delete msg
	
	
API Gateway - WebSocket API - Routing:
	- Usinf routing expression it will Route
	- If no routes : send default (route)
	- request a route selection expression to select the field on JSON to route 
	- expression: $request.body.action
	- result evaluated against the toute keys
	
API Gateway - Architechtre:
	- Create a single interface for all the microservices in your company
	- Use API endpoints with various resources
	- Apply simple domain name & SSL certificates
	- Can apply forwarding and transformation rules at the API Gateway level


------------------------------------------------------------------------------------------------------------------
Date : 2/14/2024   ---> AWS CICD: CodeCommit, codePipeline, CodeBuild, CodeDeploy <---


CICD - Introduction: Continuous Integration Continuous Delivery
	- We learned:
		- create AWS resources, manually(fundamentals)
		- Interact with AWS programmatically (AWS CLI)
		- Deploy code to AWS using Elastic Beanstalk
	
	- All did manual, very likely for us to do mistakes!
	- We would like our code "in a repository" & want to deploy on to aws
		- Automatically, the right way
		- Making sure tested before being deployed
		- with possibility to go into different stage (dev, test, staging, prod)
		- With manaual approval
	
	- To be a proper AWS developer.... we need to learn AWS CICD
	- Now using this we can do all automatically, that we've done so far with adding increased safetly
	
	- Parts:
		- AWS CodeCommit - Stroing our code
		- AWS codePipeline - automating our pipeline form code to Elasic BeanStalk
		- AWS codeBuild - building & testing our code
		- AWS codeDeploy - deploying the code to EC2 instance (not Elastic Beanstalk)
		- AWS CodeStar - manage software Development activities in to one place
		- AWS CodeArtifact - store, publish & share software package
		- AWS CodeGuru - Automated code review using Machine Learning
	
	
Continuous Integration (CI):
	- Developers push the code to a code repo ofter (e.g. GitHub, CodeCommit, BitBucket..)
	- A testing / build server checks the code as soon as it's pushed (codeBild, Jenkins CI..)
	- The developer get feedback early
	- Find bugs early, then fix bugs
	- deliver faster as the code is tested
	- deploy often 
	- happier developers, as they're unblocked

Continuous Delivery (CD):
	- Ensures that software can be released reliably
	- Ensures deployment happen often & quick
	- shift away from 1 release every 3 months to 5 releases a day
	- That usually means automated deployment (e.g codeDeploy, Jenkins CD, Spinnaker..)

Technology Stack for CICD:
	- Code  --> AWS CodeCommit
	- Build --> AWS CodeBuild
	- Test  --> AWS CodeBuild
	- Deploy  --> AWS Elastic Beanstalk
	- Provision  --> AWS Elastic Beanstalk


AWS CodeCommit:
	- Version control is the ability to understand the verious changes that happend to the code over time (and possible roll back)
	- all these enable by using GIT version control
	- A Git repository can be synchronized on your computer, but it uploaded on online repository
	- Benefits:
		- Collaborate with other developers
		- make sure the code is backed-up somewhere
		- Make sure it's fully viewable & auditable
	
	- Git repositories can be expensive
	- the industry includes GITHUB, GITLAB, GITBUCKET..
	- AWS CodeCommit:
		- Private GIT repositories
		- No Size limit on Repo (scale seamlessly)
		- Fully managed, Highly Available
		- code only in AWS Cloud account => Incresed security & Compliance
		- Security (Encrypted, access control...)
		- Integrated with Jenkins, AWS CodeBuild, * other CI Tools
		
CodeCommit - security:
	- Interaction are done using GIT(Standard)
	- Authentication :
		- SSH Keys:	AWS users can configure SSH keys in their IAM console
		- HTTPS - with AWS CLI credential helper or GIT Credentials for IAM User
	- Authorization:
		- IAM Policy manage users/roles for Repo
	- Encryption: 
		- repo automatically encrypeted and can use KMS
		- Encrypeted in transit (can only use HTTPS or SSH- both secure)
	
	- Cross-account Access:	
		- Do Not share ssh keys or AWS credentions
		- Use an IAM roles in your AWS Account & use AWS STS (AssumeRle API)
	

AWS CodePipeline:
	- Visual workflow to your CICD
	- Source - CodeCommit, ECR, S3, BitBucket, GITHUB
	- Build - CodeBuild, Jenkins, CloidBees, TeamCity
	- Test - CodeBuild, AWS Device Farm, 3rd party tools..
	- Deploy - CodeDeploy, Elastic Beanstalk, CloudFormation, ECS, S3...
	- Invoke - Lambda, Step Functions
	- Consists of stages:	
		- Each Stage can have sequential action and/or parallel actions
		- Example: Build --> test --> Deploy --> Load Testing --> ....
		- Manual approval can be defined at any stage
	
CodePipeline - Artifacts:
	- Each pipeline stage can create Artifacts
	- Artifacts stored in S3 bucket & passed on the next Stage
	
Note: Codecommit set output Artifacts to S3 then S3 send to AWS codeBuild same for CodeBuild to CodeDeploy, So sometime you can directly use through the s3.

	- Flow:
		Developer ---> AWS CodeCommit ---> (S3 bucket intermediate) --> AWS CodeBuild ---> (S3 bucket intermediate) --> AWS CodeDeploy 

codePipeline - troubleshooting:
	- for pipeline/action/stage codepipline state changes
	- Use CloudWatch Events (Amazon EventBridge). e.g
		- create events for failed pipelines
		- create events for cancelled Stages
	- If codePipeline fails a stage, your pipeline stop, and you can get information in the console
	- If Pipeline can't perform an action, make sure the "IAM Service Role" attached & have permissions
	- CloudTrail can be used to audit AWS API Calls
	

AWS CodeBuild:
	- Source : CodeCommit, S3, BitBucket, GITHUB
	- Build instructions: Code file "buildspec.yml" or insert manually in Console
	- Output logs can be stored in Amazon S3 & CloudWatch Logs
	- Use CloudWatch Metrics to Monitor Build statistics
	- Use EventBridge to detect faild builds & trigger notifications
	- Use CloudWatch Alarms to notify if you need "thresholds" for failures
	
	- Build Projects can be defined within CodePipeline or codeBuild
	
	- CodeBuild Support all the language + docker conatiner environments


codeBuild - How it Works: Diagram
	- CodeCommit (Source files : Source code + Buildspec.yml) or docker imgs  ---> CodeBuild(run instruction form buildspec.yml) (Can enable cache from S3) ---> if artifacts (s3 bucket) --> if err (store logs: s3, cloudwatch logs) 


CodeBuild - Buildspec.yml:
	- buildspec.yml file must be at the root of your code
	- env - define environment Variables
		- variables - paintext Variable
		- parameter-store - SSM store Variable
		- secrets-manager - AWS secrets manager variable
	- phases - commands
		- install: install dependencies for Build
		- pre_build - final commands to execute before Build
		- Build - actual build Command
		- Post_build - finishing touches
	- artifacts - what to upload to S3 (encryped KMS)
	- cache - files to cache (dependencies) to S3 for future build speedup


AWS CodeDeploy:
	- Deployment service that automates application Deployment
	- Deploy new Applications versions to EC2 instance, On-premises servers, lambda, ECS service
	- Automated Rollback capability in case of failed deployment, or trigger cloudwatch alarm
	- Gradual deployment control
	- "appspec.yml" file defines how the deployment happens

CodeDeploy - EC2/On-premises Platform:
	- Can deploy to EC2 Instance & On-premises services
	- Perform in-place deployments or blue/green deployment
	- Must run the codeDeploy Agent on the target instances
	- Define deployment speed
		- AllAtOnce: Most downtime
		- HalfAtATime: reduced capacity to 50%
		- OneAtATime: slowest, lowest availability impact
		- Custom: define your %

CodeDeploy Agent:
	- codeDeploy agent must be running on EC2 instances as a pre-requisites
	- It can be installed & updated automatically if you're using Systems Manager
	- The EC2 instance must have sufficient permission to access S3 to get deployment bundles
	
CodeDeploy - Lambda Platform & ECS Platform(only for Blue/green):
	- CodeDeploy can help you automate traffic shift for lambda Aliases
	- Feature is integrated within the SAM Framework
	- Linear: Grow traffic every N minutes until 100%
		- e.g. 10% every after 3 min
	- Canary: try X percent then 100%
		- e.g. 10% for 5 min then 100%
	- AllAtOnce: immediate

CodeDeploy - Deployment to EC2:
	- Define how to deploy in Appspec.yml + Deployment strategy
	- Will do in-place updata to your fleet of EC2 Instances
	- Can use hooks to verify the deployment after each deployment phase

CodeDeploy - Deploy to a ASG:
	- In-place Deplyment:
		- Updates existing EC2 instances
		- Newly created EC2 instance by ASG will also automated deployments
		
	- Blue/Green Deployment:
		- New Auto-Scaling group is created (settings are copied)
		- Choose how long to keep the Old EC2 (old ASG)
		- must be using ELB 

codeDeploy - Redeploy & Rollbacks:
	- Rollback = redeploy previously deployed revision of your Application
	- Deployment can be rolled back:
		- Automatically - when failed or rollback when a CloudWatch alarm thresholds are met
		- Manually
	- Disable rollbacks
	
	- if roll back happens, CodeDeploy redeploys the last known good revision as a new deplyment (not a restored version)

AWS CodeStar:
	- An integrated solution that groups: GitHub, CodeCommit, CodeBuild, CodeDeploy, CodeFormation, CodePipeline, CloudWatch,...
	- Quickly create CICD-ready projects for EC2, Lambda, Elastic beanstalk
	- Suppoted Languages: all lang mostly
	- Issue can trach using JIRA/GitHub
	- can integrate with Cloud9 as IDE
	- One dashboard can view all components
	- Free service, pay only for underlying usage Services
	- Limited Customization

AWS CodeArtifact:
	- Software Packages depend on each other to e built (basically Dependencies)
	- Storing & retrieving these dependencies is called Artifacts Management
	- CodeArtifact is secure, scalable, cost-effective artifact management for software Development
	- Works with common dependency management tools such as Maven, npm, pip, yarn etc.
	- Developers & codeBuild can then retrieve dependencies straight from CodeArtifact

CodeArtifact - Resource Policy:
	- Can be used to authorize another account to access CodeArtifact
	- Given principal can either read all the packages in a repository or none of them 


Amazon CodeGuru:
	- An ML-powered service for automated code reviews & application performance recommendations
	- provides two functionalities
		- CodeGuru Reviewer: Automated code reviews for static code analysis (development)
		- CodeGuru Profiler: Visibility/recommendations about application Performance during runtime (Production)
	
Amazon CodeGuru Reviewer:
	- Identify critical issues, security vulnerabilities, and hard-to-find bugs
	- Examples: common coding best pratices, resource leaks, security detection, input validation
	- Uses Macine Learning & automated reasoning
	- Hard-learned lessons across millions of code reviews on 1000s of open-source & amazon repositories
	- supported java & python
	- Integrated with GitHub, BitBucket & CodeCommit

Amazon CodeGuru Profiler:
	- helps understand the runtime behaviour of applications
	- e.g. identify if your application is consuming excessive CPU capacity on a logging runtime
	- Features:
		- identify & removed code inefficiencies
		- Improve application Performance
		- decrease compute costs
		- provides heap Summary
		- anomaly detection
	- Support applications running on AWS or on-Premises
	- Minimal overhead on application


Amazon CodeGuru - Agent Configuration:
	- MaxStackDepth - based on depth evaluate the code
	- MemoryUsageLimitPercent - memory percentage used by profiler 
	- MinimumTimeForReportingInMiliseconds - minimum time b/w sending reports
	- ReportingIntervalInMiliseconds - reporting interval used to report profiles
	- SamplingIntervalInMiliseconds - sampling interval that is used to profile samples

AWS Cloud9:
	- Cloud-based IDE
	- Code editor, debugges, terminal in a browser
	- Work on your projects from anywhere with an internet Connection
	- prepackaged with essential Tools
	- share your development environment with your teams (Pair Programming)
	- Fully Integrated with AWS SAM & lambda to easily build serverless applications


------------------------------------------------------------------------------------------------------------------
Date : 2/16/2024   ---> AWS Serverless: SAM - Serverless Application Model <---

AWS SAM:
	- SAM = Serverless Appilcation model
	- Frameworl for developing & deploying serverless Applications
	- All the configuration is YAML/JSON Code
	- Generate Complex CloudFormation using simple SAM YAML file
	- Support anything form Cloudformation: Output, Mapping, Parameters, Resources...
	- Only two commands to deploy to AWS
	- SAM can use CodeDeploy to deploy Lambda functions
	- SAM can help you to run Lambda, API Gateway, DynamoDB locally


AWS SAM - Recipe:
	- Transform Header indicates it's SAM template:
		- Transform: 'AWS::Serverless-2016-10-31'
	- Wirte Code:
		- AWS::Serverless::Function
		- AWS::Serverless::API
		- AWS::Serverless::SimpleTable
	- Package & Deploy:
		- aws cloudformation package / sam Package
		- aws Cloudformation deploy / sam deploy

Deep Dive into SAM Deployment:
	- SAM Template YMAL --> (transform: Build app locally) --> CloudFormation template YMAL--> (zip & upload: package the app) --> s3 --> (create/execute changeSet: Deploy the app) --> Clouformation (deploy services)

	- SAM - CLI Debugging:
		- Locally build, test & debug your serverlss application that are defined using AWS SAM Templates
		- Provides a lambda-like execution environment locally
		- SAM CLI + AWS toolkits => step-trough & debug your code
		- Supported IDE: AWS Cloud9 visual studio code, Jetbrains, pycharm etc
		- AWS toolkits: IDE plugins which allows you to build, test, debug, and invoke lambda functions buils usin AWS SAM


Sam Policy Templates:
	- List of templates to apply permissions to your lambda Functions
	- Important e.g.:
		- S3ReadPolicy: Give read only permission objects of S3
		- SQSPollerPolicy: Allow to poll as SQS queue
		- DynamoDBCrudPolicy: CRUD for dynamoDB


SAM & CodeDeploy:
	- SAM Framework Natively uses CodeDeploy to update lambda function
	- Traffic shifting Feature
	- Pre & Post traffic hooks features to validate deployment (before the traffic shift starts & after it ends)
	- Easy & automated rollback using cloudwatch alarms
	
SAM & CodeDeply:
	- AutoPublishAlias:
		- Detects when new code deployed
		- Creates and Publishes updated version of that function with the latest Code
		- Point the alias to the updated version of the lambda Functions
		
	- DeploymentPreference:	
		- Canary, Linear, AllAtOnce
	
	- Alarms:
		- Alarms that can trigger a rollback
	
	- Hooks:
		- pre and post traffic shifting lambda functions to test your deployment

SAM - Local capabilities:
	- Locally start AWS Lambda:	
		- sam local start-lambda
		- starts a local endpoint that emulates AWS LAMBDA
		- Can run automated tests against this local endpoint
	
	- Locally Invoke Lambda Function
		- SAM Local invoke
		- invoke lambda with payload
		- helpful for Locally test with cases
		- you can use --pofile for api calls 

	- Locally start an API Gateway Endpoint:
		- sam local start-api
		- Starts a local HTTP server that hosts all your Functions
		- Changes to functions are automatically reloaded
	
	- Generate AWS Events for lambda functions:
		- Sam local generate-event
		- Generate sample payloads for event Sources
		- s3, API Gateway, SNS, Kinesis, DynamoDB..


SAM - Exam Summary:
	- SAM is build on CF
	- SAM required the transform & resources sections
	- Commands to know:
		- sam build: fetch dependencies & create local deployment Artifacts
		- sam package: package & upload to S3, generate CF Template
		- sam deploy: deploy to CF
	- SAM policy templates for easy IAM policy definition 
	- SAM is integrated with codeDeploy to do deploy lambda aliases



------------------------------------------------------------------------------------------------------------------
Date : 2/16/2024   ---> CLoud Development Kit(CDK)  <---



































Yesterday, we discussed the sprint tasks and also participated in the QA interaction session and introduction about Touchstone Meeting. Afterward, I continued with my AWS course.

Today, I planning to go through the risk studio QA doc & continue with the AWS course.




Tpin: 043263 papa 

It mainly consists in the capability of 


18/1/2024 : done
	EC2 Instance Storage
	AWS Fundamentals : ELB + ASG
	AWS Fundamentals : RDS + Aurora + ElastiCache
	
19/1/2024: done
	Route 53
	VPC Fundamentals

20/1/2024: done
	Amazon S3
	AWS CLI, SDK, IAM Roles & Policies
	Advance Amazon S3
	Amazon S3 security
	
21/1/2024: done
	Cloudfornt
	
22/1/2024: done
	ECS, ECR & Fargate - Docker in AWS

23/1/2024: done
	AWS Elastic Bean stalk
	AWS cloudformation
	
24/1/2024:  Done
	AWS Integration & Messaging: SQS, SNS & Kinesis -- 2.11
	
25/1/2024:  Done
	AWS Monitoring & audit  -- 1.45

26/1/2024: Done
	Serverless: lambda -- 3.8
	AWS Serverless: DynamoDB -- 1.47
	
27/1/2024: 7.52 - 1.22 = 6.30
	AWS Serverless: Apigatway  -- 1.22
	AWS CICD  -- 1.52

28/1/2024:
	AWS Sererless: SAM  -- 46 min
	CDK     -- 26min
	Cognito User Pools  -- 41 min
	Other Serverless: Step function & AppSync   -- 1
	
29/1/2024: office 
	Advanced Identity   --  23
	AWS security & Encryption   -- 1.37
	AWS other Services    -- 37
	
30/1/2024 - 31/1/2024 Extra-day for compatible remaining topice if any left

1 - exam by udemy
2 - exam by aws test / mock test any paper or etc

3 to 7 revision 
8-9 exam date



Goals: 3-4 
	1. Touchstone training
	2. AWS Developer certifications
	3. Learn Dot Net (Frontend Framework)
	4. Learn Dot Net (Backend Framework)


Complete domain training
Complete product training
Scrum related
code quality etc suggestions
Give training PPT




Calculation of loss

loss = RV * Damage

// converage
Damage = Damage ID ---> Intensity Value (table, lat, long, intensity, Event id)

Damage Id = construction(code), occ (code), year of build (Band 1-5), stories (Band 1-4) ---> Damage ID




Panding Work:
	- PPT GIT
	


































