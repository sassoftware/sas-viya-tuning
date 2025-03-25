# Tuning Scenario: platform-common

This scenario covers many of the common tuning parameters applicable to nearly all
Viya environments where there are a large volume of users interacting with the system at the same time. This can include interactive sessions through any of the Viya web applications, the sas-viya CLIs, or batch jobs running in the background. The set of parameters includes:

* Large Deployment Tuning - increases the size of thread pools used for accessing the SAS Infrastructure Data Server to allow for higher throughput
* LDAP Connection Pool Tuning - configures the connection pool used by Viya's authentication mechanism to allow for a higher number of concurrent user logins when connecting to an LDAP server.
* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-arke
  * sas-authorization
  * sas-files
  * sas-file-store
  * sas-logon-app

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - platform-common

## Tuning Summary

| Pod Name           | CPU Limits     | Memory Limits  | Java Heap              | Other                        |
|--------------------|----------------|----------------|------------------------|------------------------------|
| All Services       |                |                |                        | JDBC Connection Pool (large) |
| sas-arke           | 1000m          | 1Gi            |                        |                              |
| sas-authorization  | 6000m          |                | MaxRAMPercentage (75%) |                              |
| sas-file-store     | 3000m          | 2Gi            |                        |                              |
| sas-files          | 2000m          | 3Gi            | MaxRAMPercentage (75%) |                              |
| sas-identities     |                |                | MaxRAMPercentage (75%) | LDAP Connection Pool (30)    |
| sas-logon-app      | 2000m          | 2Gi            | MaxRAMPercentage (75%) |                              |
