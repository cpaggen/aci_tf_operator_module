basic ACI demo terraform module
===============================

A terraform module to create a minimal tenant on an ACI fabric

This module is meant to be called by the TF K8s Operator.
Because the ACI provider does not accept configuration from env_variables,
and because standard TF modules never contain provider configuration,
and because there is way for the TF K8s Operator to pass provider configuration variables, 
this module somewhat deviates from the norm in the sense that it specifies the provider configuration.

That way, the TF K8s Operator can pass provider configuration variable when calling the module.

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
  source = "github.com/my-repo/demo"
  aciUser = "admin"
  aciPassword = "secret"
  aciUrl = "https://10.20.30.40"
  tenantName = "foo"
  vrfName = "vrf1"
  bdName = "bd1"
  bdSubnet = "192.168.1.1/24"
}
```


Outputs
=======

 - `name` - does what it says on the tin
 - `environment` - does what it says on the tin


Authors
=======

name.surname@company.com
