# Run Java Native Image app in Azure Spring Apps

This sample shows how to run Java Native Image app in `Azure Spring Apps`.

### Prerequisite

- An Azure subscription. If you don't have a subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.
- [Azure CLI](/cli/azure/install-azure-cli) version 2.45.0 or higher. Use the following command to install the Azure Spring Apps extension: `az extension add --name spring`
- An already provisioned Azure Spring Apps Enterprise instance. For more information, see [Quickstart: Build and deploy apps to Azure Spring Apps using the Enterprise tier](quickstart-deploy-apps-enterprise.md).

### How to run 

1. Prepare a Build Service builder with `tanzu-buildpacks/java-native-image` buildpack. See more details here.
1. Deploy app with source-code or jar file, here is a source-code example
    ```
    az spring app deploy -n <app name> -s <resource name> -g <resource group name> --source-path . --build-cpu 4 --build-memory 8Gi --builder native --build-env BP_NATIVE_IMAGE=true BP_JVM_VERSION=17
    ```
1. Verify app is running. Instances should have status `RUNNING`.
    ```
    az spring app show -n <app name> -s <resource name> -g <resource group name>
    ```
1. Verify sample is working. The url is fetch from previous step. 
    ```
    curl {url}/{name}
    Hello {name}
    ```
