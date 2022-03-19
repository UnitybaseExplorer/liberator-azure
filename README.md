# Create Container Instances with disbalacer on MS Azure
Deploy liberator on MS Azure

## Prepare on Windows
- Create Azure Account https://dou.ua/forums/topic/36795/ Порядок действий (пункти 1 - 9)
- Install azure-cli https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli


## Create Containers
- run powershell

- login to azure via powershell:
`az login`

- create resource-group:
`az group create --location centralus --name disliberator`

- set regions array:
`$regions=@("northeurope", "westeurope", "canadacentral", "uaenorth", "centralus", "brazilsouth", "koreacentral", "switzerlandwest", "australiaeast", "brazilsouth")`

- create container:
`for ($num = 0; $num -le 9; $num++) {az container create --resource-group disliberator --name liberator-$num --image docker.io/ubexplorer/liberator --dns-name-label $([guid]::NewGuid().Guid) --ports 80 --location $regions[$num] --cpu 1 --memory 0.5}`


## Monitor Containers

- container logs:
 `($num = 0; $num -le 9; $num++) {Write-Host "Container liberator-$num"; az container logs --resource-group disliberator --name liberator-$num}`

- container restart:
`for ($num = 0; $num -le 9; $num++) {az container restart --resource-group disliberator --name liberator-$num}`

- container delete:
`for ($num = 0; $num -le 9; $num++) {az container delete --resource-group disliberator --name liberator-$num --yes}`
