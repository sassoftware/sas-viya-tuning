## v1.5.2 (2025.09)
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