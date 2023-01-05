# Build

```powershell
cd /Path/To/Development-Environments
$timestamp = (get-date -format 'yyyyMMdd')
```

## Ubuntu 22.04

```powershell
docker build --pull `
    --file DevOps/Docker/Cpp-Cuda/v1/Ubuntu-22.04/Runtime/Base/Dockerfile `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-base-$timestamp `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-base-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-cuda `
    --build-arg IMAGE_TAG=v1-ubuntu-22.04-runtime-base-$timestamp `
    --file DevOps/Docker/Cpp-Cuda/v1/Ubuntu-22.04/Runtime/Core/Dockerfile `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-core-$timestamp `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-core-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-cuda `
    --build-arg IMAGE_TAG=v1-ubuntu-22.04-runtime-core-$timestamp `
    --file DevOps/Docker/Cpp-Cuda/v1/Ubuntu-22.04/Runtime/Full/Dockerfile `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-full-$timestamp `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-full-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-cuda `
    --build-arg IMAGE_TAG=v1-ubuntu-22.04-runtime-core-$timestamp `
    --file DevOps/Docker/Cpp-Cuda/v1/Ubuntu-22.04/SDK/Core/Dockerfile `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-core-$timestamp `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-core-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-cuda `
    --build-arg IMAGE_TAG=v1-ubuntu-22.04-sdk-core-$timestamp `
    --file DevOps/Docker/Cpp-Cuda/v1/Ubuntu-22.04/SDK/Full/Dockerfile `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-full-$timestamp `
    --tag eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-full-latest `
    .
```

```powershell
docker login
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-base-$timestamp
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-base-latest
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-core-$timestamp
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-core-latest
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-full-$timestamp
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-runtime-full-latest
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-core-$timestamp
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-core-latest
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-full-$timestamp
docker push eajkseajks/cpp-cuda:v1-ubuntu-22.04-sdk-full-latest
```

# Test

## Any Host Machine

```powershell
docker run --rm -it eajkseajks/cpp-cuda/runtime/base:$tag_timestamp /bin/bash
docker run --rm -it eajkseajks/cpp-cuda/runtime/core:$tag_timestamp /bin/bash
docker run --rm -it eajkseajks/cpp-cuda/runtime/full:$tag_timestamp /bin/bash
docker run --rm -it eajkseajks/cpp-cuda/sdk/core:$tag_timestamp /bin/bash
docker run --rm -it eajkseajks/cpp-cuda/sdk/full:$tag_timestamp /bin/bash
```

# Deploy

## To Registry.by-EAjks.Com

```powershell
docker login registry.by-eajks.com
docker push  eajkseajks/cpp-cuda/runtime/base:$tag_timestamp
docker push  eajkseajks/cpp-cuda/runtime/core:$tag_timestamp
docker push  eajkseajks/cpp-cuda/runtime/full:$tag_timestamp
docker push  eajkseajks/cpp-cuda/sdk/core:$tag_timestamp
docker push  eajkseajks/cpp-cuda/sdk/full:$tag_timestamp
```

## To Amazon ECR

```powershell
aws --profile Shared-Services ecr-public get-login-password --region us-east-1 | `
docker login --username AWS --password-stdin public.ecr.aws/m9r5r9o5
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-cuda/runtime/base:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-cuda/runtime/core:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-cuda/runtime/full:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-cuda/sdk/core:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-cuda/sdk/full:$tag_timestamp
```
