Notes about building Terraform Modules
When building a module, consider three areas:

    * Encapsulation: Group infrastructure that is always deployed together. Including more infrastructure in a module makes it easier for an end user to deploy that infrastructure but makes the module's purpose and requirements harder to understand

    * Privileges: Restrict modules to privilege boundaries. If infrastructure in the module is the responsibility of more than one group, using that module could accidentally violate segregation of duties. Only group resources within privilege boundaries to increase infrastructure segregation and secure your infrastructure

    * Volatility: Separate long-lived infrastructure from short-lived. For example, database infrastructure is relatively static while teams could deploy application servers multiple times a day. Managing database infrastructure in the same module as application servers exposes infrastructure that stores state to unnecessary churn and risk.
A simple way to get start with creating modules is to:

- Always aim to deliver a module that works for at least 80% of use cases.
- Never code for edge cases in modules. An edge case is rare. A module should be a reusable block of code.
- A module should have a narrow scope and should not do multiple things.
- The module should only expose the most commonly modified arguments as variables. Initially, the module should only support variables that you are most likely to need.

## Task 3: Publishing to the Terraform Public Module Registry

Anyone can publish and share modules on the Terraform Registry, but there are some requirements that you should be aware of:

- The module must be on GitHub and must be a public repo. This is only a requirement for the public registry. If you're using a private registry, you may ignore this requirement.
- Module repositories must use a naming format: `terraform-<PROVIDER>-<NAME>` where <NAME> reflects the type of infrastructure the module manages and <PROVIDER> is the main provider where it creates that infrastructure. The <NAME> segment can contain additional hyphens. Examples: terraform-google-vault or terraform-aws-ec2-instance.
- The module repository must have a description which is used to populate the short description of the module. This should be a simple one sentence description of the module.
- The module must adhere to the standard module structure, `main.tf`, `variables.tf`, `outputs.tf` This allows the registry to inspect your module and generate documentation, track resource usage, parse submodules and examples, and more.
- x.y.z tags for releases. The registry uses tags to identify module versions. Release tag names must be a semantic version, which can optionally be prefixed with a v. For example, v1.0.4 and 0.9.2. To publish a module initially, at least one release tag must be present. Tags that don't look like version numbers are ignored.