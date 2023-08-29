# ADO.Pipelines.Templates.frameWork.common.setVariables





## Pipeline Requirements

The setVariable pipeline requires the following parameters to be defined:
Paramaters:


| Name  | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| appDeploymentTarget | string | | | Required | |
| key | string | | | Required | |
| functionAppServiceNames | string | | | Optional | |
| functionArchivePattern | string | | | Optional | |
| functionExtractFolder | string | | | Optional | |
| functionPackageId | string | | | Optional | |
| functionPackageVersion | string | | | Optional | |
| enablefunctionVariables | boolean | 'true' | 'true'/'false' | Required | |


  These parameters provide multiple use case options for the setvariables templates pipeline, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

### Direct use of a template

You can directly call a particular template as per the requirement. for example: to use setup and init only.

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: gitHub-endpoint/ADO.Pipelines.Templates
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'



  steps:

  - template: frameWork/common/setVariables/templates/functionVariables.yml
      parameters: 
        appDeploymentTarget: ${{parameters.appDeploymentTarget}}
        key: ${{parameters.key}}
        functionAppServiceNames: $(platform.eventDispatcher.webAppName)
        functionArchivePattern: event-dispatcher-function.$(build.configVersion).*
        functionExtractFolder: $(build.configVersion)/event-dispatcher-function
        functionPackageId: event-dispatcher-function
        functionPackageVersion: $(build.configVersion)

I
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```
