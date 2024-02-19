# Create your first Storage Bucket

In the Google Cloud Platform, we have multiple ways to create a storage bucket. Today we will learn how to create one with Terraform.

You need to have a google cloud account to use the platform.&#x20;

1. In the Google Cloud console, click the button on the upper-right corner, activate Cloud Shell.
2. Set the default Google Cloud project where you want to apply your Terraform configuration, using your own `PROJECT_ID` &#x20;

```
export GOOGLE_CLOUD_PROJECT=PROJECT_ID  
```

3. In the Cloud Shell terminal, set the home directory as the active directory

```
cd
```

3. Create a new folder named 'terraform'

```
mkdir terraform   # make a directory
```

4. &#x20;enter the 'terraform' directory and create a new file called 'main.tf'

```
cd terraform
touch main.tf
```

4. Launch the Cloud Shell Editor by clicking **Open Editor** on the toolbar of the Cloud Shell window and then open the 'main.tf' file.
5. Now we will write some code into the 'main.tf' and create a new storage bucket in the US multiple region.

```sh
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

resource "google_storage_bucket" "static" {
 name          = "BUCKET_NAME"  # give your unique bucket name
 location      = "US"
 storage_class = "STANDARD"

 uniform_bucket_level_access = true
}

```

5. Save the file and go back to the terminal.
6. Initialize the  Terraform configuration

```
terraform init
```

7. Review the change

```
terraform plan
```

8. Apply the change

```
terraform apply
```

We also can examine the result in the platform. We can go to the Cloud Storage - Buckets dashboard and check where the new storage exists.

## Key Points

```
terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
      version = "3.5.0"
    }
  }
}
```

#### 1. Terraform block

The `terraform {}` block is required so Terraform knows which provider to download from the [Terraform Registry](https://registry.terraform.io/). In the configuration above, the `google` provider's source is defined as `hashicorp/google` which is shorthand for `registry.terraform.io/hashicorp/google`.

#### 2. Providers

The `provider` block is used to configure the named provider, in this case `google`. A provider is responsible for creating and managing resources. Multiple provider blocks can exist if a Terraform configuration manages resources from different providers.
