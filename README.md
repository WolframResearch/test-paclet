# Test Paclet for the [Wolfram Language Paclet Repository](https://resources.wolframcloud.com/PacletRepository/)

The Test Paclet action is an interface to the 
[`TestPaclet`](https://resources.wolframcloud.com/PacletRepository/resources/Wolfram/PacletCICD/ref/TestPaclet.html) 
function from 
[Wolfram/PacletCICD](https://resources.wolframcloud.com/PacletRepository/resources/Wolfram/PacletCICD/) 
and can be used to run your paclet test files within GitHub Actions.

## Usage

A YAML file that uses this action can be automatically generated for your paclet using 
[`WorkflowExport`](https://resources.wolframcloud.com/PacletRepository/resources/Wolfram/PacletCICD/ref/WorkflowExport.html):

```Mathematica
PacletSymbol["Wolfram/PacletCICD", "WorkflowExport"]["path/to/paclet", "Test"]
```

Alternatively, using GitHub actions YAML syntax directly:
```yaml
name: Test Paclet
on: [push]
jobs: 
  Test: 
    name: Test Paclet
    runs-on: ubuntu-latest
    container: 
      image: wolframresearch/wolframengine:latest
      options: --user root
    env: 
      WOLFRAMSCRIPT_ENTITLEMENTID: ${{ secrets.WOLFRAMSCRIPT_ENTITLEMENTID }}
    steps: 
    - name: Checkout repository
      uses: actions/checkout@v2
    - name: Test paclet
      uses: WolframResearch/test-paclet@v1
```

## Parameters

Input                     | Default                     | Description
------------------------- | --------------------------- | ---------------
`definition_notebook`     | `"./ResourceDefinition.nb"` | The relative path to the paclet's resource definition notebook
`paclet_cicd_version`     | `"latest"`                  | The version of [PacletCICD](https://resources.wolframcloud.com/PacletRepository/resources/Wolfram/PacletCICD/) to use

## Notes
For this action to work, your repository needs to have a license entitlement ID defined as a repository secret. See [this tutorial](https://resources.wolframcloud.com/PacletRepository/resources/Wolfram/PacletCICD/tutorial/GitHubActionsQuickStart.html) for details.


## See Also

- [Action for building your paclet](https://github.com/WolframResearch/build-paclet)
- [Action for checking your paclet for potential issues](https://github.com/WolframResearch/check-paclet)
- [Action for submitting your paclet to the Wolfram Language Paclet Repository](https://github.com/WolframResearch/submit-paclet)
- [Continuous Integration and Deployment for Wolfram Language Paclets](https://resources.wolframcloud.com/PacletRepository/resources/Wolfram/PacletCICD/)