# Conditional Access for Zero Trust Resources Terraform Deployment

## Terraform Code

This Repository creates Sample Conditional Access Policies based on the[ConditionalAccessforZeroTrustResources](https://github.com/microsoft/ConditionalAccessforZeroTrustResources) framework from Microsoft

* `azuread_conditional_access_policy.tf` - Creates Conditional Access Policies for Entra ID based on the suggested policy in  [Microsoft Azure AD Conditional Access principles and guidance](https://github.com/microsoft/ConditionalAccessforZeroTrustResources/blob/main/ConditionalAccessGovernanceAndPrinciplesforZeroTrust%20October%202023.pdf).

* `azuread_group.tf` - Creates the Entra ID Persona Groups for Conditional Access Policies based on the guidance.

```hcl
persona_types = [
    "Internals",
    "Developers",
    "Externals",
    "Guests",
    "GuestAdmins",
    "CorpServiceAccounts",
    "Admins",
    "WorkloadIdentities",
  ]
  policy_types = [
    "BaseProtection",
    "AppProtection",
    "IdentityProtection",
    "DataProtection",
    "AttackSurfaceReduction",
  ]
  ring_types = [
    "Ring0",
    "Ring1",
    "Ring2",
    "Ring3",
  ]

```

* `azuread_named_location.tf` - Creates the Named Locations for Conditional Access Policies based on the guidance.

* `data.tf`- Creates the data sources for the Conditional Access Policies based on the guidance. In this case, we have used it to import the Microsoft Intune Enrollment Application which is excluded from one of the Conditional Access Policies.

## Deployment

that automates the process of generating and applying Terraform plans for infrastructure changes. The workflow has two jobs: "terraform-plan" and "terraform-apply".

The `terraform-plan` job checks out the repository, installs the latest version of the Terraform CLI, initializes a new or existing Terraform working directory, checks that all configuration files adhere to a canonical format, logs in to Azure CLI with federated credentials, generates an execution plan for Terraform, saves the plan to artifacts, creates a string output of the Terraform plan, and publishes the Terraform plan as a task summary.

The `terraform-apply` job checks out the repository, installs the latest version of the Terraform CLI, logs in to Azure CLI with federated credentials, initializes a new or existing Terraform working directory, downloads the saved plan from artifacts, and applies the Terraform plan if there are pending changes.

As evident please update your GitHub Action secrets with the following values:

```hcl
AZURE_CLIENT_ID 
AZURE_TENANT_ID 
ARM_ACCESS_KEY 
```
