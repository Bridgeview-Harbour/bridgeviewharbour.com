# Bridgeview Harbour
www.bridgeviewharbour.com


## Website Infrastruture

### Domain Registration
the .bridgeviewharbour.com domain is registered via [Amazon Web Services Route 53 Domain Registration Service](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar.html)
The cost of registration is $12 per calendar year.
This service provides private registration and integrates with other AWS Services. 


### DNS Hosted Zone
The DNS Hosted Zone for bridgeviewharbour.com is owned by [Amazon Web Services Routre 53](https://aws.amazon.com/route53/)
Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service and is fully compliant with IPv6 and DNSSEC. Use of Route 53 allows automatic integration with other AWS Services such as AWS Certificate Manager (ACM), Elastic Load Balancing (ELB), and Amazon Cloud Front CDN.  Additionally AWS's globally located data centers and edge locations provide geo-weighted IP resolution for public websites, this means users will be routed to the closest edge location hosting your content reducing latency and improving customer page load times. 

Route53 will be used to manage hosted zones for all Bridgeview Harbour Domains including bridgeviewharbour.com, porthenryweather.com, and lakechamplainweather.com.

### Content Distribution
Amazon CloudFront will be used to distribute bridgeviewharbour.com to North American edge locations. Distribution to these geographically diverse data centers ensures optimal customer experience and faster page load times when compare to traditional single origin hosting. Intelligent DNS Geo routing will provide resolution to the nearest edge location when requesting the site. 

### Security
As of January 2021, bridgeviewharbour.com will only be served via TLS 1.2 or later per [SSL Labs Deployment Recommendations](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices) which will help with Search Engine Optimization. Enforcement of Secure Cypers and HTTPS is not just good practice, it impacts Search Engine Ranking.  In 2018 Google announced it would be begin ranking unsecure websites lower in search results and [marking them as Not Secure](https://security.googleblog.com/2018/02/a-secure-web-is-here-to-stay.html) within the Google Chrome Browser


### Continuous Deployment Pipeline
Code changes to the production Bridgeview Harbour website will be performed and approved via Git Pull Request to the Master Branch of this Repository. 
Merge and Pull requests to the master branch will be reviewed and approved. Upon Approval and successful merging of branches Amazon CodeBuild will, via webhook to this repo, package the new code and deploy it to the production S3 Bucket hosting the code.  Amazon CloudFront will be alerted to the change in code base upon the next public request to the site.  When cloudfront Diffs the cached checksum against the checksum of the new Origin and sees a difference, cloudfront will automatically pull the new origin and Cached it in the required edge locations where requests are being serviced. 
