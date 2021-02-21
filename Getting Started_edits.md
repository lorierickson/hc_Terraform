# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this guide, you'll learn to install Terraform, configure and provision infrastructure resources, and destroy infrastructure that you no longer need.

## Prerequisites 
 - Thing 1
 - Thing 2


## Install Terraform

First, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the binary package for your operating system and architecture. 

To install Terraform, unzip the package and put the binary in a directory that is in your system's `PATH`. Verify installation success by typing `terraform version`.

```shell
Terraform v0.14.7
```
With Terraform installed, let's dive right into it and start creating some infrastructure.

We recommend that you create a new directory on your local machine and create Terraform configuration code inside it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code. The `.tf` extension indicates that this is a Terraform configuration file.

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

Initialize Terraform with the `init` command. The AWS provider will be installed. ***AWS??***

```shell
$ terraform init
```
Initializing the backend...

Initializing provider plugins...
- Finding latest version of kreuzwerker/docker...
- Installing kreuzwerker/docker v2.11.0...
- Installed kreuzwerker/docker v2.11.0 (self-signed, key ID 24E54F214569A8A5)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

You shoud check for any errors. 
If it ran successfully, provision the resource with the `apply` command.

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

Now you know how to configure and provision resources using hard-coded values. In the next guide, you'll learn how to use variables to ***

For more information, see [Terraform Documentation](https://www.terraform.io/docs/index.html).


