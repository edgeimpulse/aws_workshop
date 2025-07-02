
## AWS IoT Greengrass Installation

The following sections outline how one installs AWS IoT Greengrass... then installs the Edge Impulse custom components for inclusion into a Greengrass deployment down to edge devices. 

Log into your edge device via SSH and we'll start the process of installing/configuring Greengrass. 

### 1. Install AWS IoT Greengrass Prerequisites

AWS IoT Greengrass is based on Java and thus a Java runtime must be installed. For most linux-based devices a suitable Java can be run by simply typing:

	Debian-based Linux:

			% sudo apt install -y default-jdk

	Redhat-based Linux: 

			% sudo yum install -y default-jdk

Additionally, its recommended to update your linux device with the latest security patches and updates if available. 

### 2. Install AWS IoT Greengrass

Greengrass is typically installed from within the AWS Console -> AWS IoT Core -> Greengrass -> Core Devices menu... select/press "Set up one core device". There are multiple ways to install Greengrass - "Nucleus Classic" is the version of Greengrass that is based on Java.  "Nucleus Lite" is a native version of Greengrass that is typically part of a Yocto-image based implementation. 

In this example, we choose the "Linux" device type and we are going to download the installer for Greengrass and invoke it as part of the installation of a "Nucleus Classic" instance:

![CreateDevice](GG_Install_Device.png)

Lower down in the menu, you will see the specific instructions that are custom-crafted for you to download and invoke the "Nucleus Classic" installer. Note that you will have to have previously created and set, within your shell environment, an AWS Access Key (typically with Administrator privilege) in order to run the installer:

 ![CreateDevice](GG_Install_Device2.png)

### 3. Install defaulted AWS IoT Greengrass components

When doing a Greengrass installation/deployment, a default deployment for the target device will typically get created and that deployment will install the two components below.  If one is not created, it is recommended that you create a deployment in Greengrass for your newly added Greengrass edge device and add the following available AWS Components:

			aws.greengrass.Cli
			aws.greengrass.Nucleus

### 4. Modify the Greengrass TokenExchange Role with additional permissions

When you run a Greengrass component within Greengrass, a service user (typically a linux user called "ggc_user" for "Nucleus Classic" installations) invokes the component, as specified in the lifecycle section of your recipe. Credentials are passed to the invoked process via its environment (NOT by the login environment of the "Greengrassc_user"...) during the invocation spawning process. These credentials are used by by the spawned process (typically via the AWS SDK which is part of the spawned process...) to connect back to AWS and "do stuff". These permissions are controlled by a AWS IAM Role called "GreengrassV2TokenExchangeRole".  We need to modify that role and add "Full AWS IoT Core Permission" as well as "AWS Secrets Manager Read/Write" permission.

To modify the role, from the AWS Console -> IAM -> Roles search for "GreengrassV2TokenExchangeRole", Then:

	1. Select "GreengrassV2TokenExchangeRole" in the search results list
	2. Select "Add Permissions" -> "Attach Policies"
	3. Search for "AWSIoTFullAccess", select it, then press "Add Permission" down at the bottom
	4. Repeat the search for "S3FullAccess" and "SecretsManagerReadWrite"

![TERUpdate](IAM_TER_Update.png)

When done, your GreengrassV2TokenExchangeRole should now show that it has "AWSIoTFullAccess", "S3FullAccess" and "SecretsManagerReadWrite" permissions added to it.

Next, we will pull over and configure the EdgeImpulse Custom component used to deploy Edge Impulses' model execution runtime. Lets do this!

[Back](../2_EdgeImpulseProjectBuild/EdgeImpulseProjectBuild.md) [Next](../4_SecretsManagerSetup/SecretManagerSetup.md)