

## Interview Questions

**AWS**

Q1. What is an AWS Region?

Q2. What is the difference between an Availability Zone and a Region?

Q3. Why do companies deploy applications across multiple AZs?

Q4. What is an Edge Location?

Q5. Which AWS service uses Edge Locations?

Q6. What is the difference between High Availability and Disaster Recovery?

Q7. What is a Cache Hit?

Q8. What is a Cache Miss?

Q9. Examples for statis cache files?

Q10. What is IAM?

Q11. What is the difference between Authentication and Authorization?

Q12. What is an IAM User?

Q13. What is an IAM Group?

Q14. What is an IAM Policy?

Q15. What is an IAM Role?

Q16. What is the Principle of Least Privilege?

Q17. Why should the AWS Root User not be used for daily activities?

Q18. What are temporary credentials, and why are they preferred over long-term access keys?

Q19. What is an Auto Scaling Group?

Q20. What is the difference between Minimum, Desired, and Maximum Capacity?

Q21. What are Dynamic, Scheduled, and Predictive Scaling?

Q22. What happens when an Auto Scaling Group (ASG) reaches its maximum capacity?

Q23. Which Amazon CloudWatch metrics can trigger Auto Scaling?

Q24. What is an Auto Scaling Group (ASG)?

Q25. What are the three Auto Scaling policies?

Q26. What is the difference between Dynamic, Scheduled, and Predictive Scaling?

Q27. How does Amazon CloudWatch work with Auto Scaling?

Q28. Explain the architecture of a highly available web application on AWS.

Q29. What happens if one EC2 instance becomes unhealthy?

Q30. Why should an Auto Scaling Group (ASG) span multiple Availability Zones (AZs)?

Q31. What is the difference between a Launch Template and an Amazon Machine Image (AMI)?

Q32. What is Elastic Load Balancer (ELB)?

Q33. Why do we need a Load Balancer?

Q34. What are the four types of AWS Load Balancers?

Q35. What is the difference between ALB and NLB?

Q36. How does an ALB determine whether an EC2 instance is healthy?

Q37. Does ALB use CloudWatch for Health Checks?

Q38. What happens if one EC2 instance becomes unhealthy?

Q39. What happens if all EC2 instances become unhealthy?

Q40. What happens if one ALB node fails?

Q41. Can ALB protect against an entire AWS Region failure?

Q42. How do Route 53 and ALB work together?

Q43. What is Elastic Load Balancer?

Q44. Why do we need a Load Balancer?

Q45. What are the four types of AWS Load Balancers?

Q46. What is the difference between ALB and NLB?

Q47. What is a Target Group?

Q48. What is an ALB Listener?

Q49. What is a Listener Rule?

Q50. How does an ALB determine which Target Group should receive a request?

Q51. What is Path-Based Routing?

Q52. What is Host-Based Routing?

Q53. What happens when an ALB request does not match any specific Listener Rule?

Q54. How does an ALB perform Health Checks?

Q55. Does ALB use CloudWatch to determine whether an EC2 instance is healthy?

Q56. What happens when an EC2 instance becomes unhealthy?

Q57. How does ALB work with an Auto Scaling Group?

Q58. What happens if all EC2 instances in a Target Group become unhealthy?

Q59. What is Blue/Green Deployment?

Q60. How can an ALB be used for Blue/Green Deployment?

Q61. How would you rollback a failed Blue/Green deployment?

Q62. What are Sticky Sessions?

Q63. Why can Sticky Sessions be a problem in a highly scalable application?

Q64. What is a Stateless Application?

Q65. Why are Stateless Applications preferred in cloud environments?

Q66. How can session information be stored when using a Stateless Application?

Q67. Can an ALB protect an application from an entire AWS Region failure?

Q68. How can Route 53 be used together with ALB for Multi-Region Disaster Recovery?

Q69. What is the difference between Path-Based Routing and Host-Based Routing?

## AWS CloudFront Interview Questions

Q70. What is Amazon CloudFront?

Q71. Why do we need CloudFront?

Q72. What is a CDN?

Q73. What is an Edge Location?

Q74. What is a CloudFront Distribution?

Q75. What is an Origin in CloudFront?

Q76. What is a Cache Hit?

Q77. What is a Cache Miss?

Q78. What happens during a Cache Miss?

Q79. What is TTL in CloudFront?

Q80. How does TTL affect CloudFront caching?

Q81. What is CloudFront Cache Invalidation?

Q82. When would you use CloudFront Cache Invalidation?

Q83. What type of content is suitable for CloudFront caching?

Q84. Should sensitive dynamic data such as payroll information be cached?

Q85. What are CloudFront Cache Behaviors?

Q86. Why would you configure different Cache Behaviors for static and dynamic content?

Q87. How does CloudFront work with Amazon S3?

Q88. How can you prevent public access to an S3 bucket while allowing CloudFront to access it?

Q89. What is Origin Access Control (OAC)?

Q90. What is the difference between OAC and OAI?

Q91. How does CloudFront work with an Application Load Balancer?

Q92. What happens when CloudFront receives a Cache Hit?

Q93. What happens when CloudFront receives a Cache Miss?

Q94. Why would you put CloudFront in front of an ALB?

Q95. What is the difference between CloudFront and ALB?

Q96. Can CloudFront cache dynamic content?

Q97. How would you configure CloudFront for a PeopleSoft application?

Q98. Which PeopleSoft content would you cache using CloudFront?

Q99. Why should login and payroll responses generally not be cached as shared content?

Q100. What happens if an object changes at the origin before its CloudFront TTL expires?

Q101. How would you immediately serve a new version of an object from CloudFront?

Q102. What happens if users access the ALB directly instead of going through CloudFront?

Q103. How can you design an architecture to prevent users from bypassing CloudFront?

Q104. What is the difference between CloudFront Edge Locations and an AWS Region?

Q105. How does CloudFront reduce network latency?

Q106. How does CloudFront reduce load on the origin?

Q107. Can CloudFront protect an application from an entire AWS Region failure?

##****AWS Route 53 Interview Questions**

Q108. What is Amazon Route 53?

Q109. What is DNS?

Q110. Why do we need DNS?

Q111. What is a Route 53 Hosted Zone?

Q112. What is the difference between a Public and Private Hosted Zone?

Q113. What is an A record?

Q114. What is an AAAA record?

Q115. What is a CNAME record?

Q116. What is an Alias record?

Q117. What is the difference between CNAME and Alias?

Q118. Why would you use an Alias record for an ALB?

Q119. What are the major Route 53 routing policies?

Q120. What is Simple Routing?

Q121. What is Weighted Routing?

Q122. What is Latency-Based Routing?

Q123. What is Failover Routing?

Q124. What is Geolocation Routing?

Q125. What is the difference between Weighted and Latency-Based Routing?

Q126. What is the difference between Geolocation and Latency-Based Routing?

Q127. What is a Route 53 Health Check?

Q128. How does Route 53 Health Check work?

Q129. How does Health Check work with Failover Routing?

Q130. How would you configure Route 53 for primary and DR environments?

Q131. How would you send 90% of traffic to Singapore and 10% to Sydney?

Q132. How would you gradually migrate traffic from an old application to a new application?

Q133. How would you route users to the AWS Region with the lowest latency?

Q134. How would you route users based on their geographic location?

Q135. How would you configure Route 53 with an ALB?

Q136. How would you configure Route 53 with CloudFront?

Q137. What happens when the primary endpoint in a Failover configuration becomes unhealthy?

Q138. What is the difference between a DNS record and a Route 53 routing policy?

Q139. Can Route 53 route traffic directly to an ALB?

Q140. Why should you avoid using the underlying ALB IP addresses in DNS configuration?

Q141. What is the difference between Active/Passive and Active/Active architectures in Route 53?

**Amazon S3 Interview Questions**

Q142. What is Amazon S3?

Q143. What is the difference between an S3 bucket and an S3 object?

Q144. Are S3 bucket names globally unique?

Q145. What are the major S3 storage classes?

Q146. What is S3 Standard?

Q147. What is S3 Standard-IA?

Q148. What is the difference between S3 Standard and S3 Standard-IA?

Q149. What is S3 One Zone-IA?

Q150. When would you choose One Zone-IA instead of Standard-IA?

Q151. What is S3 Intelligent-Tiering?

Q152. When should you use S3 Intelligent-Tiering?

Q153. What is S3 Glacier Instant Retrieval?

Q154. What is S3 Glacier Flexible Retrieval?

Q155. What is S3 Glacier Deep Archive?

Q156. What is the difference between Glacier Instant Retrieval, Flexible Retrieval, and Deep Archive?

Q157. Which storage class would you use for long-term compliance records that are almost never accessed?

Q158. What is an S3 Lifecycle Policy?

Q159. How can Lifecycle Policies reduce S3 storage costs?

Q160. What is the difference between S3 Lifecycle Policies and Intelligent-Tiering?

Q161. Can Lifecycle Policies automatically delete objects?

Q162. Can Lifecycle Policies manage noncurrent object versions?

Q163. What is S3 Versioning?

Q164. How does S3 Versioning protect against accidental overwrites?

Q165. What happens when you delete an object from a version-enabled S3 bucket?

Q166. What is an S3 delete marker?

Q167. Can a specific version of an S3 object be permanently deleted?

Q168. What is server-side encryption in S3?

Q169. What is SSE-S3?

Q170. What is SSE-KMS?

Q171. What is SSE-C?

Q172. What is the difference between SSE-S3 and SSE-KMS?

Q173. When would you choose SSE-KMS instead of SSE-S3?

Q174. What is the difference between encryption at rest and encryption in transit?

Q175. What is S3 Block Public Access?

Q176. Why should sensitive S3 buckets have Block Public Access enabled?

Q177. What is an S3 Bucket Policy?

Q178. What is the difference between an IAM Policy and an S3 Bucket Policy?

Q179. How would an EC2 instance securely access a private S3 bucket?

Q180. Why should an EC2 application use an IAM Role instead of storing AWS access keys?

Q181. How would you provide another AWS account read-only access to selected S3 objects?

Q182. What is S3 Cross-Region Replication?

Q183. What is Same-Region Replication?

Q184. What is the difference between CRR and SRR?

Q185. What prerequisite is required for S3 replication regarding Versioning?

Q186. What is S3 durability?

Q187. What is the difference between durability and availability?

Q188. What does 99.999999999% durability mean?

Q189. Can Amazon S3 be used for static website content?

Q190. When would you choose S3 instead of EC2 for a website?

Q191. How would you design a globally distributed static website using Route 53, CloudFront, and S3?

Q192. What is CloudFront Origin Access Control (OAC)?

Q193. How would you keep an S3 origin private while allowing CloudFront access?

Q194. What is an S3 Pre-Signed URL?

Q195. When would you use a Pre-Signed URL?

Q196. How would you provide temporary access to one private S3 object without making the bucket public?

Q197. How would you protect highly sensitive payroll documents stored in S3?

Q198. How would you automatically move S3 objects from Standard to Standard-IA and then Glacier?

Q199. Which storage class would you choose when access patterns are unknown or unpredictable?

Q200. Which Glacier storage class would you choose when archive data requires millisecond retrieval?

Q201. Which Glacier storage class would you choose when retrieval within minutes or hours is acceptable?

Q202. Which Glacier storage class would you choose for very rarely accessed long-term archives where retrieval can take hours?

**Amazon RDS Interview Question**s

Q203. What is Amazon RDS?

Q204. What are the benefits of using Amazon RDS?

Q205. What is the difference between running a database on RDS and EC2?

Q206. When would you choose a database on EC2 instead of RDS?

Q207. Which database engines are supported by Amazon RDS?

Q208. What is an RDS DB instance?

Q209. What is RDS Multi-AZ?

Q210. Why do we use Multi-AZ?

Q211. How does RDS Multi-AZ replication work?

Q212. What happens if the primary RDS instance fails in a Multi-AZ deployment?

Q213. Does the application need to change its database endpoint after Multi-AZ failover?

Q214. Is the classic Multi-AZ standby used for application read traffic?

Q215. What is an RDS Read Replica?

Q216. Why would you use a Read Replica?

Q217. What type of workload benefits from Read Replicas?

Q218. What is the difference between Multi-AZ and Read Replicas?

Q219. What is the difference between synchronous and asynchronous replication in the context of RDS?

Q220. Can you use Multi-AZ and Read Replicas together?

Q221. How would you design RDS for both high availability and read scalability?

Q222. What are RDS Automated Backups?

Q223. What is Point-in-Time Recovery?

Q224. How does RDS Point-in-Time Recovery work?

Q225. Does PITR overwrite the existing database?

Q226. What is an RDS Manual Snapshot?

Q227. What is the difference between Automated Backups and Manual Snapshots?

Q228. When would you take a Manual Snapshot?

Q229. How would you recover from an accidental database record deletion that happened 10 minutes ago?

Q230. Where should a production RDS database normally be placed in a VPC?

Q231. Why should RDS normally be placed in private subnets?

Q232. How should application servers securely connect to RDS?

Q233. How would you configure the RDS Security Group so only application servers can access it?

Q234. Why should you reference the application Security Group instead of allowing 0.0.0.0/0 on the database port?

Q235. How does RDS encryption at rest work?

Q236. Which AWS service manages encryption keys for RDS?

Q237. What happens to backups and snapshots when an RDS DB instance is encrypted?

Q238. How do you protect RDS database traffic in transit?

Q239. Why should applications use an RDS DNS endpoint rather than hard-coded database IP addresses?

Q240. What is Amazon RDS Proxy?

Q241. What problem does RDS Proxy solve?

Q242. How does database connection pooling work with RDS Proxy?

Q243. Why can RDS Proxy be useful with AWS Lambda?

Q244. What is the difference between RDS Proxy and a Read Replica?

Q245. Your RDS database has too many SELECT queries. What would you do?

Q246. Your RDS database needs automatic failover if an AZ fails. What would you do?

Q247. Your application is creating too many database connections. What would you do?

Q248. You need to restore the database to a specific time before an accidental deletion. What would you use?

Q249. You need to take a database backup immediately before a major upgrade and retain it until manually deleted. What would you use?

Q250. How would you design a highly available RDS architecture across multiple Availability Zones?

Q251. How would you design a production application using Route 53, ALB, Auto Scaling, EC2 and RDS?

Q252. How would you combine Multi-AZ, Read Replicas, Security Groups and KMS for a business-critical application?

AWS VPC Advanced Networking Interview Questions

Q253. What is an Internet Gateway?

Q254. What is required for an EC2 instance to communicate directly with the internet?

Q255. Does assigning a public IPv4 address automatically make a subnet public?

Q256. What makes a subnet a public subnet?

Q257. What is a VPC Route Table?

Q258. What does the local route in a VPC Route Table represent?

Q259. What does 0.0.0.0/0 represent?

Q260. What is the difference between routing for a public subnet and a private subnet?

Q261. What is a NAT Gateway?

Q262. Why do private EC2 instances use a NAT Gateway?

Q263. Where should a public NAT Gateway be deployed?

Q264. What is the difference between an Internet Gateway and a NAT Gateway?

Q265. Can internet clients initiate connections to private EC2 instances through a NAT Gateway?

Q266. Why would you deploy one NAT Gateway per Availability Zone?

Q267. What happens if private subnets in multiple AZs depend on a single NAT Gateway and that NAT path becomes unavailable?

Q268. What is a VPC Endpoint?

Q269. Why would you use a VPC Endpoint?

Q270. What is a Gateway VPC Endpoint?

Q271. Which AWS services commonly use Gateway Endpoints?

Q272. How would a private EC2 instance access Amazon S3 without using a NAT Gateway?

Q273. What is an Interface VPC Endpoint?

Q274. What is AWS PrivateLink?

Q275. How do Interface Endpoints use Elastic Network Interfaces?

Q276. What is the difference between a Gateway Endpoint and an Interface Endpoint?

Q277. Can Security Groups be associated with Interface Endpoints?

Q278. What is VPC Peering?

Q279. How do two VPCs route traffic through a VPC Peering connection?

Q280. Is VPC Peering transitive?

Q281. If VPC-A peers with VPC-B and VPC-B peers with VPC-C, can VPC-A automatically communicate with VPC-C?

Q282. What is AWS Transit Gateway?

Q283. When would you use Transit Gateway instead of VPC Peering?

Q284. What is a hub-and-spoke network architecture?

Q285. What is the difference between VPC Peering and Transit Gateway?

Q286. What is the difference between a Security Group and a Network ACL?

Q287. Why is a Security Group called stateful?

Q288. Why is a Network ACL called stateless?

Q289. Can Security Groups contain explicit Deny rules?

Q290. Can Network ACLs contain Deny rules?

Q291. At what level is a Security Group applied?

Q292. At what level is a Network ACL applied?

Q293. How are NACL rules evaluated?

Q294. What is a Bastion Host?

Q295. Why would you use a Bastion Host?

Q296. Where should a Bastion Host traditionally be placed?

Q297. How would you restrict SSH access through a Bastion Host?

Q298. What AWS service can provide administrative access to EC2 without opening inbound SSH port 22?

Q299. What is longest prefix match in AWS routing?

Q300. If /16, /24 and /0 routes all match a destination, which route is selected?

Q301. Why would S3 traffic use a Gateway Endpoint instead of the default route to a NAT Gateway?

Q302. How would you design a highly available VPC across two Availability Zones?

Q303. Where would you place an internet-facing ALB in a production VPC?

Q304. Where would you place application EC2 instances?

Q305. Where would you place an RDS production database?

Q306. How would private EC2 instances access the internet while remaining private?

Q307. How would you prevent heavy S3 traffic from passing through NAT Gateways?

Q308. How would you allow only the application tier to access RDS?

Q309. Design a production VPC containing an ALB, Auto Scaling Group, NAT Gateways, S3 Gateway Endpoint and RDS Multi-AZ.

## AWS CloudWatch, CloudTrail and SNS Interview Questions

Q310. What is Amazon CloudWatch?

Q311. What are CloudWatch Metrics?

Q312. Which EC2 metrics are available through standard CloudWatch monitoring?

Q313. Is EC2 memory utilization available as a standard EC2 CloudWatch metric?

Q314. How would you monitor memory utilization on an EC2 instance?

Q315. What is the CloudWatch Agent?

Q316. What types of metrics can the CloudWatch Agent collect?

Q317. How would you collect application logs from an EC2 instance?

Q318. What is CloudWatch Logs?

Q319. What is a CloudWatch Log Group?

Q320. What is a CloudWatch Log Stream?

Q321. What is a CloudWatch Alarm?

Q322. What are the three CloudWatch Alarm states?

Q323. What does the ALARM state mean?

Q324. What does INSUFFICIENT_DATA mean?

Q325. How would you create an alert when EC2 CPU exceeds 80%?

Q326. What is Amazon SNS?

Q327. How do CloudWatch Alarms and SNS work together?

Q328. What is an SNS Topic?

Q329. Which types of subscribers can receive SNS messages?

Q330. How would you send an email notification when a CloudWatch Alarm enters the ALARM state?

Q331. What is a CloudWatch Dashboard?

Q332. Why would an operations team use CloudWatch Dashboards?

Q333. How would you monitor multiple EC2, ALB and RDS resources from one screen?

Q334. Which CloudWatch metrics can help troubleshoot ALB 5xx errors?

Q335. What is the difference between HTTPCode_ELB_5XX_Count and HTTPCode_Target_5XX_Count?

Q336. If HTTPCode_ELB_5XX_Count is zero but HTTPCode_Target_5XX_Count is high, where would you investigate first?

Q337. Which RDS metrics can be monitored through CloudWatch?

Q338. How would you monitor RDS DatabaseConnections?

Q339. Does RDS require a CloudWatch Agent to publish standard RDS metrics?

Q340. What is AWS CloudTrail?

Q341. What type of activity does CloudTrail record?

Q342. How would you determine who terminated an EC2 instance?

Q343. How would you determine who modified a Security Group?

Q344. What is the difference between CloudWatch and CloudTrail?

Q345. Which service would you use to investigate AWS API activity?

Q346. Which service would you use to investigate high EC2 CPU utilization?

Q347. What is a CloudWatch Logs Metric Filter?

Q348. How would you count ERROR occurrences in application logs?

Q349. How would you create an alarm based on ERROR occurrences in CloudWatch Logs?

Q350. Explain the flow from CloudWatch Logs to an SNS notification using a Metric Filter.

Q351. How would you Auto Scale EC2 instances based on memory utilization?

Q352. Why is the CloudWatch Agent required for memory-based EC2 scaling?

Q353. How do CloudWatch Metrics, Alarms and SNS work together?

Q354. How would you design monitoring for an EC2 application behind an ALB?

Q355. How would you monitor EC2 CPU, memory and application logs?

Q356. How would you monitor ALB response errors?

Q357. How would you monitor RDS CPU, connections and storage?

Q358. How would you design centralized monitoring for EC2, ALB and RDS?

Q359. How would you combine CloudWatch and CloudTrail for production monitoring and auditing?

Q360. Design an alerting solution where application ERROR events trigger an operations email.

Q361. Your EC2 CPU reaches 95%, application logs show database errors and someone changes the Security Group. Which AWS services would you use to investigate each issue?

Q362. Explain a complete production monitoring architecture using CloudWatch Metrics, CloudWatch Agent, CloudWatch Logs, CloudWatch Alarms, SNS, Dashboards and CloudTrail.

## Amazon SQS, SNS and Event-Driven Architecture Interview Questions

Q363. What is Amazon SQS?

Q364. Why do we use SQS?

Q365. What does decoupling mean in an SQS architecture?

Q366. What is a Producer in SQS?

Q367. What is a Consumer in SQS?

Q368. How does SQS help handle sudden traffic spikes?

Q369. What happens to messages if an SQS consumer becomes unavailable?

Q370. What is SQS Visibility Timeout?

Q371. Why does SQS make a received message temporarily invisible?

Q372. What happens when the Visibility Timeout expires before the message is deleted?

Q373. What happens if a consumer crashes while processing an SQS message?

Q374. Why should the Visibility Timeout normally be longer than the expected processing time?

Q375. What can happen if processing takes four minutes but Visibility Timeout is one minute?

Q376. Does receiving an SQS message automatically delete it?

Q377. When should a consumer delete an SQS message?

Q378. What is an idempotent consumer?

Q379. Why is idempotency important with SQS Standard Queues?

Q380. What is the SQS Message Retention Period?

Q381. What is the difference between Message Retention and Visibility Timeout?

Q382. What is SQS Long Polling?

Q383. Why would you enable Long Polling?

Q384. How does Long Polling reduce empty SQS responses?

Q385. What is an SQS Dead-Letter Queue?

Q386. Why would you use a Dead-Letter Queue?

Q387. What is a redrive policy?

Q388. What does maxReceiveCount control?

Q389. What happens when a message reaches maxReceiveCount?

Q390. Does a Dead-Letter Queue automatically fix failed messages?

Q391. What is an SQS Standard Queue?

Q392. What delivery behavior does a Standard Queue provide?

Q393. Can Standard Queues deliver duplicate messages?

Q394. What ordering guarantee does an SQS Standard Queue provide?

Q395. What is an SQS FIFO Queue?

Q396. When would you choose FIFO instead of Standard?

Q397. What is MessageGroupId in an SQS FIFO Queue?

Q398. How does MessageGroupId allow different groups to process independently?

Q399. What is the difference between SQS Standard and FIFO Queues?

Q400. How would you process banking transactions in strict order for each bank account?

Q401. How would you scale EC2 workers based on an SQS backlog?

Q402. Which SQS CloudWatch metric can indicate the approximate queue backlog?

Q403. What is ApproximateNumberOfMessagesVisible?

Q404. How can SQS, CloudWatch and Auto Scaling work together?

Q405. What is Amazon SNS?

Q406. What is the publish/subscribe model?

Q407. What is an SNS Topic?

Q408. Which types of subscribers can subscribe to SNS?

Q409. What is the difference between SNS and SQS?

Q410. When would you use SNS instead of SQS?

Q411. What is SNS fan-out?

Q412. How would you send one OrderCreated event to Payment, Inventory and Analytics?

Q413. Why would you use separate SQS queues behind an SNS Topic?

Q414. What happens if one subscriber service is temporarily unavailable in an SNS + SQS architecture?

Q415. Why is one shared SQS queue not appropriate when every service needs a copy of every event?

Q416. How does SNS + SQS provide both fan-out and decoupling?

Q417. Can each SQS queue in an SNS fan-out architecture have its own DLQ?

Q418. How would you design an e-commerce event architecture for Payment, Inventory and Analytics?

Q419. Explain the difference between Visibility Timeout, Message Retention, Long Polling and maxReceiveCount.

Q420. Design an SQS architecture that handles consumer failures without losing waiting messages.

Q421. Design an architecture where repeatedly failing messages are isolated for troubleshooting.

Q422. Design an Auto Scaling architecture where EC2 workers scale according to SQS queue depth.

Q423. Design a reliable event-driven architecture using SNS, SQS and DLQs for multiple independent services.

## AWS Lambda and API Gateway Interview Questions

Q424. What is AWS Lambda?

Q425. Why is AWS Lambda called serverless compute?

Q426. What are the main benefits of using AWS Lambda?

Q427. What is a Lambda function?

Q428. What is a Lambda trigger?

Q429. Give examples of AWS services that can trigger or act as event sources for Lambda.

Q430. How can S3 and Lambda work together?

Q431. How would you automatically process an image when it is uploaded to S3?

Q432. What is Amazon API Gateway?

Q433. How do API Gateway and Lambda work together?

Q434. How would you build a serverless REST/HTTP API?

Q435. Explain the architecture API Gateway → Lambda → DynamoDB.

Q436. What is a Lambda Execution Role?

Q437. Why should Lambda use an IAM role instead of hard-coded AWS access keys?

Q438. How would you allow a Lambda function to read objects from a private S3 bucket?

Q439. How would you allow Lambda to access DynamoDB?

Q440. What is a Lambda resource-based policy?

Q441. What is the difference between a Lambda Execution Role and a Lambda resource-based policy?

Q442. How would API Gateway receive permission to invoke a Lambda function?

Q443. What is the Lambda function timeout?

Q444. What is the maximum AWS Lambda execution timeout?

Q445. What happens when a Lambda function reaches its configured timeout?

Q446. When might Lambda not be suitable for a long-running workload?

Q447. How does the AWS Lambda pricing model differ conceptually from continuously running EC2 capacity?

Q448. What is Lambda concurrency?

Q449. Why can high Lambda concurrency cause problems for downstream systems?

Q450. What is Reserved Concurrency?

Q451. How can Reserved Concurrency help protect an RDS database?

Q452. What is Provisioned Concurrency?

Q453. What is a Lambda cold start?

Q454. How can Provisioned Concurrency reduce cold-start latency?

Q455. What is the difference between Reserved Concurrency and Provisioned Concurrency?

Q456. What are Lambda Environment Variables?

Q457. Why should application configuration be separated from Lambda code?

Q458. Where should sensitive credentials such as database passwords normally be stored?

Q459. How can Lambda and AWS Secrets Manager work together?

Q460. How can Lambda process messages from Amazon SQS?

Q461. What is the benefit of placing SQS between an application and Lambda?

Q462. How does SQS provide buffering for Lambda workloads?

Q463. Which Lambda metrics can be monitored using CloudWatch?

Q464. How would you monitor Lambda errors?

Q465. How would you notify an operations team when Lambda errors exceed a threshold?

Q466. Where can Lambda application logs be collected?

Q467. What is Lambda throttling?

Q468. What can happen when a Lambda function reaches its concurrency limit?

Q469. What is synchronous Lambda invocation?

Q470. Give an example of synchronous Lambda invocation.

Q471. What is asynchronous Lambda invocation?

Q472. What is the difference between synchronous and asynchronous Lambda invocation?

Q473. How is SQS event-source processing different from a direct asynchronous Lambda invocation?

Q474. Explain API Gateway → Lambda → DynamoDB as a serverless application architecture.

Q475. Design a serverless application that minimizes Lambda cold-start latency.

Q476. Design monitoring and alerting for a production Lambda application.

Q477. Design a complete serverless architecture using API Gateway, Lambda, IAM, DynamoDB, CloudWatch and SNS.

## Amazon DynamoDB Interview Questions

Q478. What is Amazon DynamoDB?

Q479. Why is DynamoDB called a serverless NoSQL database?

Q480. What is the difference between DynamoDB and Amazon RDS?

Q481. When would you choose DynamoDB instead of RDS?

Q482. What is a DynamoDB Table?

Q483. What is an Item in DynamoDB?

Q484. What is an Attribute in DynamoDB?

Q485. What is a DynamoDB Primary Key?

Q486. What is a Partition Key?

Q487. What is a simple primary key in DynamoDB?

Q488. What is a composite primary key?

Q489. What is a Sort Key?

Q490. Why would you use a Partition Key and Sort Key together?

Q491. How would you design a table where one customer can have many orders?

Q492. How would you design a DynamoDB table for IoT readings by device and timestamp?

Q493. What is a DynamoDB Query?

Q494. What is a DynamoDB Scan?

Q495. What is the difference between Query and Scan?

Q496. Why should Query generally be preferred over Scan when the access pattern supports it?

Q497. How can a Sort Key be used for range queries?

Q498. What is a DynamoDB Secondary Index?

Q499. What is a Global Secondary Index (GSI)?

Q500. When would you use a GSI?

Q501. Can a GSI use a different Partition Key from the base table?

Q502. Can a GSI be added after a DynamoDB table has been created?

Q503. What is a Local Secondary Index (LSI)?

Q504. What is the key difference between GSI and LSI?

Q505. Why must an LSI be defined when the DynamoDB table is created?

Q506. What is an Eventually Consistent Read?

Q507. What is a Strongly Consistent Read?

Q508. What is the difference between Eventually and Strongly Consistent Reads?

Q509. Does a GSI support Strongly Consistent Reads?

Q510. Do DynamoDB base tables support Strongly Consistent Reads?

Q511. Does an LSI support Strongly Consistent Reads?

Q512. What are the DynamoDB capacity modes?

Q513. What is DynamoDB On-Demand Capacity?

Q514. When would you choose On-Demand mode?

Q515. What is DynamoDB Provisioned Capacity?

Q516. What are RCU and WCU?

Q517. When would you choose Provisioned Capacity?

Q518. How can DynamoDB Auto Scaling work with Provisioned Capacity?

Q519. What is DynamoDB TTL?

Q520. When would you use TTL?

Q521. Does DynamoDB TTL guarantee deletion at the exact expiration time?

Q522. What are DynamoDB Streams?

Q523. Which item-level changes can DynamoDB Streams capture?

Q524. How do DynamoDB Streams and Lambda work together?

Q525. What is DynamoDB Accelerator (DAX)?

Q526. When would you use DAX?

Q527. What is DynamoDB Point-in-Time Recovery (PITR)?

Q528. What is the difference between PITR and an On-Demand Backup?

Q529. How is DynamoDB data encrypted at rest?

Q530. How does AWS KMS integrate with DynamoDB?

Q531. What are DynamoDB Global Tables?

Q532. When would you use DynamoDB Global Tables?

Q533. What is a hot partition or hot key in DynamoDB?

Q534. Why is high cardinality important when selecting a Partition Key?

Q535. Why might Country be a poor Partition Key if most traffic comes from one country?

Q536. How would you efficiently query an existing production table by an attribute that is not part of its current primary key?

Q537. Design a serverless application using API Gateway, Lambda and DynamoDB.

Q538. Design a production DynamoDB architecture using appropriate keys, GSI, Streams, TTL, DAX, PITR, KMS and capacity mode.
