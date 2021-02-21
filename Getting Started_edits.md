# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this guide, you'll learn to install Terraform, configure and provision infrastructure resources, and destroy infrastructure that you no longer need.

## Prerequisites 
 - Thing 1
 - Thing 2


## Install Terraform

First, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the binary package for your operating system and architecture. 

To install Terraform, unzip the package and put the binary in a directory that is in your system's `PATH` environment variable. 

Verify installation success by typing `terraform version`. The output for a successful installation shows the Terraform version.

```shell
Terraform v0.14.7
```

## Build infrastructure

Now that you have Terraform installed, you can define and provision your infrastructure. 

We recommend that you create a new directory on your local machine and create Terraform configuration code inside it. For this guide, create a `terraform-demo` directory, and change to the new directory.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your configuration code. The `.tf` extension indicates that this is a Terraform configuration file. 

```shell
$ touch main.tf
```

Paste the following lines into the file and save it. The content of this configuration describes the infrastructure objects that it will create. 

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

Initialize the configuration directory using the `init` command. This installs the Docker provider.

```shell
$ terraform init
```
You'll see output similar to the following when the initialization is successful. (If you see error messages, follow the recommended steps to address the issues, and re-run the `init` command.)

```shell
Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

After the configuration directory is initialized, you can provision the resources using the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message indicating that the resource was created.

## Destroy infrastructure

Finally, destroy the infrastructure to remove the resources that were created by this configuration.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and press ENTER. Terraform will destroy the resources it had created earlier.

## Next steps

Now you know how to configure and provision resources using hard-coded values. In the next guide, you'll learn how to use variables to ***

For more information, see [Terraform Documentation](https://www.terraform.io/docs/index.html).


