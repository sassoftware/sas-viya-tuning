## v1.9.0 (2026.05)
* Added sas-audit resource limits to platform-common configuration
* Added sas-job-execution-app resource limits to compute-common configuration

## v1.8.0 (2026.02)
* Removed the platform-crunchy-postgres configuration
* Removed the JVM tuning configurations for scoring-execution

## v1.7.0 (2025.12-2026.01)
* Removed scenarios with no active tuning settings:
  * compute-scheduled-jobs
  * decisioning
  * reporting-visualization
* Removed the following analytics-model-building configurations:
  * sas-analytics-gateway JVM tuning (default values have changed)
  * sas-data-mining-project-resources resource limits (default values have changed)
* Removed the following compute-common configurations:
  * sas-compute resource limits (default values have changed)
  * sas-job-execution JVM tuning (default values have changed)
  * sas-launcher JVM tuning (default values have changed)
* Removed the following platform-common configurations:
  * sas-file-store memory limit (default values have changed)
  * sas-authorization, sas-credentials, sas-files, sas-identities, and sas-logon-app JVM tuning (default values have changed)
* Updated scoring-execution configuration:
  * Removed kustomization.yaml (JVM tuning in sitedefault.yaml persists) 


## v1.6.0 (2025.09 - 2025.11)
* Removed the following platform-common configurations:
  * sas-arke (default values have changed)
  * sas-files (default values have changed)
  * sas-authorization (default values have changed)
* Removed the following compute-common configurations:    
  * sas-workload-orchestrator (default values have changed)
* Updated compute-common configuration:
  * Removed cpu limit setting for sas-job-execution (default value has changed)    
* Updated platform-common configuration:
  * Removed cpu limit setting for sas-logon-app (default value has changed)
* Updated compute-scheduled-jobs configuration:
  * Removed cpu limit setting for sas-scheduler (default value has changed)
* Updated decisioning sitedefault configuration:
  * Removed decisions JVM tuning (decisions pod merged into decisionsFramework)

## v1.5.1 (2025.06 - 2025.08)
* Fixed kustomization.yaml reference to renamed sas-model-manager directory

## v1.5.0 (2025.06)
* Renamed sas-model-management to sas-model-manager (Model Management service was merged into new MCR service)
* Added sas-workload-orchestrator resource limits to compute-common configuration
* Updated sas-studio-app resource limits:
  * Reduced CPU limit from 4000m to 1000m
  * Reduced memory limit from 4Gi to 1Gi
  * Removed JVM tuning (SAS Studio is now a Go application)
* Updated documentation:
  * Replaced hardcoded GitLab URL with placeholder for repository location

## v1.4.0 (2025.04)
* Updated sas-launcher environment variable settings. These changes are not compatible with earlier versions.

## v1.3.1 (2025.01 - 2025.03)
* Fixed the pod requests for Crunchy
* Added JVM tuning for sas-credentials in platform-common configuration

## v1.3.0 (2025.01 - 2025.02)
* Introduced new tunings for the following scenarios:
    * analytics-model-building
    * analytics-model-management
    * decisioning
    * scoring-execution
* Updated platform-common configuration:
    * Removed memory limit setting for sas-authorization (default values have changed)
* Updated compute-common configuration:
    * Removed memory and cpu limit settings for sas-launcher (default values have changed)

## v1.2.0 (2024.08 - 2024.12)
* Refactored tunings for the new sas-file-store deployment

## v1.1.0 (2024.03 - 2024.07)
* Initial release
* The contents of this release have been verified against some Viya stable releases from 2024.07 and earlier.  This project started in the Spring of 2024, and thus has not been tested against all previous Viya releases.    