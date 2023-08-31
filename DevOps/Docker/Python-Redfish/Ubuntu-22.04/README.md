# Building and Deploying for Ubuntu 22.04

```powershell
cd /Path/To/Development-Environments
$timestamp = (get-date -format 'yyyyMMdd')
```

## Build

```powershell
docker build --pull `
    --file DevOps/Docker/Python-Redfish/Ubuntu-22.04/Dockerfile `
    --tag docker.io/eajkseajks/python-redfish:ubuntu-22.04-$timestamp `
    --tag docker.io/eajkseajks/python-redfish:ubuntu-22.04-latest `
    .
```

## Deploy to Docker.IO

```powershell
docker login
docker push docker.io/eajkseajks/python-redfish:ubuntu-22.04-$timestamp
docker push docker.io/eajkseajks/python-redfish:ubuntu-22.04-latest
```
