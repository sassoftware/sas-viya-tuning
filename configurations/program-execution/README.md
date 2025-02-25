# Tuning Scenario: decisioning

This scenario covers tuning parameters applicable to deployments using the high performance program execution service, SAS Micro Analytic Service (MAS). These tunings should only be applied when MAS is deployed and used to concurrently execute a high volume of programs.

* Memory and CPU Limit Tuning - update JVM settings for several pods, including:
  * sas-microanalytic-score

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - program-execution

## Tuning Summary

| Pod Name                           | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|------------------------------------|----------------|----------------|------------------------|------------------------------|
| sas-microanalytic-score            | 4000m          | 5Gi            | MaxRAMPercentage (75%) |                              |
