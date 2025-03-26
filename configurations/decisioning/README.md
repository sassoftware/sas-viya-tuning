# Tuning Scenario: decisioning

This scenario covers tuning parameters applicable to deployments with a high volume of concurrent sessions building and managing decisions and related resources, typically from within SAS Decision Manager. The set of parameters includes:

* Memory and CPU Limit Tuning - update JVM settings for several pods, including:
  * sas-business-rules
  * sas-decisions
  * sas-treatment-definitions

## Usage Notes

The tuning recommendations for this configuration include environment settings only. There are no changes currently recommended for any of the
Kubernetes pods/deployments. Because of this, only the settings defined in the [sitedefault.yaml](./sitedefault.yaml) file would need to be applied.


## Tuning Summary

| Pod Name                           | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|------------------------------------|----------------|----------------|------------------------|------------------------------|
| sas-decisions                      |                |                | MaxRAMPercentage (75%) |                              |
| sas-decisions-framework            |                |                | MaxRAMPercentage (75%) |                              |
| sas-treatment-definitions          |                |                | MaxRAMPercentage (75%) |                              |
