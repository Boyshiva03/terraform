**Here are the steps to install Terraform and an explanation of the standard workflow involved in using it**

**Part 1: How to Install Terraform**

The installation method depends on your operating system. Using a package manager is generally the easiest and most maintainable way.

**For Windows**

Option A: Using Chocolatey (Recommended) If you have Chocolatey installed, open PowerShell as Administrator and run:

choco install terraform (PowerShell)


**Option B: Manual Installation**

Download: Go to the Terraform downloads page and download the Windows binary (ZIP file).

Extract: Unzip the file to a specific folder (e.g., C:\terraform).

Update Path:

Search for "Environment Variables" in Windows Search.

Click "Environment Variables" > Select Path under "System variables" > Click Edit.

Click New and add the path to your folder (e.g., C:\terraform).

Click OK to save.

**For Linux (Ubuntu/Debian)**

**Update and install dependencies:**

Bash

sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
Add the HashiCorp GPG key:

Bash

wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
Add the repository and install:

Bash

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt-get update
sudo apt-get install terraform

**Verification**: For any OS, verify installation by opening a new terminal/command prompt and typing:

Bash

terraform -version


==================================================================================================================

**Part 2: The Steps Involved (The Terraform Workflow)**

**1. Write (Configuration)**
You define the infrastructure you want in .tf files using HCL (HashiCorp Configuration Language).

What you do: Create a file named main.tf and define "resources" (like a virtual machine, storage bucket, or VPC).

Key Concept: You describe the desired state (e.g., "I want 3 servers"), not the instructions to build them.


**2. Initialize (terraform init)**
This is the first command you run after writing your code.

Command: terraform init

What it does: It looks at your configuration, determines which providers are needed (e.g., AWS, Azure, Google Cloud), and downloads the necessary plugins to your local machine. It also sets up the "backend" where your state file will be stored.

**3. Plan (terraform plan)**
This is a "dry run" or a safety check.

Command: terraform plan

What it does: Terraform compares your code (desired state) against what actually exists in the real world (current state). It then outputs a detailed list of exactly what it will do if you apply.

Look for: It will report how many resources it will add, change, or destroy.

**4. Apply (terraform apply)**
This executes the changes.

Command: terraform apply

What it does: It executes the plan. Terraform calls the cloud provider's API to create, update, or delete resources to match your code.

Note: It will ask for confirmation (typing "yes") before proceeding unless you use the -auto-approve flag.

**5. Destroy (terraform destroy)**
(Optional) Used when you want to tear down everything you built.

Command: terraform destroy

What it does: It looks at your state file and removes all infrastructure managed by that specific configuration.


<img width="637" height="228" alt="image" src="https://github.com/user-attachments/assets/2f1f62cd-57f9-48c5-9ed5-27c8438b991f" />



