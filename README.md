# App Configuration Toolchain Integration

Adopt a Devops approach in your feature releases using IBM Cloud App Configuration service and IBM Cloud Continuous delivery.  Continuous delivery includes toolchains that automates the building of your applications. This repo contains the toolchain template.

## Contents
- [App Configuration Toolchain Integration](#app-configuration-toolchain-integration)
  - [Contents](#contents)
  - [Prerequisite](#prerequisite)
  - [Create an instance of App Configuration service](#create-an-instance-of-app-configuration-service)
  - [Create Toolchain](#create-toolchain)
  - [Pipeline Details](#pipeline-details)
    - [appconfiguration-sync Pipeline](#appconfiguration-sync-pipeline)
      - [Inputs](#inputs)
    - [appconfiguration-cd Pipeline](#appconfiguration-cd-pipeline)
      - [Inputs](#inputs-1)


## Prerequisite

- You need an [IBM Cloud](http://cloud.ibm.com/) account. If you don't have an account, create one [here](https://cloud.ibm.com/registration/).

## Create an instance of App Configuration service
- Log in to your IBM Cloud account.
- In the [IBM Cloud catalog](https://cloud.ibm.com/catalog#services), search **App Configuration** and select [App Configuration](https://cloud.ibm.com/catalog/services/apprapp). The service configuration screen opens.
- **Select a region** - Currently, Dallas (us-south) and London (eu-gb) region is supported.
- Select a pricing plan, resource group and configure your resource with a service name, or use the preset name.
- Click **Create**. A new service instance is created and the App Configuration console displayed.
- Create features, collections & segments as per the need of your application.

## Create Toolchain 

[![Deploy To IBM Cloud](https://console.bluemix.net/devops/graphics/create_toolchain_button.png)](https://github.com/ibm-cloud-appconfiguration/appconfiguration-toolchain)

Once the pipeline is created, populate the `Environment Properties` for each of the pipeline and update the details.

## Pipeline Details

### appconfiguration-sync Pipeline

This pipeline verifies the configuration stored in the git, to the configuration that exist in an App Configuration service instance.  If there is a difference, this pulls the configuration information and stores it to a file, which is used by the application. 

#### Inputs

  - **apikey**: The ibmcloud api key that has access to the App Configuration instance
  - **baseUrl**: (Default: `https://apprapp.cloud.ibm.com/apprapp/feature/v1/instances/`) Base url to the App Configuration service instance.
  - **branch**: (Default: `master`) The branch of the application to clone.
  - **collection_id**: App Configuration collection id.
  - **featureFilePath**: (Default: feature.json) Path to the App Configuration feature file, used by the application to evaluate feature flags.
  - **gitToken**: GIT token to access the git repository.
  - **guid**: App Configuration GUID.
  - **region**: Region of the App Configuration instance.
  - **repository**: Application GIT repository URL.


### appconfiguration-cd Pipeline

This pipeline builds the application using the dockerfile and deploys to a kubernetes cluster.  

#### Inputs

  - **apikey**: The ibmcloud api key that has access to the cluster.
  - **baseUrl**: (Default: `https://apprapp.cloud.ibm.com/apprapp/feature/v1/instances/`) Base url to the App Configuration service instance.
  - **branch**: (Default: `master`) The branch of the application to clone.
  - **clusterName**: Name of the cluter to deploy the application.
  - **gitToken**: GIT token to access the git repository.
  - **imageUrl**: IBM Cloud Image Respository URL to store the built docker image.
  - **region**: (Default: `us-south`) Region of the cluster.
  - **resourceGroup**: (Default: `default`) Resource group of the cluster.
  - **repository**: Application GIT repository URL.



