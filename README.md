# sas-viya-tuning

The sas-viya-tuning repo contains a set of tuning parameters designed to improve overall performance for large scale Viya deployments.  

This project is broken down into a set of configuration "tunables" for various scenarios that users of SAS Viya commonly perform.  Each 
scenario represents an action, or a set of actions, users may perform while interacting with SAS Viya web applications, command-line interfaces,
mobile applications, etc.  

Which scenarios are applicable will depend on the specific Viya environment and which applications are used.  
Not all scenarios in this project necessarily need to be included, and administrators can pick and choose which ones pertain to their environment.

The tuning parameters for each scneario can be broken down into the following components:
* site-default tuning - configuration properties to apply to Viya services during initial start-up
* kustomization files - Kustomize transformers to apply to various Kubernetes Deployment and StatefulSet resources

For additional details and a description of what each scenario covers, make sure to drill into their respective README files.

It is important to note that the settings contained within this project are not necessarily a one-size-fits-all model.  This project is designed to capture configuration changes for many of the 
core / most-active pods in a Viya deployment and makes a best attempt at tuning these pods based on high concurrent workloads.  In some cases, depending on the number of users accessing
the system or the various workloads themselves, it may be necessary to adjust these parameters, or add additional parameters required for other pods in the system.

And finally, keep in mind that there may be some amount of overlap in the configurations - where one scenario may include changes for a service or application that is also referenced within a 
different scenario.  In these situations, it is important to remember that when applying these configurations, the values from the last referenced configuration will be applied.


## Getting started

### For new Viya deployments

1. Clone the project:

   `git clone https://gitlab.sas.com/erbour/sas-viya-tuning.git`

2. Copy the contents of this project to the `site-config` location within the deployment directory used to install/configure Viya

   `cp sas-viya-tuning {deploy-dir}/site-config`

3. In your deployment's main `kustomization.yaml` file, add the following line within the `transformers` section to include the appropriate tuning resources

    ```bash
    transformers:
      - site-config/sas-viya-tuning/configurations
    ```

4. For each applicable scenario, add the appropriate reference to the `sas-viya-tuning/configurations/kustomization.yaml` file as needed.  Note, the `platform-base` scenario is applied by default.
For example:

    ```bash
    resources:
      - platform-base
      - platform-crunchy-postgres
      - visual-analytics
    ```

5. Some scenarios contain their own custom `sitedefault.yaml` file containing additional tunings that are to be applied when the Viya services/applications are deployed.  If a custom `sitedefault.yaml` file does exist, copy and merge
the contents of the file into your deployment's main `sitedefault.yaml` file.


<!-- 
### For existing Viya deployments

1. Clone the project:

   `git clone https://gitlab.sas.com/erbour/sas-viya-tuning.git`

2. Copy the contents of this project to the deployment directory used to install/configure Viya

   :bulb: **Tip:** If a sitedefault file is already being used, make sure it exists within a different path, or rename it to ensure the contents are not overwritten.  After renaming it, you will need to merge in the contents of the existing file with the contents of the `sas-viya-tuning/sitedefault/sitedefault.yaml` file.

   `cp -r sas-viya-tuning/sitedefault {deploy-dir}`

   `cp -r sas-viya-tuning/site-config {deploy-dir}`

3. Add the following entry to the `transformers` block of your deployment's `kustomization.yaml` file and then follow the instructions in [Updating Software](https://documentation.sas.com/?cdcId=sasadmincdc&cdcVersion=default&docsetId=k8sag&docsetTarget=titlepage.htm) in the SAS Viya Platform Operations Guide to apply the changes.

   `- site-config/tuning`

4. Apply sitedefault file - TBD 

-->
