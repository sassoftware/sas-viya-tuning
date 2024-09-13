# Tuning Scenario: reporting-visualization

This scenario covers tuning parameters applicable to deployments with a high volume of concurrent sessions viewing and editing SAS reports, typically from within SAS Visual Analytics. The set of parameters includes:

* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-report-execution
  * sas-visual-analytics-app

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - reporting-visualization
