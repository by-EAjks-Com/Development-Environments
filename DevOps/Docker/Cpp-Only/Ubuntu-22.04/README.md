# Building and Deploying for Ubuntu 22.04

```powershell
cd /Path/To/Development-Environments
$timestamp = (get-date -format 'yyyyMMdd')
```

## Build

```powershell
docker build --pull `
    --file DevOps/Docker/Cpp-Only/Ubuntu-22.04/Runtime/Base/Dockerfile `
    --tag eajkseajks/cpp-only:ubuntu-22.04-runtime-base-$timestamp `
    --tag eajkseajks/cpp-only:ubuntu-22.04-runtime-base-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-only `
    --build-arg IMAGE_TAG=ubuntu-22.04-runtime-base-$timestamp `
    --file DevOps/Docker/Cpp-Only/Ubuntu-22.04/Runtime/Core/Dockerfile `
    --tag eajkseajks/cpp-only:ubuntu-22.04-runtime-core-$timestamp `
    --tag eajkseajks/cpp-only:ubuntu-22.04-runtime-core-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-only `
    --build-arg IMAGE_TAG=ubuntu-22.04-runtime-core-$timestamp `
    --file DevOps/Docker/Cpp-Only/Ubuntu-22.04/Runtime/Full/Dockerfile `
    --tag eajkseajks/cpp-only:ubuntu-22.04-runtime-full-$timestamp `
    --tag eajkseajks/cpp-only:ubuntu-22.04-runtime-full-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-only `
    --build-arg IMAGE_TAG=ubuntu-22.04-runtime-core-$timestamp `
    --file DevOps/Docker/Cpp-Only/Ubuntu-22.04/SDK/Core/Dockerfile `
    --tag eajkseajks/cpp-only:ubuntu-22.04-sdk-core-$timestamp `
    --tag eajkseajks/cpp-only:ubuntu-22.04-sdk-core-latest `
    .
```

```powershell
docker build `
    --build-arg IMAGE_REPOSITORY=eajkseajks `
    --build-arg IMAGE_NAME=cpp-only `
    --build-arg IMAGE_TAG=ubuntu-22.04-sdk-core-$timestamp `
    --file DevOps/Docker/Cpp-Only/Ubuntu-22.04/SDK/Full/Dockerfile `
    --tag eajkseajks/cpp-only:ubuntu-22.04-sdk-full-$timestamp `
    --tag eajkseajks/cpp-only:ubuntu-22.04-sdk-full-latest `
    .
```

## Deploy

```powershell
docker login
docker push eajkseajks/cpp-only:ubuntu-22.04-runtime-base-$timestamp
docker push eajkseajks/cpp-only:ubuntu-22.04-runtime-base-latest
docker push eajkseajks/cpp-only:ubuntu-22.04-runtime-core-$timestamp
docker push eajkseajks/cpp-only:ubuntu-22.04-runtime-core-latest
docker push eajkseajks/cpp-only:ubuntu-22.04-runtime-full-$timestamp
docker push eajkseajks/cpp-only:ubuntu-22.04-runtime-full-latest
docker push eajkseajks/cpp-only:ubuntu-22.04-sdk-core-$timestamp
docker push eajkseajks/cpp-only:ubuntu-22.04-sdk-core-latest
docker push eajkseajks/cpp-only:ubuntu-22.04-sdk-full-$timestamp
docker push eajkseajks/cpp-only:ubuntu-22.04-sdk-full-latest
```
