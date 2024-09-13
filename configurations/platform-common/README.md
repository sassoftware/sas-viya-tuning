# Tuning Scenario: platform-common

This scenario covers many of the common tuning parameters applicable to nearly all
Viya environments where there are a large number of users interacting with the system. The 
set of parameters includes:

* Large Deployment Tuning - increases the size of thread pools used for accessing the SAS Infrastructure Data Server to allow for higher throughput
* LDAP Connection Pool Tuning - confgures the connection pool used by Viya's authentication mechanism to allow for a higher number of concurrent user logins when connecting to an LDAP server.
* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-arke
  * sas-authorization
  * sas-files
  * sas-folders
  * sas-logon-app

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - platform-common
