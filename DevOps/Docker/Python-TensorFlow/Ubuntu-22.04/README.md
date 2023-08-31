# Building and Deploying for Ubuntu 22.04

```powershell
cd /Path/To/Development-Environments
$timestamp = (get-date -format 'yyyyMMdd')
```

# Build

```powershell
docker build --pull `
    --file DevOps/Docker/Python-TensorFlow/Ubuntu-22.04/Dockerfile `
    --tag eajkseajks/python-tensorflow:ubuntu-22.04-$timestamp `
    --tag eajkseajks/python-tensorflow:ubuntu-22.04-latest `
    .
```

## Deploy

```powershell
docker login
docker push eajkseajks/python-tensorflow:ubuntu-22.04-$timestamp
docker push eajkseajks/python-tensorflow:ubuntu-22.04-latest
```
