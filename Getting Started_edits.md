# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this guide, you'll learn to install Terraform, to configure and provision resources, and to destroy resources that you no longer need.

## Prerequisites 
 - Download the Terraform binary package for your operating system and architecture from [Terraform.io](https://www.terraform.io/downloads.html).
 - Thing 2


## Install Terraform

First, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the binary package for your operating system and architecture. 

To install Terraform, unzip the package
With Terraform installed, let's dive right into it and start creating some infrastructure.

We recommend that you create a new directory on their local machine and create Terraform configuration code inside it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

You shoud check for any errors. If it ran successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message indicating that the resource was created.

## Destroy infrastructure

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and press ENTER. Terraform will destroy the resources it had created earlier.

## Next steps

Now you know how to configure and provision resources using hard-coded values. In the next guide, you'll learn how to use variables to 
For more information, visit 


