# Tuning Scenario: analytics-model-building

This scenario covers tuning parameters applicable to deployments with a high volume of concurrent sessions building and managing analytical models, typically from within SAS Model Studio. The set of parameters includes:

* Pipeline Execution Tuning - increases the size of the thread pools used for executing model pipelines to allow for higher throughput

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    ```bash
      - analytics-model-building
    ```