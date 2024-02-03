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
	- S3 to lambda, SNS, SQS and EventBridge etc, using event bridge can add mutiple functionality
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
	- If primary failed the go for second origin, (s3 bucket or EC2 instance as origin)

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
	- s3 cannot worked with file system

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
	- Env files (bulk) - Amazon s3
	
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
	- you can use lifecycle policy for old version also send s3 for prevent 

Elastic Beanstalk Extensions:
	- zip file need deploy on Elastic Beanstalk
	- .ebextensions/  should be in root directry
	- YAML / JSON format
	- .config prefix file inside the .ebextensions/ folder
	- once .ebextensions/ deleted you all env deleted
	
Elastic Beanstalk Under the hood:
	- Elastic Beanstalk relies on cloudformation
	- use case: You can define cloudformation resource in you .ebextensions/ files for any resource like s3, ElastiCache etc


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
		









Hi team, Yesterday I did the hands-on Geospatial Analytic, Also Attended Interactive session on DataQuality & Geospatial, also attened the Verisk research annual meeting in which they talked about how are adding more data in the research model and talked about the new york data, 

And For today I'm planning to work on the GITHUB PPT & also revised touch stone concepts.




Tpin: 043263 papa 

It mainly consists in the capability of 


18/1/2024 : Done
	EC2 Instance Storage
	AWS Fundamentals : ELB + ASG
	AWS Fundamentals : RDS + Aurora + ElastiCache
	
19/1/2024: Done
	Route 53
	VPC Fundamentals

20/1/2024: done
	Amazon S3
	AWS CLI, SDK, IAM Roles & Policies
	Advance Amazon S3
	Amazon S3 security
	
21/1/2024: done
	Cloudfornt
	
22/1/2024:  Done
	ECS, ECR & Fargate - Docker in AWS

23/1/2024: 
	AWS Elastic Bean stalk
	AWS cloudformation
	
24/1/2024: office
	AWS Integration & Messaging: SQS, SNS & Kinesis
	
25/1/2024:
	AWS Monitoring & audit

26/1/2024:
	Serverless: lambda
	AWS Serverless: DynamoDB
	
27/1/2024: 
	AWS Serverless: Apigatway
	AWS CICD

28/1/2024: 	
	AWS Sererless: SAM
	CDK
	Cognito User Pools
	Other Serverless: Step function & AppSync
	
29/1/2024: office 
	Advanced Identity
	AWS security & Encryption
	AWS other Services
	
30/1/2024 - 31/1/2024 Extra-day for compatible remaining topice if any left

1 - exam by udemy
2 - exam by aws test / mock test any paper or etc

3 to 7 revision 
8-9 exam date
