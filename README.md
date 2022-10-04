
# Reusable Workflows to use in your GitHub Actions Pipelines

Some common workflows that could be reusable across multiple projects.

## Workflows

```text
.github/
└── workflows
    ├── staticCodeAnalysis.yml
    └── terraformAzure.yml

```

### Tflint

A Pluggable [Terraform](https://www.terraform.io/) Linter. The key features are:

- Find possible errors (like invalid instance types) for Major Cloud providers (AWS/Azure/GCP).
- Warn about deprecated syntax, unused declarations.
- Enforce best practices, naming conventions.

#### Input Parameters

| Parameter Name | Type | Default Value | Description |
| :-- | :-- | :-- |:-- |
| `tflint-version` | string | 0.41.0 | tflint version to use. |
| `project-folder` | string | current folder | The folder containing the terraform project. |

### Terraform-Azure

A template workflow to do terraform deployments in Azure. Some key features are:

- Downloading a specific version of Terraform CLI and adding it to the `PATH`.
- Configuring the [Terraform CLI configuration file](https://www.terraform.io/docs/commands/cli-config.html) with a Terraform Cloud/Enterprise hostname and API token.
- Installing a wrapper script to wrap subsequent calls of the `terraform` binary and expose its STDOUT, STDERR, and exit code as outputs named `stdout`, `stderr`, and `exitcode` respectively. (This can be optionally skipped if subsequent steps in the same job do not need to access the results of Terraform commands.)

#### Input Parameters

| Parameter Name | Type | Default Value | Allowed Values | Description |
| :-- | :-- | :-- | :-- | :-- |
| `outputResourceID` | Strig |  |  | The Azure Resource ID to output once the deployment is complete. |
| `destroy-environment` | boolean | true | true/false | Destroy the environment after the workflow is finished. |
| `environment` | string | Dev | Ideally this should match the GitHub Environments. | Environment to deploy. |
| `terraform-version` | string | 1.3.0 |  | terraform version to use. |
| `project-folder` | string | current folder |  | The folder containing the terraform project. |
| `cloud-type` | string | public | Possible values are `public`, `china`, `german`, `stack` and `usgovernment`. | The cloud type to use. |

#### Secrets

| Secret Name | Description |
| :-- | :-- |
| `TF_API_TOKEN` | Terraform Cloud user API token. |
| `ARM_SUBSCRIPTION_ID` | Azure subscription ID. |
| `ARM_CLIENT_ID` | Azure client ID. |
| `ARM_CLIENT_SECRET` | Azure client secret. |
| `ARM_TENANT_ID` | Azure tenant ID. |

#### Outputs

| Output Name | Description |
| :-- | :-- |
| `resourceID` | Resource ID to output once the workflow is completed. |

## Authors

- Marcelo Zambrana
