# ADO Docker Template

    This template uses the Service Connection created using Azure Resource Manager Service Principal that has scope of accessibility to Azure Container Registry

## Pipeline Requirements

The template pipeline requires the following parameters to be defined:

### Parameters:


| Name  | Displayname | Comments |
| ------------- | ------------- | ------------- |
| ServiceConnection | Azure Service Connection forazure resource manager in your Azure pipeline |This helps the module to authenticate with azure cli |
| ACRname | Azure Container Registry Name |  |
| ACRrepo | acr docker repostiroy | docker registry imagename to be created |
| DockerfilePath  | location of Dockerfile | Required when buid step |
| imageTags | Version or tag for image | when multiple tags pass in following way: **"1.2.3,latest"** |
| buildContext  | the path to constitute everything for Docker Image | Optionally used with build step |
| buildArgs | arguments for build step | string | | | Optional |--build-arg var.value=1 |
-----------------------------------------------------------------------------------------------------------------------
 
### How to Use:

  ```yaml
  # azure-pipeline.yml
  resources:
    repositories:
      - repository: Docker
        type: github
        name: NashTech-Labs/azurePipelineDocker
        ref: main
        endpoint: 'GitHubServiceConnection'

  steps:
    - template: azure-pipelines.yml@Docker
        parameters:
            ServiceConnection: '<arm-connection>'
            ACRname: '<acr-name>'
            ACRrepo: '<dockerimagename>'
            DockerfilePath: './Dockerfile'
            buildContext: '.'
            buildArgs: '--target=server'
            imageTags: '0.0.1,latest'
  ```
