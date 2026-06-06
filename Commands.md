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
