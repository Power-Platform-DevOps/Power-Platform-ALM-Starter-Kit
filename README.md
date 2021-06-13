# Power Platform ALM Starter Kit

<p align="center">
    <a href="#repolicense" alt="Repository License">
        <img src="https://img.shields.io/github/license/Power-Platform-DevOps/Power-Platform-ALM-Starter-Kit?color=yellow&label=License" /></a>
    <a href="#openissues" alt="Open Issues">
        <img src="https://img.shields.io/github/issues-raw/Power-Platform-DevOps/Power-Platform-ALM-Starter-Kit?label=Open%20Issues" /></a>
    <a href="#openpr" alt="Open Pull Requests">
        <img src="https://img.shields.io/github/issues-pr-raw/Power-Platform-DevOps/Power-Platform-ALM-Starter-Kit?label=Open%20Pull%20Requests" /></a>
</p>

<p align="center">
    <a href="#watchers" alt="Watchers">
        <img src="https://img.shields.io/github/watchers/Power-Platform-DevOps/Power-Platform-ALM-Starter-Kit?style=social" /></a>
    <a href="#forks" alt="Forks">
        <img src="https://img.shields.io/github/forks/Power-Platform-DevOps/Power-Platform-ALM-Starter-Kit?style=social" /></a>
    <a href="#stars" alt="Stars">
        <img src="https://img.shields.io/github/stars/Power-Platform-DevOps/Power-Platform-ALM-Starter-Kit?style=social" /></a>
</p>

The goal of this project is to provide to the `Power Platform community` a `kit` that will `help people start their DevOps journey with the Power Plaform`.
The content of this repository mainly focus `advanced makers` with experience with ALM concepts and **code first** development.
We will try to make this **starter kit** useful for you.

## What does the Power Platform ALM Starter Kit currently covers?

* Create a Power Platform environment and the corresponding service endpoint in Azure DevOps using a pipeline you can trigger manually
* Create a Power Platform service endpoint associated to an existing environment using a pipeline you can trigger manually
* Delete a Power Platform environment and the corresponding service endpoint in Azure DevOps using a pipeline you can trigger manually
* Delete a Power Platform service endpoint associated to an existing environment using a pipeline you can trigger manually

## What can you find in the Power Platform ALM Starter Kit?

```
Power-Platform-ALM-Starter-Kit
│   README.md
│   LICENSE
|   CODE_OF_CONDUCT.md
└───Pipelines
└───└───Templates
│   │   │   create-powerplatform-environment-template.yml: Pipeline template for the creation of a Dataverse environment
│   │   │   create-powerplatform-service-endpoint-template.yml: Pipeline template for the creation of a Power Platform service connection in Azure DevOps
│   │   │   delete-powerplatform-service-endpoint-template.yml: Pipeline template for the deletion of a Power Platform service connection in Azure DevOps
│   │   │   generate-powerplatform-environment-domainname-template.yml: Pipeline template for the generation of a Power Platform environment DomainName based on the EnvironmentName provided
│   │   │   generate-powerplatform-environment-url-template.yml: Pipeline template for the generation of the URL of a Power Platform environment based on the EnvironmentName provided
│   │   │
└───└───Utils
│   │   │   create-powerplatform-environment-and-service-endpoint.yml: Pipeline used to create of a Dataverse environment if it does not exist (search based on the name provided) and generate the associated Power Platform service connection in Azure DevOps
│   │   │   delete-powerplatform-environment-and-service-endpoint.yml: Pipeline used to delete a Dataverse environment and delete the associated Power Platform service connection in Azure DevOps
│   │   │   delete-powerplatform-service-endpoint.yml: Pipeline used to delete a Power Platform service connection in Azure DevOps
│   │   │   powerplatform-service-connection-test.yml: Pipeline used to test a Power Platform service connection with its name provided
│   │   │  
└───Configuration
│   │   powerplatform-spn-template.json: Body request template for the creation of a Power Platform service connection in Azure DevOps
│   │   DataverseEnvironmentConfiguration.txt: Template for the configuration of the Dataverse environment to create
└───Scripts
└───└───Tests
│   │   │   New-DataverseEnvironment.Tests.ps1: Test script of the New-DataverseEnvironment PowerShell function
│   │   New-DataverseEnvironment.ps1: PowerShell function for the creation of a Dataverse environment if it does not exist (search based on the name provided)
```

## How to set-up the Power Platform ALM Starter Kit?
### Prerequisites

To use this starter kit, you will need to have the following components already available:
- an **Azure DevOps organization**
- an **Azure DevOps project with a repository**
- the **Power Platform Build Tools** extension installed in your Azure DevOps organization
- an **app registration** registered in Azure Active Directory with (*at least*) the following permissions and a client secret generated: `Dynamics CRM.user_impersonation`
- an **application user** created on one of your existing Dataverse environments (*for example the **Production** environment*) with the **System Administrator** security role using the app registration we talked about in the previous point
- a **Power Platform service connection** created in the considered Azure DevOps project associated to the Dataverse environment we talked about in the previous point with the application user registered
- a **PAT (Personal access token)** created for the considered Azure DevOps organization with `Full access` (*at the moment, we are not able to clearly identify the access needed to enable a service connection for all pipelines*)
- Add the **Contribute** permission to your project **Build Service** user account in your repository

### Step-by-step guide

1. Copy the `Pipelines`, `Configuration` and `Scripts` folders of this repository
2. Past it at the root of the repository in the Azure DevOps project you want to use
3. Update the **DataverseEnvironmentConfiguration.txt** configuration file in the **Configuration** folder with the configuration you want for your environments (*you can use the content of the **Resources** section of this page to help you complete this step*)
4. Create pipelines from all YAML pipeline definitions in the `Pipelines/Utils` folder
5. Create a **variable group** in your Azure DevOps project with the following name and with the variables below: `power-platform-environment-management-variable-group`
   - `ApplicationId`: **Application (client) ID** of your app registration in Azure Active Directory
   - `AzureDevOpsOrganizationURL`: **URL** of the Azure DevOps organization you are working in (*ex: https://dev.azure.com/demonstration/*)
   - `ClientSecret`: **Clien secret** of your app registration in Azure Active Directory
   - `DataverseEnvironmentConfigurationFileName`: **Full name** (with extension) of the file you want to use for the configuration of the Dataverse environments to create (*ex: DataverseEnvironmentConfiguration.txt*)
   - `PatToken`: Value of the **PAT (Personal access token)** we talked about in the **Prerequisites** section above
   - `PowerPlatformEnvironmentURLBase`: **Base of the URL** (linked to the location) you want to consider for your Dataverse environments to create (*ex: crm12.dynamics.com*)
   - `TenantId`: **ID** of your app registration in Azure Active Directory
6. Test the pipelines

### Resources

You can use the commands below from the [**Microsoft.PowerApps.Administration.PowerShell**](https://www.powershellgallery.com/packages/Microsoft.PowerApps.Administration.PowerShell) PowerShell module to find the information for configuration file for the creation of the Dataverse environments:
- [**Get-AdminPowerAppEnvironmentLocations**](https://docs.microsoft.com/en-us/powershell/module/microsoft.powerapps.administration.powershell/get-adminpowerappenvironmentlocations) to get all the supported locations for your Dataverse environment
- [**Get-AdminPowerAppCdsDatabaseLanguages**](https://docs.microsoft.com/en-us/powershell/module/microsoft.powerapps.administration.powershell/get-adminpowerappcdsdatabaselanguages) to get all the supported languages for a specific location for your Dataverse environment
- [**Get-AdminPowerAppCdsDatabaseTemplates**](https://docs.microsoft.com/en-us/powershell/module/microsoft.powerapps.administration.powershell/get-adminpowerappcdsdatabasetemplates) to get all the supported applications for a specific location  for your Dataverse environment
- [**Get-AdminPowerAppCdsDatabaseCurrencies**](https://docs.microsoft.com/en-us/powershell/module/microsoft.powerapps.administration.powershell/get-adminpowerappcdsdatabasecurrencies) to get all the supported currencies for a specific location  for your Dataverse environment

For the `PowerPlatformEnvironmentURLBase` variable in the `power-platform-environment-management-variable-group` variable group, you can find the available values in the [**Datacenter regions**](https://docs.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) Microsoft documentation page.

## Contributing to the Power Platform ALM Starter Kit project

1. Fork this repository.
2. Create a branch: `git checkout -b <branch_name>`.
3. Make your changes and commit them: `git commit -m '<commit_message>'`
4. Push to the original branch: `git push origin <project_name>/<location>`
5. Create a pull request targeting the `main` branch of this repository

Alternatively see the GitHub documentation on [creating a pull request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request).

## Contributors

Thanks to the following people who have contributed to this project:

<!-- Static version of the contributors list for now, but if all owners agree, we can install the AllContributors GitHub App (https://allcontributors.org/docs/en/bot/installation) 
<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center">
        <a href="https%3A%2F%2Ftwitter.com%2FBergmannBene">
            <img src="https://avatars.githubusercontent.com/u/9703748?v=3" width="100px;" alt=""/>
            <br />
            <sub>
                <b>Benedikt Bergmann</b>
            </sub>
        </a>
        <br />
        <a title="Documentation">📖</a>
    </td>
    <td align="center">
        <a href="https%3A%2F%2Ftwitter.com%2FRaphaelPothin">
            <img src="https://avatars.githubusercontent.com/u/23240245?v=3" width="100px;" alt=""/>
            <br />
            <sub>
                <b>Raphael Pothin</b>
            </sub>
        </a>
        <br />
        <a title="Documentation">📖</a>
    </td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

## Contact

If needed, you can contact us on twitter:
- [@BergmannBene on Twitter](https://twitter.com/BergmannBene)
- [@RaphaelPothin on Twitter](https://twitter.com/RaphaelPothin)

## License

This project is licensed under the [MIT](https://github.com/Power-Platform-DevOps/Power-Platform-ALM-Starter-Kit/blob/main/LICENSE) license.