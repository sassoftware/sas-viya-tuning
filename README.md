# sas-viya-tuning

The sas-viya-tuning repo contains a set of tuning parameters designed to improve overall performance for large scale Viya deployments.  

This project is broken down into the following components:
* site-default tuning - configuration properties to apply to Viya services during initial start-up
* kustomization files - transformers to apply to various Kubernetes Deployment and StatefulSet resources

It is important to note that the settings contained within this project are not a one-size-fits-all model.  This project is designed to capture configuration changes for many of the 
core / most-active pods in a Viya deployment.  Changes to these parameters, or additional parameters required for other pods in the system, may need to be 
applied depending on the workload of the Viya deployment.


## Getting started

### For new Viya deployments

1. Clone the project:

   `git clone https://gitlab.sas.com/erbour/sas-viya-tuning.git`

2. Copy the contents of this project to the deployment directory used to install/configure Viya

   :bulb: **Tip:** If a sitedefault file is already being used, make sure it exists within a different path, or rename it to ensure the contents are not overwritten.  After renaming it, you will need to merge in the contents of the existing file with the contents of the `sas-viya-tuning/sitedefault/sitedefault.yaml` file.

   `cp -r sas-viya-tuning/sitedefault {deploy-dir}`

   `cp -r sas-viya-tuning/site-config {deploy-dir}`

3. Apply the sitedefault file as per the Common Customizations step

4. Add the following entry to the `transformers` block of your deployment's `kustomization.yaml` prior to installing Viya per these instructions
in [Deploying the Software](https://documentation.sas.com/?cdcId=sasadmincdc&cdcVersion=default&docsetId=dplyml0phy0dkr&docsetTarget=titlepage.htm) in the SAS Viya Platform Operations Guide.

   `- site-config/tuning`

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

