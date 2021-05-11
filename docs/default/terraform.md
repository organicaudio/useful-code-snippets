# Terraform

- "Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. Terraform codifies cloud APIs into declarative configuration files."
- [Example tf files](https://gist.github.com/CrowdSalat/bcab0fdf534d7cadb9714079066e9013)
- [official documentation](https://www.terraform.io/docs/index.html)
- [official learn stuff](https://learn.hashicorp.com/terraform)
- you can also [import existing infrastructure](https://www.terraform.io/docs/import/index.html) into terraform

## Setup

- Install [manually](https://www.terraform.io/downloads.html) or use a [repository manager](https://www.terraform.io/docs/cli/install/apt.html) 
- enable autocomplete `terraform -install-autocomplete`
- Read provider specific setup documentation on [terraform registry](https://registry.terraform.io/browse/providers) or [here](https://www.terraform.io/docs/providers/) 
- Create folder, create your tf files and run: `terraform init && terraform apply`

## Wording

- a ``provider`` creates and manages resources. They wrap the API of a service (provider) like AWS, Azure or GCP.
- If you use multiple providers you can qualifiy which provider uses which resource.
- a ``resource`` might be a physical resource like a aws EC2 instance or a logical resource like a application.
- A resource has a type and a name (e.g. ``resource "aws_instance" "example"`{...}``)and can be configured inside the curly brackets.
- a `datasource` is a way to get information about existing infrastructure (mostly useful when it is not managed by terraform or by another terraform configuration)
- a set of .tf files is called a **terraform configuration**

## CLI

```shell
terraform init # initializes various local settings 
terraform fmt # format all files in directory
terraform validate # validate file

terraform apply # checks diff between config file and real infrastructure and creates execution plan to eliminate this diff

terraform state # The state of the infrastructure is saved in terraform.tfstate file. It can be manually modified by this command.

terraform destroy # completely destroys the Terraform-managed infrastructure
```

## Resource Dependencies

There are explicit and implicit dependencies for creating a order of actions.

- explicit: with the ``depends_on`` field of a resource.
- implicit: e.g. usage of ``instance = aws_instance.example.id``

Resources which are not dependant on others can be build in parallel.

## Provisioning

- Only necessary if you do not use image-based infrastructure (you can create images with vagrant or packer).
- "can be used to model specific actions on the local machine or on a remote machine in order to prepare servers or other infrastructure objects for service."
- is not declarative
- provisioner are defined inside a resource and have a type like: ``local-exec`` or ``remote-exec``
- Are for bootstrapping components (on creation) not to change software on a running component.
- **You need to destroy the infrastructure if the resource already exist, so the resource will be recreated and the bootstrapping logic of the provisioner can be done.**
- If a resource successfully creates but fails during provisioning, Terraform will error and mark the resource as "tainted".
- Terraform tries to destroy and recreate tainted resources every time *apply* ist called.
- ``terraform taint <resource.id>`` manually marks a resource as tainted.


## Input Variables

[Official documentation](https://www.terraform.io/docs/configuration/variables.html)

### How to use variable

```hcl
var.my_api_token

#use nested var
var.system.name
#use list
element(var.system.used_port, 0)
# use map
lookup(var.system.port_app, "80", "default_val")
```
### How to declare a variable

```hcl
# with default value and description
variable "my_api_token" {
  type        = string # number, bool, list(<TYPE>), map(<TYPE>) etc.
  description = "An API token."
  default = "1234-5679-123"
  #sensitive=true #does not show value in logs
}

# nested variable
```hcl
variable "system" {
  type = object({
    name      = string
    used_ports = list(string)
    port_app = map(string)
  })
  default = object({
    name      = "VLS"
    used_ports = ["80","43"]
    port_app ={"80":"http","43":"https"}
  })
}

```
### Where to initialize variable: 

 In a nutshell:

- preset in variables.tf file via the *default* field
- overwrite console (``-var 'var_name=var_value'``)
- overwrite in terraform.tfvars file
- overwrite in *.tfvars file and  (``-var-file 'production.tfvars'``)
- overwrite in environmental variables (TF_VARS_)

A bit more extensive:

- variables are defined in a *variables.tf* file and may be assigned a default value
- variables are accessed with a `var.<variable_name>` notation.
- variables can be overwritten in console: `terraform apply -var 'region=us-east-2'`
- variables can also be overwritten from file. Terraform search automatically for *terraform.tfvars* or *.auto.tfvars* files. Alternatively you can pass a file in console `terraform apply -var-file 'production.tfvars'`.
- variables can be overwritten by environment variables. They need to start with **TF_VAR_***<name of variable to overwrite>*. Environment variables are limited to string-type variables (can not use List and map type variables).
- variables which are unspecified are asked for after executing ``terraform apply``

### Variable Types

#### Lists

```hcl
# define
variable "cidrs" { type = list }`

# init
cidrs = [ "10.0.0.0/16", "10.1.0.0/16" ]
```

### Maps


```hcl
# define and init
variable "amis" {
  type = "map"
  default = {
    "us-east-1" = "ami-b374d5a5"
    "us-west-2" = "ami-4b32be2b"
  }
}

# use
resource "aws_instance" "example" {
  ami           = var.amis["us-east-1"]
  instance_type = "t2.micro"
}

```

## Output Variables
`
Output blocks can be pasted in any of the *.tf files. Output are printed after ``terraform output`` or ``terraform apply`` are run.
In a rot module the label of the output block is showed to the user as the name of the variable. In a module the label can be used to reference the variable. You may need to prefix the variable with the terraform type like `data` or `var`.

Example:
```hcl
output "ip" {
  value = aws_eip.ip.public_ip
}
```

## modules

Modules are self-contained packages of Terraform configurations that are managed as a group. Any set of Terraform configuration files in a folder can be a module. The official modules can be downloaded from [Terraform Registry](https://registry.terraform.io/).

### use module

- After adding new modules you need to rerun ``terraform init`` not only ``terraform apply``
- ``terraform get`` will download the modules
- Modules reside under ~/.terraform/modules/<the module alias given in root tf script>
- You can define [from where to download the module](https://www.terraform.io/docs/modules/sources.html) via the `source` attribute of `module` 
    - local: `./my-module`
    - git: 'github.com/crowdsalat/examplemodule'
    - Terraform Registry: `source = 'hashicorp/consul/aws'`

Example for module usage via registry:

```hcl
module "consul" {
  source      = "hashicorp/consul/aws"
  version = "0.7.3" # optional
  num_servers = "3"
}
```

### create module

- A module is a bunch of .tf files in a directory
- The files are only for organization, terraform just merges them to one file before using 
- The name of the module is defined by the folder 

Files (convention):

- main.tf
- variables.tf: input parameters for the module  
- outputs.tf: return values of the module  
- backend.tf: define remote backend
- variables.tf: used variables


## Remote State Storage

- Use a **remote backend** to store state-data on a server.
- When not configured the state is stored locally in a terraform.tfstate file
- There are different backends. Terraform Cloud is one of such.

Google cloud backend example:

```hcl
 backend "gcs" {
    bucket = "existing-bucket-name"
  }
```

## expressions

[Documentation](https://www.terraform.io/docs/configuration/expressions/index.html)