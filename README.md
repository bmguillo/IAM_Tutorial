# IAM Step by Step Tutorial 

## 
* Setting up IAM Access Groups & Resource Groups
* Provisioning New IAM-Enabled Services & Exporting/Importing Data 
* Migration of Services from Cloud Foundry Orgs/Spaces to Resource Groups within an IBM Cloud Account

### Reason for Migration:
- Watson service use of the CF org/space access model is being deprecated on October 30, 2019.The IBM Watson Group is         aligning with the larger IBM Cloud strategy for account organization and access control to service instances. This           involves enabling Identity and Access Management (IAM) and Resource Groups

### Best Practices brainstorming prior to IAM setup:<br>
- Think about the project in your organization you wish to organize in the context of IAM.<br>
- Think about the platform and infrastructure resources(users & services) you will use for this project<br>
- Think about the region(s) you will deploy the environment/services<br>
- Think about the users who will need various levels of access to work on this project & their responsibilities<br>
- Think about DevOps architecture patterns, delivery & sample environments you will need such as: development, testing,       staging, production<br>

### Migration Path Order(Recommended):<br>
- Lite instances/services(if you are on the Lite plan, you will have only one default RG called “default”)
- Standard instances/services (non production:development,testing,staging)
- Standard instances/services (production)*
- Premium instances/services (non production:development, testing,staging)
- Premium instances/services (production)*

### Access Policy/Resource Group Considerations
- Platform access for users to add to access policies, create a skill, provision new instances, bind services such as         Cloudant
- Recommended to create an access group that contain a specific set of users so that you can assign the access                 group(permissions) to the resource group which contain the resources you want them all to have access all at once to e.g.   devs https://cloud.ibm.com/docs/iam?topic=iam-userroles
- Only the account owner can create resource groups and administrators can create access groups
- Resource Groups cannot be deleted because they are tied to billing and you also cannot change names


### Code Refactoring Considerations Prior to Migration:
- Update the environment files with the new authentication(username/pw to api key and workspace id/skill id), endpoints
- Update the SDK to a new SDK that manages tokens.
- Code changes to SOE to ingest new authentication.

### Best Practices:
- If you do not already have an appropriate DevOps pipeline style organization/naming convention for CF services, it is recommended when setting up IAM.
   * CF space to RG replacement/mapping: projectname-dev-CF --> projectname-dev-RG
   * projectname-dev-RG, projectname-testing-RG, projectname-staging-RG, projectname-production-RG
   * this will ensure isolation so no mistaken what environment the users are working in
   * access groups: devs(users only have access to dev resources), operators(users only have access to prod resources),          testers(users only have access to test resources), but you can assign a user to multiple access groups
- Report issues with PUP and specifically there is an issue with missing migration icons for some services like Cloudant:      https://github.ibm.com/Bluemix/core-dev/issues/7651 



### Pre-requisite #1: Create Resource Group(s) & Assign resource group & resource access to developers

![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/1.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/2.png)
   
### Pre-requisite #2: Assign access within access group via access policies for the team

-	Access groups can be (devs, testers) 
- Add users to assign to the access group
-	Assign users
-	Access policies

![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/3.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/4.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/5.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/6.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/7.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/8.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/9.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/10.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/11.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/12.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/13.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/14.png)


### Let’s explore the old (console.ibm.com) vs. new cloud.ibm.com and migrate instances to RG or provision new instances using RG:


1.a	Provision new instances of a service utilizing RG
  
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/15.png)

1.b   Export workspace JSON from old CF service instance / Import JSON into new service instance

or 

2.	Within the old console.ibm.com I have several CF Services that have the option to migrate to a RG & - CF Applications do not get migrated, only CF Services ![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/16.png)  from the Dashboard

![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/17.png)

3.	Let’s now take a look at the new console, cloud.ibm.com within the Dashboard click View Resources then click on Cloud Foundry Services & you should see the same migrate icon
 
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/18.png)
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/19.png) 



4.	Click the Migrate link after hovering over Migrate icon or choose to utilize the breadcrumb icon--> migrate to resource group![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/20.png)   




5.	Click continue on this menu ![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/21.png)
6.	Choose a resource group to migrate your service to then click migrate:  
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/22.png)
7.	Click done on migrate successful popup message
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/23.png)
8.	There is no longer a migrate icon next to the service instance in the resource list:
![test](https://github.com/bmguillo/IAM_Tutorial/blob/master/img/24.png)
 





