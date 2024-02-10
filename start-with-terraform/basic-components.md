---
description: >-
  In this page, you will learn the basic and essential components of Terraform.
  They are the fundamental knowledge of Terraform and Infrastructure as Code.
---

# Basic Components

In the preceding section, we explored the basics of Infrastructure as Code and got to know Terraform. Now, let's highlight one for Terraform's coolest features: its **declarative philosophy.** This approach allows you to define and set up infrastructure resources using a simple configuration language. Terraform only looks at where you are (initial state) and where yo want to be (destination state), applying only the right and necessary changes to get there. Which means, you don't have to worry about what's happening in between or write loads of extra code.

The core Terraform workflow consists of only four steps:

* **init** -- Initialize your workspace so Terraform can apply your code.
* **write** -- Express your infrastructure needs using code. Just like telling Terraform what you want in a language it understands.
* **plan** -- Get a sneak peek at all the changes Terraform is about to make, so you're always in the know and avoid the human-error.
* **apply** -- Execute the changes from your plan, and watch Terraform create, update, or destroy resources as needed.

## init

The first command to run for a new configuration—or after checking out an existing configuration from version control—is `terraform init`. This will initialize various local settings and data that will be used by subsequent commands.

```bash
terraform init
```

Although the concise description is only just two words, this command undertakes various essential tasks behind the scenes. For instance,  it initializes the associated backend, whether local or remote. In cases where the configuration involves provider plugins, the command seamlessly downloads and installs the required provider plugins. Furthermore, `terraform init` sets up modules if they exist in your code.  Additionally, the command takes care of the automatic setup of the local Terraform state, streamlining the overall configuration process.

## plan

## apply

## variables

## outputs

## provider

## versions


