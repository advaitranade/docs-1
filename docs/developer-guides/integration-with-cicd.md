import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import Install from '@site/src/components/install.mdx';
import CodeBlock from '@theme/CodeBlock';

# Integration with CI/CD
Conductor workflows are the core part of your application and should be versioned, controlled, and released similarly to the code.

### Conductor Workflows
Workflows have two main components:
1. Workflow definition that is maintained as a file (JSON or code)
2. Worker implementation used by the workflows

### Workflows
Workflow definitions should be maintained as an independent unit that can be unit and integration tested before releasing to the production environment.

For details on how to unit test workflows, see [Unit and Regression Testing Workflows](/content/developer-guides/unit-and-regression-tests)

#### Steps to publish your workflows as part of the ci/cd
:::note Notes
See [Generating Tokens](/access-control-and-security/applications#generating-token) on how to generate an access token for the API requests below.
:::

#### Downloading workflows from Conductor server to check into your version control
1. Download the JSON from the Conductor UI (Download option from the UI)
2. (Alternatively) Use the API to download JSON for the workflow
    ```shell
    # Get the workflow definition given name and version
    GET -H "X-Authorization:<TOKEN>" /api/metadata/workflow/{name}?version=<version>
    ```
    ```shell
    # Retrieve all the workflows
    GET -H "X-Authorization:<TOKEN>" /api/metadata/workflow/
    ```
#### Publish workflows to the Conductor server from your deployment scripts
Inject `ORKES_ACCESS_KEY`, `ORKES_ACCESS_SECRET` and `ORKES_CONDUCTOR_SERVER_URL` variables with the appropriate values in your deployment pipeline.

The following script cycles through all the workflow definitions in the current folder and uploads it to the Conductor server.

```shell dynamic https://github.com/orkes-io/workflow-cicd/blob/main/src/deploy_workflows.sh section=1 .../src/deploy_workflows.sh



```


### Worker implementation
Workers are your application-specific code and should be maintained, tested, and released as any other code released to production.

Intro
Diagram of
Dev -> UAT -> Prod
How to maintain workflows and task definitions in a version control system such as Git?
How to create a pipeline to promote from Dev -> UAT?
How to test before promoting?
Sample Project
FAQ:
How to get the key and secret?
What permissions does my application for CI need?
How to manage env specific variables in your definition?
Not supported at this time
Github action example?
TODO
Bamboo example?
Partially available
Bitbucket example?
TODO

