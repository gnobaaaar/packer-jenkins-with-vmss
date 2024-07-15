# packer-jenkins-with-vmss


Creating a Linux Azure VM Image Using Packer
<br/>
1. Install Packer<br/>
https://developer.hashicorp.com/packer/tutorials/docker-get-started/get-started-install-cli
<br/>
```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install packer
```
<br/><br/>

2. Create an Azure Resource Group<br/>
Create a resource group to build, create, and store the source image.<br/>
```
az group create -n myResourceGroup -l koreacentral
```
<br/><br/>

3. Create Azure Credentials<br/>
Create credentials with Contributor role within the subscription.<br/>
```
az ad sp create-for-rbac --role Contributor --scopes /subscriptions/<subscription_id> --query "{ client_id: appId, client_secret: password, tenant_id: tenant }"
```
<br/>
Example Output<br/>
```
{
    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
}
```
<br/><br/>

4. Define the Packer Template<br/>
Refer to the packer-test.json file.<br/>

<br/><br/>

5. Build the Image<br/>
```
sudo ./packer build ubuntu.json
```
