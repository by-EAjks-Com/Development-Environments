# Build

```powershell
cd /Path/To/EAjksceleration
$tag = 'v1-ubuntu-20.04-'
$tag_timestamp = $tag + (get-date -format 'yyyyMMdd')
$tag_latest = $tag + 'latest'
```

## Runtime/Base

```powershell
docker build --no-cache --pull `
    --file DevOps/Docker/Base/Python-TensorFlow/v1/Ubuntu-20.04/Dockerfile `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/python-tensorflow:$tag_timestamp `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/python-tensorflow:$tag_latest `
    .
```

# Test

## Any Host Machine

```powershell
docker run --rm -it registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/python-tensorflow:$tag_timestamp /bin/bash
```

# Deploy

## To Registry.by-EAjks.Com

```powershell
docker login registry.by-eajks.com
docker push  registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/python-tensorflow:$tag_timestamp
```

## To Amazon ECR

```powershell
aws --profile Shared-Services ecr-public get-login-password --region us-east-1 | `
docker login --username AWS --password-stdin public.ecr.aws/m9r5r9o5
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/python-tensorflow:$tag_timestamp
```
