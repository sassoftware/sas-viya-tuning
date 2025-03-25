# Tuning Scenario: scoring-execution

This scenario covers tuning parameters applicable to deployments using the high performance program execution service, SAS Micro Analytic Service (MAS). These tunings should only be applied when MAS is deployed and used to concurrently execute a high volume of programs.

* Memory and CPU Limit Tuning - update JVM settings for several pods, including:
  * sas-microanalytic-score

**Important:** When tuning the SAS Micro Analytic Service (MAS), keep in mind that on average, each MAS module consumes roughly 100MB of non-JVM memory; therefore, your MAS node and pod(s) should be sized based on the required JVM size, and the sum of all modules expected to be compiled and loaded into MAS. 

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - scoring-execution

## Tuning Summary

| Pod Name                           | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|------------------------------------|----------------|----------------|------------------------|------------------------------|
| sas-microanalytic-score            | 4000m          | 5Gi            | 2g                     |                              |
