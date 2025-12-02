# Basic DevOps Toolchain pipeline

This repository contains a basic pipeline configuration that demonstrates basic functionalities, such as git and slack integrations. 

## Setup and Configuration

### Prerequisites

* On [GitHub.com](https://github.com/settings/personal-access-tokens/new), create a new fine-grained personal access token that grants permissions on the repository that you want to access
![](./docs/000-git-pat01.png)
![](./docs/001-git-pat02.png)

### Toolchain creation

* In the IBM Cloud console, navigate to [Create a Toolchain](https://cloud.ibm.com/devops/create) and create a new toolchain by choosing "Build your own toolchain"
![](./docs/010-create-empty-toolchain.png)

* Set a name, region and resource group
![](./docs/011-set-name-and-region.png)

* Review the empty toolchain
![](./docs/012-empty-toolchain.png)

### Add Git repositories

* On your toolchain dashboard, click "Add +" and search for the GitHub integration
![](./docs/020-add-git-integration.png)

* As repository type choose "Existing" and select the Git repo that contains your custom pipeline definitions
![](./docs/021-add-custom-pipeline-definitions.png)

* Create the integration

* Add a second GitHub integration pointing to https://github.com/open-toolchain/tekton-catalog, which contains adds common, reusable tasks and helpers
![](./docs/022-add-tekton-catalog.png)

* Review the added git integrations
![](./docs/023-git-integrations.png)

### Add a delivery dipeline

* On your toolchain dashboard, click "Add +" and search for the GitHub integration
![](./docs/030-add-delivery-pipeline-integration.png)

* Choose a name and set the type to "Tekton"
![](./docs/031-set-name-and-type.png)

* Create the integration

* Review the added delivery pipeline integration
![](./docs/032-review-delivery-pipeline-integration.png)

* In case you don't have created a Continiuous Delivery service, create one by clicking [the link in the notification](https://cloud.ibm.com/catalog/services/continuous-delivery)
![](./docs/033-continuous-delivery-service-creation.png)

### Find your toolchain instance

* From any plance, navigate back to your toolchain instance by using the burger menu in the console: "Platform Automation > Toolchains"
![](./docs/040-navigate-to-toolchains.png)

* Choose your toolchain instance from the list of toolchains
![](./docs/041-toolchain-list.png)

### Configure your basic pipeline

* Click on the name of your delivery pipeline; e.g. "basic"
![](./docs/050-toolchain-dashboard.png)

* On the "Settings > Definitions" tab, click "Add +"
![](./docs/051-add-defintions.png)

* Add the git integration from the tekton-catalog repository (branch: master)
![](./docs/052-add-git-definitions.png)

* Add the definitions hosted in your own repository
![](./docs/053-add-custom-definitions.png)

* Complete this step by saving the added definitions
![](./docs/054-save-definitions.png)

* Navigate to the "Worker" tab and select "IBM Managed Workers" and click "Save"
![](./docs/055-set-worker-config.png)

* Navigate to the "Environment properties" tab and add the following properties

| Type | Name | Value
|:-----|:-----|:-----
| Secure value | git-access-token | `<github-personal-access-token>`
| Text value | git-repository | `<github-url>`; e.g.: `https://github.com/reggeenr/basic-devops-toolchain-pipeline`
| Text value | git-branch | `main`
| Text value | git-repo-directory | `<target-directory>`; e.g.: `basic-devops-toolchain-pipeline`
| Text value | git-user-name | `<github-user-name>` that should be used for commits
| Text value | git-user-email | `<github-user-email>` that should be used for commits
| Enumeration  | pipeline-debug | `0` and `1`. To disable debug mode, `0` should be selected per default

* Review the configured environment properties
![](./docs/056-review-env-props.png)

* Navigate to the main page of your pipeline by using the breadcrumb
![](./docs/057-pipeline-details-page.png)

* Click "Add" to configure a manual trigger
![](./docs/058-add-manual-trigger.png)

* Configure the manual trigger
![](./docs/059-configure-manual-trigger.png)

### Run your pipeline

* From your delivery pipeline details page click "Run" to execute the manual trigger
![](./docs/060-run-pipeline.png)

* Review pipeline run environment properties
![](./docs/061-run-properties.png)

* Navigate to the pipeline run by clicking "View the PipelineRun"
![](./docs/062-view-pipelinerun.png)

## Noteworthy docs

* [IBM Cloud Continuous Delivery](https://cloud.ibm.com/docs/ContinuousDelivery)
* [Tekton - Tasks and Pipelines](https://tekton.dev/docs/pipelines/)