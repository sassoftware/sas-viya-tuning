# sas-viya-tuning

The sas-viya-tuning repo contains a set of tuning parameters designed to improve overall performance for large scale Viya deployments.  

This project is broken down into a set of configuration "tunables" for various scenarios SAS Viya users perform on a routine basis.  Each
scenario represents an action, or a set of actions, users may perform while interacting with SAS Viya web applications, command-line interfaces,
scheduled batch jobs, mobile applications, etc.

Which scenarios are applicable will depend on the specific Viya environment and which applications are used.  
Not all scenarios in this project necessarily need to be included, and administrators can pick and choose which ones pertain to their environment.

In most cases, the tuning parameters for a given scenario can be broken down into the following categories:
* site-default tuning - configuration properties to apply to Viya services during initial start-up
* kustomization files - Kustomize transformers to apply to various Kubernetes Deployment and StatefulSet resources

For additional details and a description of what each scenario covers, make sure to drill into the respective README files.

It is important to note that the settings contained within this project are not necessarily a one-size-fits-all model.  This project is designed to capture configuration changes for many of the core / most-active pods in a Viya deployment and makes a best attempt at tuning these pods based on high concurrent workloads.  Depending on the number of users accessing
the system or the various workloads themselves, it may be necessary to adjust these parameters, or add additional parameters required for other pods in the system.

And finally, keep in mind that there may be some amount of overlap in the configurations - where one scenario may include changes for a service or application that is also referenced within a 
different scenario.  In these situations, it is important to remember when applying these configurations, values from the last referenced configuration will be applied.


## Supported Scenarios

### Platform Scenarios
| Scenario         | Description                                 |
|------------------|---------------------------------------------|
| [platform-common](./configurations/platform-common/README.md) | Recommended tunings that apply to core services contained within the SAS Viya Platform.
| [platform-crunchy-postgres](./configurations/platform-crunchy-postgres/README.md) | Recommended tunings that apply to the Crunchy Postgres instance (only applicable when Viya is deployed with an internal Postgres instance).

### SAS Application Scenarios
| Scenario                  | Description                                 |
| --------------------------|---------------------------------------------|
| [analytics-model-building](./configurations/analytics-model-building/README.md) | Tunings specific to SAS Model Studio and building analytical models.
| [compute-common](./configurations/compute-common/README.md) | Tunings specific to the SAS Compute, SAS Launcher services, and SAS Workload Orchestrator, when a high number of concurrent Compute sessions are required.
| [compute-scheduled-jobs](./configurations/compute-scheduled-jobs/README.md) | Tunings specific situations where there is a large number of scheduled jobs running within the deployment.
| [reporting-visualization](./configurations/reporting-visualization/README.md) | Tunings specific to SAS Visual Analytics, when a high volume of users are accessing the web application, viewing and/or editing reports, etc.



## Getting Started

Follow these steps for integrating the tuning parameters into a new or existing Viya deployment.

1. Clone the project:

   `git clone https://gitlab.sas.com/erbour/sas-viya-tuning.git`

   The following steps are necessary following the `clone` command to point to the right branch:

   `git fetch origin`

   `git checkout scenarios`

2. Copy the contents of this project to the `site-config` location within the deployment directory used to install/configure Viya

   `cp sas-viya-tuning {deploy-dir}/site-config`

3. In your deployment's main `kustomization.yaml` file, add the following line within the `transformers` section to include the appropriate tuning resources:

    ```bash
    transformers:
      - site-config/sas-viya-tuning/configurations
    ```

   For more information on the initial `kustomization.yaml` file, see the [SAS Viya Platform Administration](https://go.documentation.sas.com/doc/en/sasadmincdc/v_053/dplyml0phy0dkr/n0g237aqo6pz1in1t19wjb94j9bi.htm) guide.

4. Review the individual `README.md` files for each scenario for information on what specific tunings are covered.  Keep in mind that further customizations may be required for each scenario - either by adjusting the default values or adding new configurations - depending on your workload needs.  For each applicable scenario, add the appropriate reference to the `sas-viya-tuning/configurations/kustomization.yaml` file as needed.  Note, the `platform-common` scenario is applied by default and is recommended for all environments.
For example:

    ```bash
    resources:
      - platform-common
      - compute-common
      - compute-scheduled-jobs
    ```

5. Once the transformers are in place, follow the steps below to complete the setup, depending on if your'e dealing with a new Viya deployment, or one that already exists and needs to be updated.

**For new Viya deployments**

1. Certain scenarios contain their own custom `sitedefault.yaml` file, each consisting of additional tunings to be applied when the Viya services/applications are deployed.  If a custom `sitedefault.yaml` file does exist for a scenario, copy and merge the contents of the file into your deployment's main `sitedefault.yaml` file.  For more information on using a sitedefault file, see [Add a sitedefault File to Your Deployment](https://go.documentation.sas.com/doc/en/sasadmincdc/v_045/dplyml0phy0dkr/n08u2yg8tdkb4jn18u8zsi6yfv3d.htm#n19f4zubzxljtdn12lo0nkv4n4cf) in the SAS Viya Administration guide.

2. Follow the instructions in the [Deployment](https://documentation.sas.com/?cdcId=sasadmincdc&cdcVersion=default&docsetId=k8sag&docsetTarget=titlepage.htm) section of the SAS Viya Administration guide to deploy the software.
 
**For existing Viya deployments**

1. Certain scenarios contain their own custom `sitedefault.yaml` file, each consisting of additional tunings to be applied when the Viya services/applications are deployed.  However, 
because the sitedefault file is only processed during the initial installation of the software, these configurations will have to be applied using one of two approaches:

   * SAS Environment Manager
   * sas-bootstrap-config


   For this documentation, we will describe how to apply the necessary changes using SAS Environment Manager only.

   :bulb: **Tip:** If a sitedefault file was initially used for the deployment, even though it won't be used to process these updates, it is still recommended to modify that file so that it
   contains the configurations in this project in case you need to re-deploy the system.  To do so, merge in the properties from the various `sitedefault.yaml` files for each applicable scenario into your deployment's existing sitedefault file.

2. Using SAS Environment Manager, follow these steps:

   * Navigate to the Configuration view
   * Select the appropriate service under the "All services" list
   * Check if a configuration exists that matches the property within the sitedefault file.  For example, all "java_option_xxxx" properties should be added under the "jvm" configuration for a service.  If a configuration does exist, click on the Edit link.  If a configuration does not exist, click on the New Configuration link.
   * Update the configuration with the appropriate values.  When updating the Xmx (Java Heap) setting for a service, the property can be set as:
       
       java_option_xmx: -XX:MaxRAMPercentage=75

   * Note, some properties require a restart of the service to take effect.  This restart will occur in the following step when the services are re-deployed.

3. Follow the instructions in the [Modifying Existing Customizations in a Deployment](https://go.documentation.sas.com/doc/en/sasadmincdc/v_045/dplyml0phy0dkr/n1f2q6pp0gjheqn1jl204vptrubs.htm) section of the SAS Viya Platform Administration guide to update the software.
