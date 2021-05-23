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

Whether you are:
- an experienced Power Platform or Dynamics 365 team who want to improve the quality and the delivery time of your deployments
- a citizen developer who wants an easy way to develop new features for your app on an isolated environment before sharing them with other members of your company

we will try to make this starter kit useful for you.

## What does the Power Platform ALM Starter Kit covers?

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
│
└───Pipelines
└───└───Templates
│   │   │   create-powerplatform-service-endpoint-template.yml: Pipeline template for the creation of a Power Platform service endpoint
│   │   │   delete-powerplatform-service-endpoint-template.yml: Pipeline template for the deletion of a Power Platform service endpoint
│   │   │   generate-powerplatform-environment-domainname-template.yml: Pipeline template for the generation of a Power Platform Environment DomainName from the EnvironmentName variable
│   │   │   generate-powerplatform-environment-url-template.yml: Pipeline template for the generation of the URL of a Power Platform Environment using the EnvironmentName variable
│   │   │
└───└───Utils
│   │   │   create-powerplatform-environment-and-service-endpoint.yml: Pipeline used to create of a Power Platform environment and generate the associated Power Platform service endpoint
│   │   │   create-powerplatform-service-endpoint.yml: Pipeline used to create of a Power Platform service endpoint
│   │   │   delete-powerplatform-environment-and-service-endpoint.yml: Pipeline used to delete a Power Platform environment and delete the associated Power Platform service endpoint
│   │   │   delete-powerplatform-service-endpoint.yml: Pipeline used to delete a service endpoint
│   │   │   powerplatform-service-connection-test.yml: Pipeline used to test a Power Platform service connection with its name provided as variable
│   │   │  
└───ServiceEndpoints
│   │   powerplatform-spn-template.json: Body request template for the creation of a Power Platform service endpoint
```

## How to deploy the Power Platform ALM Starter Kit?
### Prerequisites

To use this starter kit, you will need to have the following components already available:
- an Azure DevOps organization
- an Azure DevOps project with a repository
- the Power Platform Build Tools extension installed in your Azure DevOps organization
- a service principal registered in Azure DevOps with the following permissions and a client secret: `Dynamics CRM.user_impersonation` and `Microsoft Graph.User.Read`
- an Application User created on one of your existing Power Platform environments (for example the **Production** environment)
- a Power Platform Service Connection created in the considered Azure DevOps project associated to the Power Platform environment with the Application User previously configured
- a PAT (Personal access token) created for the considered Azure DevOps organization with `Full access` (at the moment, we are not able to clearly identify the access needed to enable a service connection for all pipelines)
- Add the **Contribute** permission to your project **Build Service** user account on your repository

### Step-by-step guide

1. Copy the `Pipelines` and `ServiceEndpoints` folders of this repository
2. Past it at the root of the repository of the Azure DevOps project you want to use
3. Create pipelines from all YAML pipeline definitions in the `Pipelines/Utils` folder manually adding the variables specified at the beginning of each pipeline definitions
4. Test the pipelines

## Contributing to the Power Platform ALM Starter Kit project

1. Fork this repository.
2. Create a branch: `git checkout -b <branch_name>`.
3. Make your changes and commit them: `git commit -m '<commit_message>'`
4. Push to the original branch: `git push origin <project_name>/<location>`
5. Create the pull request.

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