# Tuning Scenario: platform-crunchy-postgres

This scenario includes additional tunings for deployments configured with an internal Crunchy Postgres instance, where the default CPU and memory limits need to be increased.

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:

    resources:
      - platform-crunchy-postgres
    ```