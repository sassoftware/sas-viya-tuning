# Tuning Scenario: compute-common

This scenario covers many of the common tuning parameters applicable to deployments requiring a large number of compute sessions, including sessions launched from client applications such as SAS Studio, scheduled jobs, and batch jobs. The set of parameters includes:

* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-compute
  * sas-job-execution
  * sas-launcher
  * sas-workload-orchestrator

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - compute-common
