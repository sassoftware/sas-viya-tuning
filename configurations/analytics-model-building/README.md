# Tuning Scenario: analytics-model-building

This scenario covers tuning parameters applicable to deployments with a high volume of concurrent sessions building and managing analytical models, typically from within SAS Model Studio. The set of parameters includes:

* Pipeline Execution Tuning - increases the size of the thread pools used for executing model pipelines to allow for higher throughput
* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-analytics-gateway
  * sas-analytics-resources
  * sas-data-mining-project-resources
  * sas-data-mining-risk-models

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - analytics-model-building

## Tuning Summary

| Pod Name                           | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|------------------------------------|----------------|----------------|------------------------|------------------------------|
| sas-analytics-gateway              |                | 4Gi            | MaxRAMPercentage (75%) |                              |
| sas-analytics-resources            | 3000m          | 1Gi            |                        |                              |
| sas-data-mining-project-resources  | 2000m          |                |                        |                              |
| sas-data-mining-risk-models        | 1000m          |                |                        |                              |
