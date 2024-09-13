# Tuning Scenario: compute-scheduled-jobs

This scenario covers additional tuning parameters required when a large number of jobs are scheduled by users within applications such as SAS Studio or SAS Environment Manager.  The set of parameters includes:

* Memory and CPU Limit Tuning - increase the memory and CPU limits of certain platform pods, including:
  * sas-scheduler

## Usage Notes

Add the following line to the `resources` section of the main sas-viya-tuning [kustomization.yaml](../kustomization.yaml) file:


    resources:
      - compute-scheduled-jobs

