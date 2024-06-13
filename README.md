# Deploy API Action

## Instructions

1. Add the base repo with `helm repo add ganiulis https://ganiulis.github.io/charts`.
2. Fetch the `values.yaml` example with `helm show values ganiulis/api-template > values.yaml`.
3. Tweak the `values.yaml` file according to your needs and leave it somewhere in your repository.
4. Set a base64-encoded `kubeconfig` secret. See https://github.com/wahyd4/kubectl-helm-action?tab=readme-ov-file#how-to-use for details.

## Example

```yaml
name: Deploy

on:
  workflow_dispatch:
    inputs:
      tag:
        description: Image tag to deploy
        required: true
        type: string
        default: latest

jobs:
  deploy-api:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: ganiulis/deploy-api-action@0.1.1
        with:
          values-yaml: charts/values.yaml
          kube-config-data: "${{ secrets.KUBECONFIG }}"
          tag: "${{ inputs.tag }}"
```
