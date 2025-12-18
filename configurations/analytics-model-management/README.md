# Tuning Scenario: analytics-model-management

This scenario covers tuning parameters applicable to deployments with a high volume of concurrent sessions managing analytical models, typically from within SAS Model Manager. The set of parameters includes:

* Pipeline Execution Tuning - increases the size of the thread pools used for executing model pipelines to allow for higher throughput
* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-model-manager
  * sas-model-publish
  * sas-score-definitions

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - analytics-model-manager

## Tuning Summary

| Pod Name                           | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|------------------------------------|----------------|----------------|------------------------|------------------------------|
| sas-model-manager               | 1000m          | 1Gi            |                        |                              |
| sas-model-publish                  | 1000m          | 1Gi            |                        |                              |
| sas-score-definitions              | 1000m          | 1Gi            |                        |                              |
