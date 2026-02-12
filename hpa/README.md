


# HPA Scaling

> [!WARNING]
> The HPA (Horizontal Pod Autoscaler) settings in this directory are expiremntal only. Do not apply these to a production environment.



## Getting Started

Follow these steps for integrating the HPA settings into a new or existing Viya deployment.

1. In your deployment's main `kustomization.yaml` file, add the following line within the `transformers` section to include the appropriate tuning resources:

    ```bash
    transformers:
      - site-config/sas-viya-tuning/hpa
    ```

   For more information on the initial `kustomization.yaml` file, see the [SAS Viya Platform Administration](https://go.documentation.sas.com/doc/en/sasadmincdc/v_053/dplyml0phy0dkr/n0g237aqo6pz1in1t19wjb94j9bi.htm) guide.

2. Review the list of HPA transfomers in the current directory's [kustomization.yaml](./kustomization.yaml). Remove any transformers that are not required for your Viya environment.

3. Once the transformers are in place, follow the instructions in [Modifying Existing Customizations in a Deployment](https://go.documentation.sas.com/doc/en/sasadmincdc/v_045/dplyml0phy0dkr/n1f2q6pp0gjheqn1jl204vptrubs.htm) to re-deploy.
