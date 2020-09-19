# Create new Azure SQL Server and one database

**Parameters**:

- serverName
- administratorLogin
- administratorLoginPassword

## Azure CLI script

### Login to the Azure account

```bash
az login
az account set --subscription [SubscriptionName]
```

### Set some parameters for the template

Modify these variables:

```bash
projectName="POC-daniel-test"
sqlDBName="SampleDB"
administratorLogin="adminsuser"
administratorLoginPassword="adminpass#1"
templateFile="azuredeploy.json"
```

### Create resource group

```bash
resourceGroupName="${projectName}-rg"
az group create \
  --name $resourceGroupName \
  --location "East US 2"
```

### Deploy the template

```bash
az deployment group create \
  --name DeploySQLFromLocalTemplate \
  --resource-group $resourceGroupName \
  --template-file $templateFile \
  --parameters  \
  serverName="${projectName}-sql" \
  sqlDBName="$sqlDBName" \
  administratorLogin=$administratorLogin \
  administratorLoginPassword=$administratorLoginPassword \
```