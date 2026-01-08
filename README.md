# APLZ Repo showing all the boot strap downloads 

**Inputs YAML Differences**
- **Found files:**
	- [accelerator/gitub/bicep/config/inputs.yaml](accelerator/gitub/bicep/config/inputs.yaml)
	- [accelerator/gitub/ scenario_1/config/inputs.yaml](accelerator/gitub/ scenario_1/config/inputs.yaml)
	- [accelerator/gitub/ scenario_2/config/inputs.yaml](accelerator/gitub/ scenario_2/config/inputs.yaml)
	- [accelerator/gitub/ scenario_3/config/inputs.yaml](accelerator/gitub/ scenario_3/config/inputs.yaml)
	- [accelerator/gitub/ scenario_4/config/inputs.yaml](accelerator/gitub/ scenario_4/config/inputs.yaml)
	- [accelerator/gitub/ scenario_5/config/inputs.yaml](accelerator/gitub/ scenario_5/config/inputs.yaml)
	- [accelerator/gitub/ scenario_6/config/inputs.yaml](accelerator/gitub/ scenario_6/config/inputs.yaml)
	- [accelerator/gitub/ scenario_7/config/inputs.yaml](accelerator/gitub/ scenario_7/config/inputs.yaml)
	- [accelerator/gitub/ scenario_8/config/inputs.yaml](accelerator/gitub/ scenario_8/config/inputs.yaml)
	- [accelerator/azure-devops/bicep/config/inputs.yaml](accelerator/azure-devops/bicep/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_1/config/inputs.yaml](accelerator/azure-devops/scenario_1/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_2/config/inputs.yaml](accelerator/azure-devops/scenario_2/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_3/config/inputs.yaml](accelerator/azure-devops/scenario_3/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_4/config/inputs.yaml](accelerator/azure-devops/scenario_4/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_5/config/inputs.yaml](accelerator/azure-devops/scenario_5/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_6/config/inputs.yaml](accelerator/azure-devops/scenario_6/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_7/config/inputs.yaml](accelerator/azure-devops/scenario_7/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_8/config/inputs.yaml](accelerator/azure-devops/scenario_8/config/inputs.yaml)
	- [accelerator/azure-devops/scenario_9/config/inputs.yaml](accelerator/azure-devops/scenario_9/config/inputs.yaml)
	- [accelerator/local/bicep/config/inputs.yaml](accelerator/local/bicep/config/inputs.yaml)
	- [accelerator/local/scenario_1/config/inputs.yaml](accelerator/local/scenario_1/config/inputs.yaml)
	- [accelerator/local/scenario_2/config/inputs.yaml](accelerator/local/scenario_2/config/inputs.yaml)
	- [accelerator/local/scenario_3/config/inputs.yaml](accelerator/local/scenario_3/config/inputs.yaml)
	- [accelerator/local/scenario_4/config/inputs.yaml](accelerator/local/scenario_4/config/inputs.yaml)
	- [accelerator/local/scenario_5/config/inputs.yaml](accelerator/local/scenario_5/config/inputs.yaml)
	- [accelerator/local/scenario_6/config/inputs.yaml](accelerator/local/scenario_6/config/inputs.yaml)
	- [accelerator/local/scenario_7/config/inputs.yaml](accelerator/local/scenario_7/config/inputs.yaml)
	- [accelerator/local/scenario_8/config/inputs.yaml](accelerator/local/scenario_8/config/inputs.yaml)
	- [accelerator/local/scenario_9/config/inputs.yaml](accelerator/local/scenario_9/config/inputs.yaml)

- **Common keys (present in all files):** bootstrap_location, root_parent_management_group_id, subscription_ids, bootstrap_subscription_id, service_name, environment_name, postfix_number.

- **Platform / provider differences:**
	- GitHub-targeted files include: `github_personal_access_token`, `github_runners_personal_access_token`, `github_organization_name`, `apply_approvers` and use the flag `use_self_hosted_runners`.
	- Azure DevOps-targeted files include: `azure_devops_personal_access_token`, `azure_devops_agents_personal_access_token`, `azure_devops_organization_name`, `azure_devops_project_name`, `apply_approvers` and use the flag `use_self_hosted_agents`.
	- Local-targeted files include: `create_bootstrap_resources_in_azure`, `grant_permissions_to_current_user`, `target_directory`.

- **`iac_type` and `bootstrap_module_name` differences:**
	- Files vary between `iac_type: "terraform"` and `iac_type: "bicep"` depending on the folder; `bootstrap_module_name` maps to the target provider (examples: `alz_github`, `alz_azuredevops`, `alz_local`).

- **Notes:**
	- The top-level decision keys (region, management group, subscription ids, naming) are consistent placeholders across files.
  
	- Use this summary to know which inputs to set depending on whether you plan to bootstrap via GitHub, Azure DevOps, or locally.

