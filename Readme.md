This directory contains templates for setting variables. The templates are organized as follows:

Parameters:

| Name  | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| functionAppServiceNames | string | | | Optional | |
| functionArchivePattern | string | | | Optional | |
| functionExtractFolder | string | | | Optional | |
| functionPackageId | string | | | Optional | |
| functionPackageVersion | string | | | Optional | |
| enablefunctionVariables | boolean | 'true' | 'true'/'false' | Required | |


Direct use of a template

You can directly call a particular template as per the requirement. for example: to use setup and init only.

 

# azure-pipeline.yml
resources:
repositories:
  - repository: Template
    type: github
    name: your_username/terraform.validate.ado
    ref: <respective branch name>
    endpoint: 'githubServiceConnectioNname'

steps:

  - ${{ if eq( parameters['enablefunctionVariables'], 'true') }}:
    - template: templates/functionVariables.yml
      parameters:
        appDeploymentTarget: ${{parameters.appDeploymentTarget}}
        key: ${{parameters.key}}
        functionAppServiceNames: ${{parameters.functionAppServiceNames}}
        functionArchivePattern: ${{parameters.functionArchivePattern}}
        functionExtractFolder: ${{parameters.functionExtractFolder}}
        functionPackageId: ${{parameters.functionPackageId}}
        functionPackageVersion: ${{parameters.functionPackageVersion}}
