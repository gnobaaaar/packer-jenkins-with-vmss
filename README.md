# packer-jenkins-with-vmss


Creating a Linux Azure VM Image Using Packer

1. Install Packer
https://developer.hashicorp.com/packer/tutorials/docker-get-started/get-started-install-cli

```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install packer
```


2. Create an Azure Resource Group
Create a resource group to build, create, and store the source image.
```
az group create -n myResourceGroup -l koreacentral
```


3. Create Azure Credentials
Create credentials with Contributor role within the subscription.
```
az ad sp create-for-rbac --role Contributor --scopes /subscriptions/<subscription_id> --query "{ client_id: appId, client_secret: password, tenant_id: tenant }"
```
Example Output
```
{
    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
}
```


4. Define the Packer Template
Refer to the packer-test.json file.



5. Build the Image
```
sudo ./packer build ubuntu.json
```
