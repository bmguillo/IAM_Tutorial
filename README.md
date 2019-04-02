# Step by Step Tutorial of Setting up IAM within an IBM Cloud Account

##Setting up IAM & Migrating Services from Cloud Foundry to Resource Groups/ Provisioning New Service to Utilize RG:


Best Practices brainstorming prior to IAM setup:<br>
•	Think about the project in your organization you wish to organize in the context of IAM.<br>
•	Think about the platform and infrastructure resources(users & services) you will use for this project<br>
•	Think about the region(s) you will deploy the environment/services<br>
•	Think about the users who will need various levels of access to work on this project & their responsibilities<br>
•	Think about DevOps architecture patterns, delivery & sample environments you will need such as: development, staging, testing, pre-production, production<br>


Hints/ Tips:
•	dev-project-CF space is the equivalent of dev-project-RG(Resource Group) logical grouping
•	RG replaces CF(Cloud Foundry) space 
•	Platform access: access for users to add to access policies, provision new instances, bind Cloudant; service access not implemented yet e.g. change intents, , change name of services
•	CF Applications do not get migrated, only CF Services 
•	If you are on the Lite plan, you will have only one default RG called “default”
•	Resource groups: The Services you want a specific set of users(access group) to all have access to. You set up your access group, define a policy for it and all the users obtain access at once.
•	Access group: specific set of users
•	Only the account owner can create resource groups and administrators can create access groups
•	Resource Groups cannot be deleted because they are tied to billing and you also cannot change names
•	There is a github to report issues with PUP and specifically there is an issue with missing migration icons for some services like Cloudant: https://github.ibm.com/Bluemix/core-dev/issues/7651


Pre-requisite #1: Create Resource Group(s) & Assign resource group & resource access to developers

   
Pre-requisite #2: Assign access within access group via access policies for the team
-	Access groups can be (devs, testers) 
-	Assign users
-	Access policies


 


   
 
 

 

Add users to assign to the access group
   
 


Access policies
 

  
 



 

 
   

 



Let’s explore the old (console.ibm.com) vs. new cloud.ibm.com and migrate instances to RG or provision new instances using RG:


1.	Provision new instances of a service utilizing RG
  

or 

2.	Within the old console.ibm.com I have several CF Services that have the option to migrate to a RG  from the Dashboard

 

3.	Let’s now take a look at the new console, cloud.ibm.com within the Dashboard click View Resources then click on Cloud Foundry Services & you should see the same migrate icon
 
 



4.	Click the Migrate link after hovering over Migrate icon or choose to utilize the breadcrumb icon migrate to resource group   




5.	Click continue on this menu 
6.	Choose a resource group to migrate your service to then click migrate:  
7.	Click done on migrate successful popup message
 
8.	There is no longer a migrate icon next to the service instance in the resource list:
 





