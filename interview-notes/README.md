

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

AWS Route 53 Interview Questions

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
