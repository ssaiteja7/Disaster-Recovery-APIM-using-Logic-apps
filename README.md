# Disaster-Recovery-APIM-using-Logic-apps

Azure API Management disaster recovery comes with premium pricing plan that’s very expensive. However, enterprises don’t necessarily require a premium plan just for DR. A cost effective solution to manage backup and restore automatically will suffice the need. Enterprises can leverage this with basic/standard version of API Management.

**Overview**
Ready to use solution to recover from availability problems that affect the region that hosts your API Management service.
Enterprise don’t necessarily require a premium tier just for DR. A cost-effective solution to manage backup and restore automatically will suffice the need. Enterprises can leverage 

**Usage Guidelines**
**Prerequisites:**
* Azure API Management
* Logic Apps
* Storage Account
* Traffic Manager
* Azure AD,
* Azure DevOps (Optional)

Readily available ARM Templates/Configurations to provision the services

**Technical Components :**
As a part of the solution we have covered following services to implement Azure API Management Disaster Recovery with standard Tier.
Azure API Management with standard tier in two different regions.
Azure Traffic Manager to distribute the load in case of DR situation.
Two Logic apps – for automation of backup from primary region and restore in secondary region of API Management
Storage account – for storing backup information of API Management primary
Azure AD application – to allow logic app provide authentication mechanism to make changes in API Management (through Service Principal concept).

**Architecture ** 

![image](https://user-images.githubusercontent.com/90609419/161036211-4494972d-8880-4b17-bf81-70c4023f821e.png)


**Implementation **

Logic app uses timer orchestration step to automatically trigger itself. logic app sends service principal details to Azure AD and then retrieves the authentication token.

Invoke API Management rest API with operation as backup

The operation starts copying data to storage account in other region

Post successful copy operation of backup; another logic app is triggered which restores the backup data in another API Management instance created in secondary region.

Post restore operation both API Management instances are now exactly identical. For example, in secondary API Management all policies, subscription key, APIs etc. will be same as primary API Management.

The request from end user/ application is received to traffic manager. Traffic manager is configured in failover mode with primary API Management as active and secondary API Management as passive.

**Technologies used :**
* Microsoft Azure
* Azure ARM Templates
* Azure Devops (Optional)


