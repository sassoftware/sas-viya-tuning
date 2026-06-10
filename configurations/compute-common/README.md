# Tuning Scenario: compute-common

This scenario covers many of the common tuning parameters applicable to deployments requiring a large number of compute sessions, including sessions launched from client applications such as SAS Studio, scheduled jobs, and batch jobs. The set of parameters includes:

* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-job-execution-app
  * sas-launcher
  * sas-studio
  * sas-studio-app

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - compute-common

## Tuning Summary

| Pod Name                  | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|---------------------------|----------------|----------------|------------------------|------------------------------|
| sas-job-execution-app     |                | 1Gi            |                        |                              |
| sas-launcher              |                |                |                        | default cpu 4 / max cpu 8; default memory limit 8Gi request 2Gi; max memory limit 8Gi request 2Gi |
| sas-studio                | 2000m          | 2Gi            |                        |                              |  
| sas-studio-app            | 1000m          | 1Gi            |                        |                              |
