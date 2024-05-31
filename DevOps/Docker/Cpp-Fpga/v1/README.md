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
    --file DevOps/Docker/Base/Cpp-Fpga/v1/Ubuntu-20.04/Runtime/Base/Dockerfile `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/base:$tag_timestamp `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/base:$tag_latest `
    .
```

## Runtime/Core

```powershell
docker build --no-cache `
    --build-arg IMAGE_REPOSITORY=registry.by-eajks.com/by-eajks.com/value-propositions `
    --build-arg IMAGE_NAME=eajksceleration/cpp-fpga/runtime/base `
    --build-arg IMAGE_TAG=$tag_timestamp `
    --file DevOps/Docker/Base/Cpp-Fpga/v1/Ubuntu-20.04/Runtime/Core/Dockerfile `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/core:$tag_timestamp `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/core:$tag_latest `
    .
```

## Runtime/Full

```powershell
docker build --no-cache `
    --build-arg IMAGE_REPOSITORY=registry.by-eajks.com/by-eajks.com/value-propositions `
    --build-arg IMAGE_NAME=eajksceleration/cpp-fpga/runtime/core `
    --build-arg IMAGE_TAG=$tag_timestamp `
    --file DevOps/Docker/Base/Cpp-Fpga/v1/Ubuntu-20.04/Runtime/Full/Dockerfile `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/full:$tag_timestamp `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/full:$tag_latest `
    .
```

## SDK/Core

```powershell
docker build --no-cache `
    --build-arg IMAGE_REPOSITORY=registry.by-eajks.com/by-eajks.com/value-propositions `
    --build-arg IMAGE_NAME=eajksceleration/cpp-fpga/runtime/core `
    --build-arg IMAGE_TAG=$tag_timestamp `
    --file DevOps/Docker/Base/Cpp-Fpga/v1/Ubuntu-20.04/SDK/Core/Dockerfile `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/core:$tag_timestamp `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/core:$tag_latest `
    .
```

## SDK/Full

```powershell
docker build --no-cache `
    --build-arg IMAGE_REPOSITORY=registry.by-eajks.com/by-eajks.com/value-propositions `
    --build-arg IMAGE_NAME=eajksceleration/cpp-fpga/sdk/core `
    --build-arg IMAGE_TAG=$tag_timestamp `
    --file DevOps/Docker/Base/Cpp-Fpga/v1/Ubuntu-20.04/SDK/Full/Dockerfile `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/full:$tag_timestamp `
    --tag registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/full:$tag_latest `
    .
```

# Test

## Any Host Machine with Xilinx ALVEO U50 Card(s)

```powershell
DEVICES=""
for xclf in /dev/xclmgmt*
do
    DEVICES="$DEVICES --device=$xclf:$xclf"
done
for usrf in /dev/dri/renderD*
do
    DEVICES="$DEVICES --device=$usrf:$usrf"
done
```

```powershell
docker run --rm $DEVICES -it registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/base:$tag_timestamp /bin/bash
docker run --rm $DEVICES -it registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/core:$tag_timestamp /bin/bash
docker run --rm $DEVICES -it registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/full:$tag_timestamp /bin/bash
docker run --rm $DEVICES -it registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/core:$tag_timestamp /bin/bash
docker run --rm $DEVICES -it registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/full:$tag_timestamp /bin/bash
```

```powershell
. /opt/xilinx/xrt/setup.sh
xbutil scan
xbutil validate
```

# Deploy

## To Registry.by-EAjks.Com

```powershell
docker login registry.by-eajks.com
docker push  registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/base:$tag_timestamp
docker push  registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/core:$tag_timestamp
docker push  registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/runtime/full:$tag_timestamp
docker push  registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/core:$tag_timestamp
docker push  registry.by-eajks.com/by-eajks.com/value-propositions/eajksceleration/cpp-fpga/sdk/full:$tag_timestamp
```

## To Amazon ECR

```powershell
aws --profile Shared-Services ecr-public get-login-password --region us-east-1 | `
docker login --username AWS --password-stdin public.ecr.aws/m9r5r9o5
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-fpga/runtime/base:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-fpga/runtime/core:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-fpga/runtime/full:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-fpga/sdk/core:$tag_timestamp
docker push  public.ecr.aws/m9r5r9o5/eajksceleration/cpp-fpga/sdk/full:$tag_timestamp
```
