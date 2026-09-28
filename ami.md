[terraform documentatino](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ami?utm_source=chatgpt.com)

# Find an Ubuntu AMI (Amazon Machine Image) from AWS
data "aws_ami" "ubuntu" {

  # If multiple AMIs match the filters,
  # select the newest/latest AMI
  most_recent = true

  # Ubuntu's official AWS account ID
  # This prevents Terraform from selecting an AMI
  # published by another AWS account
  owners = ["099720109477"]

  # Filter the AMI based on its name
  filter {
    # AWS AMI property to search
    name = "name"

    # Look for Ubuntu 24.04 (Noble) 64-bit server AMIs
    # The * is a wildcard, so it can match different versions/dates
    values = ["ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*"]
  }

  # Filter the AMI based on virtualization type
  filter {
    # Only select AMIs that use HVM virtualization
    name   = "virtualization-type"
    values = ["hvm"]
  }

  # Filter the AMI based on the root disk type
  filter {
    # Only select AMIs whose root device is backed by EBS
    name   = "root-device-type"
    values = ["ebs"]
  }
}

