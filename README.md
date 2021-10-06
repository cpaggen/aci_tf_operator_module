basic ACI demo terraform module
===============================

A PoC-quality Terraform module that creates a minimal tenant on an ACI fabric.

*Attention*: this module is meant to be called by the TF Cloud K8s Operator [link](https://github.com/hashicorp/terraform-k8s).

Because the ACI provider does not accept configuration from env_variables,
and because standard TF modules never contain provider configuration,
and because there is no way for the TF K8s Operator to pass provider configuration variables, 
this module somewhat deviates from the norm in the sense that it specifies the provider configuration.

That way, the TF K8s Operator can pass provider configuration variable when calling the module. Be aware that if you flag a variable as *sensitive*, you must then define it into a K8s secret that's read by the operator. You must then base64-decode the stored value for that variable when passing it to a module. That's just how the TF Cloud K8s Operator works, not my rule :)

Module Input Variables
----------------------

- `aciUser` - ACI provider username
- `aciPassword` - ACI provider password
- `aciUrl` - ACI provider URL
- `tenantName` - name of the tenant 
- `tenantDescr` - optional description for the tenant
- `tenantAlias` = optional alias for the tenant 
- `vrfName` - name of the VRF under this tenant
- `vrfDescr` - optional description for the VRF
- `bdName` - name of the under the VRF
- `bdDescr` - optional description for the BD
- `bdSubnet` - subnet/mask for the BD

Usage
-----

```hcl
module "aci" {
  source = "github.com/cpaggen/aci_tf_operator_module"
  aciUser = "admin"
  aciPassword = "secret"
  aciUrl = "https://10.20.30.40"
  tenantName = "foo"
  vrfName = "vrf1"
  bdName = "bd1"
  bdSubnet = "192.168.1.1/24"
}
```
As this is meant to be called within the TF Cloud K8s Operator,
you typically invoke this module like so: 

![workspace.yaml](https://github.com/cpaggen/aci_tf_operator_module/blob/master/TF_cloud_operator_workspace_yml.png?raw=true)

Outputs
=======

None in this current version. If your workspace successfully executes your plan, you will see something similar to this: ![plan_ran](https://github.com/cpaggen/aci_tf_operator_module/blob/master/TF_cloud_operator_runs_ACI_plan.png?raw=true)


Authors
=======

cpaggen@gmail.com
