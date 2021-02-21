# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this guide, you'll learn to install Terraform, configure and provision infrastructure resources, and destroy infrastructure that you no longer need.

## Prerequisites 
 - Visit [Terraform.io](https://www.terraform.io/downloads.html) and download the binary package for your operating system and architecture. 
 - Download and install [Docker Desktop](https://www.docker.com/products/docker-desktop).


## Install Terraform

To install Terraform, unzip the Terraform binary package that you downloaded and put the binary in a directory that is in your system's `PATH` environment variable. 

Open a terminal session and verify installation success by typing `terraform version`. The output for a successful installation shows the Terraform version.

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

The command may take up to a few minutes to run and will display a message indicating that the resource was created. The output will show you the changes that are to be made to the resources, and asks whether you want to perform the actions. 

```shell
 # docker_image.nginx will be created
  + resource "docker_image" "nginx" {
      + id     = (known after apply)
      + latest = (known after apply)
      + name   = "nginx:latest"
      + output = (known after apply)
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
```
Type `yes` to apply and perform the actions and create the resources.

```shell
docker_image.nginx: Creating...
docker_image.nginx: Creation complete after 9s [id=sha256:35c43ace9216212c0f0e546a65eec93fa9fc8e96b25880ee222b7ed2ca1d2151nginx:latest]
docker_container.nginx: Creating...
docker_container.nginx: Creation complete after 1s [id=f1a277895a26b9198721f94874c947f8728cc893c565cc7300a1eb2a25363cbe]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```

## Destroy infrastructure

Finally, destroy the infrastructure to remove the resources that were created by this configuration.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and press ENTER. Terraform will destroy the resources it had created earlier.

## Next steps

Now you know how to configure and provision resources using hard-coded values. In the next guide, you'll learn how to use variables to ***

For more information, see [Terraform Documentation](https://www.terraform.io/docs/index.html).


