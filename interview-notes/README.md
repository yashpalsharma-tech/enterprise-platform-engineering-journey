

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
