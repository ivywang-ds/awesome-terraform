---
description: >-
  In this project, you will learn how to create a VPC network and a compute
  instance, how to update a resource and how to destroy a resource
---

# 2. Create a compute instance and change the resource

With the [ create a storage bucket ](create-your-first-storage-bucket.md)experience, it's likely you're already familiar with Terraform. Let's proceed to create another type of resource: a compute instance.

We will stay with the GCP Console.

## &#x20;1. Create a Virtual Private Cloud Network

1. Create a directory named 'terraform' and then create a file named `main.tf`

```bash
mkdir terraform
cd terraform
touch main.tf
```

2. Launch the Cloud Shell Editor by clicking **Open Editor** on the toolbar of the Cloud Shell window and then open the `main.tf` file.
3. Write some code into the `main.tf` and create a virtual private cloud network.

```hcl
# declare providers

terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
      version = "3.5.0"
    }
  }
}

provider "google" {

  project = "PROJECT ID"  #replace to your project id
  region  = "REGION"      #replae to your region
  zone    = "ZONE"        #replace to your zone
}
```

```hcl
# create the vpc network

resource "google_compute_network" "vpc_network" {
  name = "my-network"
}
```

<figure><img src="../.gitbook/assets/create a vpc network.png" alt=""><figcaption><p>Create a VPC network</p></figcaption></figure>

## 2. Create a Compute Instance

1. Go back to the `main.tf` and add a compute instance resource above the network \_interface chunk. It will look like this:

```hcl
resource "google_compute_instance" "vm_instance" {
  name         = "my-instance"
  machine_type = "e2-micro"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = google_compute_network.vpc_network.name
    access_config {
    }
  }
}
```

This code snippet is longer and have more arguments.  But it is still easy to read:

* We will create a compute instance names 'my-instance' and the machine type is 'e2-micro'.&#x20;
* The compute instance will use a Debian operating system, and will be connected to the VPC Network.

2. save the file and go back to the terminal.
3. Review the change and apply the change.

```bash
terraform plan
terrafrom apply   
```

<figure><img src="../.gitbook/assets/create a compute instance.png" alt=""><figcaption><p>Create a compute instance</p></figcaption></figure>

## 3. Change resource in updating

Consider this scenario: We are not managing one or two resources, instead, you need to manage hundreds resources including virtual machine, storage, network, and so on for multiple departments or multiple environments.  How can we find out the targeted resource as quickly as possible?

We can use `tags` argument to help us manage the resources.&#x20;

Here is the example. Go back to the `main.tf` file in a editor mode, add the snippet  to your "vm\_instance" so that it looks like this:

```hcl
resource "google_compute_instance" "vm_instance" {
  name         = "terraform-instance"
  machine_type = "e2-micro"
  tags         = ["dev", "machine-learning"]
  # ...
}
```

Then run the `terrform apply` to update the change.

<figure><img src="../.gitbook/assets/change in updating.png" alt=""><figcaption><p>Change resource in updating</p></figcaption></figure>

### &#x20;Overall check

<figure><img src="../.gitbook/assets/Check the resource management in Dashboard.png" alt=""><figcaption><p>Overall check resources in Dashboard</p></figcaption></figure>

In Google Cloud Platform, navigating to the VM instances dashboard reveals a setup including a network labeled `my-network` and an instance named `my-instance`, running on Debian OS. Additionally, the network is tagged with `dev` and `machine-learning` to categorize its usage and purpose.

## 4. Change resource in replacing

Here's an example. Navigate back to your `main.tf` file in editor mode and incorporate the following snippet into your "vm\_instance" configuration. While updating resources is commonly preferred,  there are instances where it becomes necessary to replace an existing resource rather than merely updating it. This need arises, for instance, when the cloud provider no longer supports updating the resource as per your current configuration, a scenario also referred to as a destructive change.

```hcl
  boot_disk {
    initialize_params {
      image = "cos-cloud/cos-stable"
    }
  }
```

Then run the `terrform apply` to update the change.

<figure><img src="../.gitbook/assets/change resource in replacing.png" alt=""><figcaption><p>Change resource in replacing</p></figcaption></figure>

The prefix `-/+` means that Terraform will destroy and recreate the resource, rather than updating it in-place. While some attributes can be updated in-place (which are shown with the `~` prefix), changing the boot disk image for an instance requires recreating it.

<figure><img src="../.gitbook/assets/Change in-replacing-2.png" alt=""><figcaption><p>Change resource in replacing- Done</p></figcaption></figure>

When the replacing is done, you will see the notification. One resource is destroyed and one is added.&#x20;



## 5. Destroy a resource

Having learned how to create and update a resource, let's proceed to deleting it. While rare in production, deletion is common in development, testing, and staging environments.

We can use the  `terraform destroy` command. It is very straightforward

```bash
terraform destroy
```

The `-` prefix indicates that the instance and the network will be destroyed. As with apply, Terraform shows its execution plan and waits for approval before making any changes.

<figure><img src="../.gitbook/assets/destroy resource.png" alt=""><figcaption><p>destroy resource</p></figcaption></figure>

Terraform intelligently sequences actions, similar to how it applies configurations with `terraform apply`. It enforces an order of operations to adhere to external constraints, such as Google Cloud's requirement for a VPC network to be devoid of resources before deletion. Leveraging a dependency graph, Terraform ensures that it only attempts to delete the network after all instances within it have been successfully destroyed, preserving operational integrity and compliance with cloud provider policies.



