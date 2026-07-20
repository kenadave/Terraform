1) terraform init : Downloads local provider plugins

2) terraform plan

# The provider block can be left completely empty
provider "local" {}

# The resource block requires filename and a content source
resource "local_file" "example" {
  filename = "${path.module}/outputs/config.txt"
  content  = "Hello, Terraform!"
}

https://registry.terraform.io/providers/hashicorp/local/latest/docs/resources/file

That's right, we have made use of the local_sensitive_file resource type to mask the contents of the file from the execution plan.

3) hostname/organizational namespace/type
hostname can be omitted

4) Use variables.tf file for variable names and use var. for accessing in the main.tf file

5) There can be multiple providers. It can be Official, Partner, or Community. Check https://registry.terraform.io/namespaces/ for it.

6) While declaring variables, it can be empty. In that case it will ask for values when doing Terraform apply.
or we can also use -var flag in terraform apply
or we can also use environment variables like TF_VAR_filename

7) If so many variables then name file as .tfvars or .tfvars.json which consists of only variable assignments

8) output "id1" {
   value = random_uuid.id1.result
}

9) Purpose of state :
- used while deleting resorces to know which one to delete first
- used in improving performance when many resources are there
- the cached file, terraform will refer to the same file everytime and wont refresh everytime. use --refresh=false

10) terraform init => state file does not change
11) terraform plan  -------------
                                | => state file changes  
12) terraform apply -------------
13) terraform validate 
14) terraform show
15) terraform providers, terraform providers mirror
16) Terrform generates immutable resources
17) 
output "os-version" {
  value = data.local_file.content
}
data "local_file" "content" {
  filename = "/etc/os-release"
}
data source which does not create, update or delete the resource, but it is just used to read the file created by other resource
18)
18) terraform format/fmt
19) terraform apply -refresh-only
20) terraform
21) terraform output
22) terraform graph
23) terraform state show local_file.data
24) lifecycle rules: create_before_destroy, prevent_destroy, ignore_changes
25) 
variables.tf
variable "users" {
    type = list(string)
    default = [ "/root/user10", "/root/user11", "/root/user12", "/root/user10"]
}
variable "content" {
    default = "password: S3cr3tP@ssw0rd"
    
}

main.tf
resource "local_file" "example"{
    for_each = toset(var.users)
    filename = each.value
    content = var.content
}
