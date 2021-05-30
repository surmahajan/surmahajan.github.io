# Security

1. Visibility: What assets you have? 
    AWS Config allows us to discover all our assets within AWS. 
2. Auditability: 
    CloudTrail - records all api calls
3. Controllability: Is my data controlled?
    AWS KMS (multi-tenant)
    AWS CloudHSM (dedicated hardware)
4. Agility: How quickly can we adapt to changes?
    CloudFormation
    AWS Elastic Beanstalk
5. Automation: Are our processes repeatable?
    AWS OpsWorks
    AWS CodeDeploy
6. Scale
7. Other services: IAM, CloudWatch, Trusted Advisor
---
AWS Security responsibilities (Security of the cloud)
    - Global Infrastructure
    - Hardware, Software, Networking, Facilities
    - Managed Services (S3, DynamoDB)

Customer Security responsibilities (Security in the cloud)
    - Infrasrtucture as a Service (EC2)
    - Upgrades, Security patches, 
    - Configuration of AWS provided firewall (NaCLs)
    - Client side data encryption, Data integrity authentication
    - Server side encryption
    - Network traffic protection  

