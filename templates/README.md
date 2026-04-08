# Templates

This directory contains reusable templates for SAS Viya tuning configurations.

## Available Templates

- **`patch-transformer-resource-limits.yaml.template`** - Patch CPU and memory resource limits for Kubernetes Deployments

## patch-transformer-resource-limits.yaml.template

### Overview

The `patch-transformer-resource-limits.yaml.template` is a template for creating Kustomize PatchTransformer manifests that modify CPU and memory resource limits for Kubernetes Deployments in SAS Viya.

### Purpose

This template standardizes the way resource limits are patched across different services in your SAS Viya deployment, ensuring consistent formatting and structure.

### Template Variables

The template uses the following placeholders that should be replaced with actual values:

- **`{{ SERVICE_NAME }}`** - The name of the Kubernetes Deployment to patch (e.g., `sas-compute`, `sas-studio`, `sas-launcher`)
- **`{{ CPU_LIMIT }}`** - CPU limit in CPU units (e.g., `4000m`, `2000m`, `1000m`)
- **`{{ MEMORY_LIMIT }}`** - Memory limit in bytes (e.g., `2Gi`, `4Gi`, `8Gi`)

### Usage

1. **Create a descriptive custom tuning folder** in the `configurations/` directory to organize your tuning files

   Example folder names for environment-specific tunings:
   ```
   configurations/acme-tuning/
   configurations/qa-performance-tuning/
   configurations/prod-resource-optimization/
   configurations/highavailability-tuning/
   ```

2. **Copy the template** into your new folder and rename it to match your service (remove `.template` extension)

   ```bash
   mkdir -p ../configurations/acme-tuning/sas-compute
   cp patch-transformer-resource-limits.yaml.template ../configurations/acme-tuning/sas-compute/resource-limits.yaml
   ```

3. **Replace the placeholders** with your desired values:
   - Replace `{{ SERVICE_NAME }}` with your Deployment name
   - Replace `{{ CPU_LIMIT }}` with the desired CPU limit
   - Replace `{{ MEMORY_LIMIT }}` with the desired memory limit
   - If you only need CPU or memory changes, remove the other patch entry from the template

4. **Example Result**

   If you substitute the variables with:
   - `SERVICE_NAME` = `sas-compute`
   - `CPU_LIMIT` = `4000m`
   - `MEMORY_LIMIT` = `2Gi`

   You'll get:

   ```yaml
   ---
   apiVersion: builtin
   kind: PatchTransformer
   metadata:
     name: sas-compute-resource-limits-tuning
   patch: |-
     - op: replace
       path: /spec/template/spec/containers/0/resources/limits/cpu
       value: 4000m
     - op: replace
       path: /spec/template/spec/containers/0/resources/limits/memory
       value: 2Gi
   target:
     group: apps
     kind: Deployment
     name: sas-compute
     version: v1
   ```

### Common CPU and Memory Values

These values are guidelines (rule-of-thumb starting points), not strict recommendations. Final CPU and memory limits should be tuned based on each service's behavior and the expected workload volume and concurrency.

- **Small services** (low resource): CPU: `500m`, Memory: `512Mi`
- **Standard services**: CPU: `1000m` - `2000m`, Memory: `1Gi` - `2Gi`
- **Large services** (compute-intensive): CPU: `4000m` - `8000m`, Memory: `4Gi` - `8Gi`

### Integration with Kustomization

1. Create a `kustomization.yaml` file in your tuning folder:

   ```yaml
   # configurations/acme-tuning/kustomization.yaml
   resources:
     # Custom tuning
     - sas-compute/resource-limits.yaml
     # Add more services as needed:
     # - sas-studio/resource-limits.yaml
     # - sas-launcher/resource-limits.yaml

   transformers:
     # Custom tuning
     - sas-compute/resource-limits.yaml
     # Add more services as needed:
     # - sas-studio/resource-limits.yaml
     # - sas-launcher/resource-limits.yaml
   ```

2. Add your custom tuning folder to the master `kustomization.yaml` file located in `configurations/kustomization.yaml`:

   Edit `configurations/kustomization.yaml` and add your custom tuning folder to the `resources` list:

   ```yaml
   resources:
     - analytics-model-building
     - analytics-model-management
     - compute-common
     - platform-common
     - platform-crunchy-postgres
     - acme-tuning          # Add your custom tuning folder here
   ```

   This ensures your custom PatchTransformer configurations are applied when deploying the entire SAS Viya environment.

