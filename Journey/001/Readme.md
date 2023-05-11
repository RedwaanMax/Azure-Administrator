
# Tagging Resources in Azure
(![image](https://github.com/RedwaanMax/Azure-Administrator/assets/130489929/3724c07f-e31a-4c94-bf49-959762284bfe)

## Introduction

✍️ In the scenario for this hands-on lab, the finance department has reached out to you. They are requesting additional taxonomy information on a recent Azure bill, including who created the resources, which department budget should be used for the resources, and if the resources are necessary for running business critical systems.

If there are any non-essential business systems, they ask that you signify that in some way.

## Prerequisite

✍️ In the Azure Portal, click the Cloud Shell icon (>_ ) in the upper right.
Select PowerShell.
Click Show advanced settings.
Use the same region as the lab provided storage account and the existing resource group. Create a new Storage account (use a globally unique name).
For File share, select Create new and give it a name of "fileshare".
Click Create storage.
Note: You need to create resource group(s) and storage account before starting this lab.

## Use Case

- Process Diagram

(![image](https://github.com/RedwaanMax/Azure-Administrator/assets/130489929/78113878-ff94-485a-8d70-25731f43cb3b)
- ✍️  Add, Remove and Update Tags for Resources in Azure

## Cloud Research

During my exploration of Azure tags, I grappled with the concept that tags don't inherently support inheritance. This presented a difficulty     when trying to apply uniform taxonomy across nested resources, as tags applied at the resource group level don't automatically propagate to the resources within.

This peculiarity required a more manual approach to tagging, which could become labor-intensive in larger environments. Going forward, I intend to research more on automated tagging solutions to overcome this challenge and improve the efficiency of resource management in Azure.

### Step 1 — List the resource groups in Powershell:
az group list

(![image](https://github.com/RedwaanMax/Azure-Administrator/assets/130489929/927ffe9e-9f0f-4ae9-a61f-a549bfb2c519)
### Step 2 — Copy the group name.


### Step 3 — Update the resource group tags:
`az group update --resource-group "<RESOURCE_GROUP_NAME>" --tags "Environment=Production" "Dept=IT" "CreatedBy=<YourName>"`

(![image](https://github.com/RedwaanMax/Azure-Administrator/assets/130489929/e8ea2d1f-97f3-4122-a42e-38af3d9b4c16)

### Remove Tags for VM and Mark for Deletion

### Step 4 — In the Cloud Shell, list the existing virtual machines:

`az vm list --query '[].{name:name, resourceGroup:resourceGroup, tags:tags}' -o json`




### Step 5 — Remove the existing tags from the VM:
`az vm update -g "<RESOURCE_GROUP_NAME>" -n webvm1 --remove tags.defaultExperience`


### Step 6 — Mark the VM for deletion:
`az vm update -g "<RESOURCE_GROUP_NAME>" -n webvm1 --set tags.MarkForDeletion=Yes`



### Step 7 — Remove the existing tags from the VM:
`az vm update -g "<RESOURCE_GROUP_NAME>" -n webvm1 --remove tags.defaultExperience`


### Step 8 — Mark VM For Deletion:
`az vm update -g "<RESOURCE_GROUP_NAME>" -n webvm1 --set tags.MarkForDeletion=Yes`

## Change Tags for the Virtual Network

## Step 9 - list the virtual networks:
az network vnet list --query '[].{name:name, resourceGroup:resourceGroup, tags:tags}' -o json
(![image](https://github.com/RedwaanMax/Azure-Administrator/assets/130489929/46862105-ec71-48e5-a1df-52810d4839c0)
## Step 10 - Overwrite the existing tags:
`az resource tag --tags "Dept=IT" "Environment=Production" "CreatedBy=<YourName>" --resource-group "<RESOURCE_GROUP_NAME>" -n "vnet1" --resource-type "Microsoft.Network/virtualNetworks"`
This command has now changed the department tag from 'MyDepartment' to 'IT'

(![image](https://github.com/RedwaanMax/Azure-Administrator/assets/130489929/bdaf20bf-fee8-4645-99de-a316baa2920e)

## ☁️ Cloud Outcome

✍️ This hands-on lab on Azure resource tagging has significantly boosted my understanding of effective resource management. I learned the importance of taxonomy in identifying resource origins, responsibilities, and criticality.

Practically applying Azure Cloud Shell commands to add, update, and remove tags from resources like a resource group, VM, and virtual network underscored their utility in real-world scenarios. This experience has refined my skills in managing and streamlining Azure resources, an asset that will undoubtedly serve me well in future endeavors..

## Next Steps

✍️ Moving forward, I plan to delve into automated tagging strategies using Azure Policies or Functions. I'm also interested in exploring cost management in Azure, particularly how tagging can assist in cost tracking. Ultimately, I aim to apply these skills in a practical project.

## Social Proof

✍️ Show that you shared your process on Twitter or LinkedIn

[link](link)
