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

## Tuning Summary

| Pod Name                  | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|---------------------------|----------------|----------------|------------------------|------------------------------|
| sas-compute               | 4000m          | 2Gi            |                        |                              |
| sas-job-execution         | 2000m          | 1500Mi         | MaxRAMPercentage (75%) |                              |
| sas-launcher              |                |                | MaxRAMPercentage (75%) |                              |
| sas-studio                | 2000m          | 2Gi            |                        |                              |  
| sas-studio-app            | 1000m          | 1Gi            |  |                              |
| sas-workload-orchestrator | 4000m          |                |                        |                              |  
