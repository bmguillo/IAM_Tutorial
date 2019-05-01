# IAM Step by Step Tutorial - Watson Assistant

* Setting up IAM Access Groups & Resource Groups
* Provisioning New IAM-Enabled Services & Exporting/Importing Data 
* Migration of Services from Cloud Foundry Orgs/Spaces to Resource Groups within an IBM Cloud Account                         https://cloud.ibm.com/docs/services/assistant?topic=watson-migrate

### Reason for Migration:
- Watson service use of the CF org/space access model is being deprecated on October 30, 2019.The IBM Watson Group is                                             aligning with the larger IBM Cloud strategy for account organization and access control to service instances. This           involves enabling Identity and Access Management (IAM) and Resource Groups

### Best Practices brainstorming prior to IAM setup:<br>
- Think about the project in your organization you wish to organize in the context of IAM.<br>
- Think about the platform and infrastructure resources(users & services) you will use for this project<br>
- Think about the region(s) you will deploy the environment/services<br>
- Think about the users who will need various levels of access to work on this project & their responsibilities<br>
- Think about DevOps architecture patterns, delivery & sample environments you will need such as: development, testing,                                                                             staging, production<br>
- If you do not already have an appropriate DevOps pipeline style organization/naming convention for CF services, it is                             recommended when setting up IAM.
   * CF space to RG replacement/mapping: projectname-dev-CF --> projectname-dev-RG
   * projectname-dev-RG, projectname-testing-RG, projectname-staging-RG, projectname-production-RG
   * this will ensure isolation so no mistaken what environment the users are working in
   * access groups: devs(users only have access to dev resources), operators(users only have access to prod resources),                                           testers(users only have access to test resources), but you can assign a user to multiple access groups
- Report issues with PUP and specifically there is an issue with missing migration icons for some services like Cloudant:      https://github.ibm.com/Bluemix/core-dev/issues/7651 

### Migration Path Order(Recommended):<br>
- Lite instances/services(if you are on the Lite plan, you will have only one default RG called “default”)
- Standard instances/services (non production:development,testing,staging)
- Standard instances/services (production)*
- Plus instances/services (non production:development,testing,staging)
- Plus instances/services (production)*
- Premium instances/services (non production:development, testing,staging)
- Premium instances/services (production)*

### Access Policy/Resource Group Considerations
- Platform access for users to add to access policies, create a skill, provision new instances, bind services such as         Cloudant
- Recommended to create an access group that contain a specific set of users so that you can assign the access                 group(permissions) to the resource group which contain the resources you want them all to have access all at once to e.g.   devs https://cloud.ibm.com/docs/iam?topic=iam-userroles
- can only have one instance/slot per RG
- Only the account owner can create resource groups and administrators can create access groups
- Resource Groups cannot be deleted because they are tied to billing and you also cannot change names

### Code Refactoring Considerations Prior to Migration:
- Update the environment files with the new authentication(username/pw to api key and workspace id/skill id), endpoints
- Update the SDK to a new SDK that manages tokens.
- Code changes to SOE to ingest new authentication.

### Parallel Testing Considerations
- Create a from(state) --> to(state) diagram to communicate to stakeholders what has been completed, what is left to be                                                                         completed
- Each step of the process (code refactoring step, migration of non prod instance 1 etc. ) should be tested & assess before continuing on with the process
- CF instance becames an alias pointing to the IAM-enabled instance indicated by chainlink icon, should be able to test both CF credentials and IAM
- Switch users to the new IAM-enabled instances
- Run CF/IAM enabled instances in parallel until behavior is expected then drain users off

## Step by Step Walkthrough of IAM Process in IBM Cloud

### Pre-requisite #1: Create Resource Group(s) & Assign resource group & resource access to users
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/resourcegroup.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/resourcegroupcreation.png)

   
### Pre-requisite #2: Assign access within access group via access policies for the team
-	Access groups can be (developers, testers) 
- Add users to assign to the access group
-	Assign users to access policies

![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/IAM.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/accessgroupchg.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/accessgroupcreation.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/addusers.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/accesspolicies.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/11chg.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/14.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/assignrg&ratodev.png)

### Let’s explore cloud.ibm.com and provision new IAM-enabled instances(recommended path for production) and migrate non - prod instances to IAM:

## Production Service Instances
1.	Provision new instances of a service utilizing RG
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/provnewserv1.png)

2.	Create new Watson Assistant(s) & skill(s)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/provnewserv2.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/provnewserv3.png)

3. Export skill JSON from old CF service(Watson Assistant) & Import into new IAM-enabled RG service(Watson Assistant)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/provnewserv4.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/provnewserv5.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/provnewserv6.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/provnewserv7.png)


or 

## Non-Production Service Instances
1.	Within the IBM Cloud Dashboard click Cloud Foundry Services & you should see the migrate icon
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/watsonassistantmigrate.png)

2.	Click the Migrate link after hovering over Migrate icon or choose to utilize the breadcrumb icon--> migrate to resource group![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/20.png)   

3.	Choose a resource group to migrate your service to then click migrate and click done on migrate successful popup, service should now be found under "Services" and should not have a migrate icon
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/migrate1a.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/migrate2.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/migrate3.png)







