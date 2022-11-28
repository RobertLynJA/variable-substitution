# My Changes:
- Updated to Node 16

# GitHub Action for substituting variables in parameterized files ![.github/workflows/ci.yml](https://github.com/robertlynja/variable-substitution/workflows/.github/workflows/ci.yml/badge.svg?branch=master)

With the Variable Substitution Action for GitHub, you can apply variable substitution to XML, JSON and YAML based configuration and parameter files.

-	Tokens defined in the target configuration files are updated and then replaced with variable values.
-	Variable substitution is applied for only the JSON keys predefined in the object hierarchy. It does not create new keys.
-	Only variables defined explicitly as Environment variables as part of the workflow or system variables that are already available for workflow context can be used in substitution.
-	Variable substitution takes effect only on the `applicationSettings`, `appSettings`, `connectionStrings` and `configSections` elements of configuration files. Please refer [this](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/transforms-variable-substitution?view=azure-devops&tabs=Classic#xml-variable-substitution) for more information. 

If you are looking for more Github Actions to deploy code or a customized image into an Azure Webapp or a Kubernetes service, consider using [Azure Actions](https://github.com/Azure/actions).

The definition of this Github Action is in [action.yml](https://github.com/robertlynja/variable-substitution/blob/master/action.yml).

### Example
See [Use variable substitution with GitHub Actions](https://docs.microsoft.com/en-us/azure/developer/github/github-variable-substitution) for an example of how to use variable substitution.

# End-to-End Sample Workflow

## Sample workflow to apply Variable substitution on XML, JSON, YML files

```yaml
# .github/workflows/var-substitution.yml
on: [push]
name: variable substitution in json, xml, and yml files

jobs:
  build:
    runs-on: windows-latest
    steps:
    - uses: actions/checkout@v2

    - uses: robertlynja/variable-substitution@v1.02
      with:
        files: 'Application/*.json, Application/*.yaml, ./Application/SampleWebApplication/We*.config'
      env:
        Var1: "value1"
        Var2.key1: "value2"
        SECRET: ${{ secrets.SOME_SECRET }}

 ```
